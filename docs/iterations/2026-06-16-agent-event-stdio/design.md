# Agent Event Stdio Runtime

## Goal

Replace the sandbox agent runtime's ACP adapter path with a Claude Code native stdio stream path.

The runtime should stop depending on `claude-agent-acp` for PitchPilot turns. The resident sandbox bridge should launch Claude Code directly with stream JSON input/output, parse engine events into PitchPilot normalized timeline events, and keep the existing DeckDO/browser fanout path stable.

## References

- ARX stdin adapter: `/home/ubuntu/arx/crates/arx-bridge/src/adapter/stdin.rs`
- ARX stream parser: `/home/ubuntu/arx/crates/arx-bridge/src/engine.rs`
- ARX normalized event model: `origin/refactor/acp-protocol-events:crates/arx-core/src/agent_protocol.rs`
- ARX Claude Code engine manifest: `/home/ubuntu/arx/engines/claude-code/engine.toml`
- Current PP-CF bridge: `containers/oasis/pp-cli/bin/pp-agent-bridge.mjs`
- Current PP-CF runtime resolver: `apps/api/src/agent/engine.ts`
- Current PP-CF sandbox methods: `apps/api/src/durable/AgentSandbox.ts`
- Current PP-CF DeckDO dispatch: `apps/api/src/durable/DeckDO.ts`

The exact ARX document path named by the user was not present in the local ARX checkout, including `origin/refactor/acp-protocol-events`. The implementation will use the matching ARX code and nearby design documents listed above.

## Current State

PP-CF currently has a resident bridge process, but its engine protocol is ACP:

```text
DeckDO
  -> AgentSandbox DO
  -> pp-agent-bridge.mjs
  -> claude-agent-acp
  -> Claude Code
```

Events return to DeckDO through the bridge event WebSocket or HTTP fallback:

```text
pp-agent-bridge.mjs
  -> /api/internal/decks/:id/agent-events-ws
  -> DeckDO timeline normalization and browser fanout
```

The latency and maintenance problem is the middle ACP adapter. `pp-agent-bridge.mjs` speaks JSON-RPC ACP, maps ACP `session/update` into PitchPilot events, and DeckDO only enables the persistent runtime when `engineTransport === "acp"`.

## Target Architecture

Use Claude Code's native print/stdio stream mode:

```text
DeckDO
  -> AgentSandbox DO
  -> pp-agent-bridge.mjs
  -> claude -p --input-format stream-json --output-format stream-json --verbose --permission-mode bypassPermissions --include-partial-messages
```

The resident bridge remains the sandbox boundary and keeps the same local HTTP/IPC control surface:

- `GET /status`
- `POST /warmup`
- `POST /prompt`
- `POST /cancel`
- `POST /shutdown`

The bridge no longer sends ACP `initialize`, `session/new`, `session/load`, `session/prompt`, or `session/cancel`. It writes one JSONL user message per turn to Claude stdin and parses Claude stdout line by line.

## Runtime Command

Default engine config should become:

```json
{
  "kind": "sandbox",
  "transport": "stdin-stream-json",
  "binary": "claude",
  "args": [
    "-p",
    "--input-format", "stream-json",
    "--output-format", "stream-json",
    "--verbose",
    "--permission-mode", "bypassPermissions",
    "--include-partial-messages"
  ],
  "message_template": "{\"type\":\"user\",\"message\":{\"role\":\"user\",\"content\":\"{message}\"}}",
  "done_event": "result"
}
```

When a valid previous Claude session id exists, the bridge should launch with resume args:

```text
--resume <session_id>
```

The bridge should still pass:

- `ANTHROPIC_API_KEY`
- selected model
- `CLAUDE.md` in the workspace
- append system prompt through `--append-system-prompt` or `--append-system-prompt-file` if available
- allowed tools / permission mode

## Event Model

The internal UI should stop treating ACP as the event vocabulary.

Bridge output should normalize Claude stream JSON into PitchPilot event frames that match the existing DeckDO fanout shape:

| Claude stream-json | PitchPilot frame |
|---|---|
| `stream_event.content_block_delta` text delta | `/stream-delta` |
| `stream_event.content_block_start` thinking | runtime event `agent.thinking.started` |
| `stream_event.content_block_delta` thinking delta | runtime event `agent.thinking.delta` |
| `assistant.message.content[].tool_use` | tool event started |
| `user.message.content[].tool_result` | tool event completed or failed |
| `result` | `/turn-finalize` with `claude_session_id` |
| stderr/error pattern | runtime error event and failed finalize |

The raw Claude line should be kept in debug payloads when `debugEvents=1` or equivalent backend debug flag is enabled, but normal user UI should render the normalized categories:

- Thinking
- Message
- Activity
- Error only when actionable

## Attachments

ACP content blocks should be removed from the bridge protocol. AgentSandbox already builds prompt blocks from persisted attachments. For stdio:

- Text attachments become explicit text references in the user message.
- File/resource attachments are materialized in the workspace and referenced by path.
- Images should be materialized in the workspace and referenced in the user message with path and MIME metadata unless Claude stream-json input supports richer blocks reliably in the deployed CLI version.

The first implementation should preserve current file materialization behavior and avoid claiming image binary transport until smoke-tested with the sandbox Claude CLI.

## Session Continuity

The source of truth remains DeckDO storage:

- `claude_session:<tulpaId>`
- `claude_session_prompt_hash:<tulpaId>`
- `claude_session_model:<tulpaId>`
- `agent_runtime_cache`

The bridge extracts `session_id` from Claude `result` or `system init` events and returns it in `/turn-finalize`. DeckDO persists it exactly as today.

If the system prompt hash changes, DeckDO should clear the stored session and restart the resident bridge.

## Warmup Behavior

`/warmup` can no longer perform ACP `initialize/session/new`.

New warmup semantics:

- verify bridge process is reachable;
- verify Claude binary exists;
- write prompt files and system prompt append file;
- optionally start Claude with no prompt only if the CLI supports a harmless ready probe.

The first implementation should keep warmup cheap and not create fake turns. True model work starts at `/prompt`.

## Interrupt Behavior

ACP soft cancel is removed. Stdio Claude Code does not expose the same `session/cancel` RPC.

For this iteration:

- `/cancel` marks the active turn as interrupted;
- sends SIGINT to the Claude child first;
- escalates to SIGTERM if the process does not exit;
- finalizes the turn as interrupted;
- leaves the resident bridge alive and ready to start a fresh Claude process on the next prompt.

This is an interrupt, not a full sandbox destroy.

## Code Changes

1. `apps/api/src/agent/engine.ts`
   - Change default transport from `acp` to `stdin-stream-json`.
   - Change default binary from `claude-agent-acp` to `claude`.
   - Add default stream-json args, message template, done event, and Claude session resume config.
   - Rename comments from `persistent-acp` where they describe a generic resident runtime.

2. `apps/api/src/agent/runtimeCache.ts`
   - Replace `persistent-acp` with a generic resident mode name, likely `persistent-stdio`.
   - Accept old values only if needed for temporary cleanup, but new writes should use the stdio mode.

3. `apps/api/src/durable/DeckDO.ts`
   - Let `stdin-stream-json + persistent-stdio` use `promptPersistentAgent` and fast path.
   - Remove the condition that forces non-ACP transports to `per-turn`.
   - Update warmup support to allow stdio.
   - Keep per-turn `pp-run-agent` as fallback only for explicitly configured per-turn engines.

4. `apps/api/src/durable/AgentSandbox.ts`
   - Pass engine args, message template, done event, and resume session id into the resident bridge.
   - Update status names and timings from ACP-specific labels to stdio/runtime labels.

5. `containers/oasis/pp-cli/bin/pp-agent-bridge.mjs`
   - Replace ACP JSON-RPC child logic with a stdio child manager.
   - Launch Claude directly.
   - Write JSONL user messages to child stdin.
   - Parse stdout stream-json lines.
   - Emit stream deltas, tool events, runtime events, and turn finalize.
   - Preserve bridge event WebSocket and HTTP fallback.
   - Preserve R2 artifact mirroring where file writes can be detected.

6. `containers/oasis/pp-cli/bin/pp-run-agent.mjs`
   - Keep per-turn fallback working.
   - Align default engine binary/config with stdio if it currently defaults to ACP.

7. Tests
   - Add parser tests for Claude stream-json samples.
   - Add runtime cache tests for `persistent-stdio`.
   - Add DeckDO runtime mode resolution tests if local test harness exists.
   - Add a bridge smoke script or unit test that feeds sample JSONL stdout lines and verifies emitted event frames.

## Out of Scope

- Rebuilding the whole frontend timeline UI.
- Replacing DeckDO fanout with direct browser-to-bridge WebSocket.
- Introducing a custom model SDK agent loop.
- Full MCP permission UI.
- Removing every historical ACP file in one pass if not on the active runtime path.

## Test Plan

Local checks:

```bash
pnpm --filter @pitchpilot/api test
pnpm --filter @pitchpilot/api typecheck
node --check containers/oasis/pp-cli/bin/pp-agent-bridge.mjs
node --check containers/oasis/pp-cli/bin/pp-run-agent.mjs
```

Container/runtime smoke:

1. Build sandbox image with the new bridge.
2. Deploy dev Worker using the new image.
3. Create a deck from the browser.
4. Send a simple message and verify:
   - user message appears immediately;
   - first agent event is not delayed by ACP initialize/session calls;
   - stream deltas appear;
   - tool events appear under Activity;
   - turn finalizes with a session id.
5. Send a second message in the same deck and verify:
   - no ACP startup events exist;
   - `--resume` is used when a session id exists;
   - runtime cache fast path works.
6. Trigger interrupt and verify the current child exits while the bridge remains available.
7. Export HTML/PDF/PPTX from the generated deck to ensure the agent-created artifacts still mirror to R2.

## Risks

- Claude Code stream-json input may not preserve all rich ACP content block behavior. Attachments need a conservative file-path based representation first.
- SIGINT cancel semantics may differ from ACP cancel semantics.
- Warmup becomes less powerful because stdio mode has no ACP `initialize/session/new`.
- Existing admin-configured tulpas with `transport: "acp"` may need data cleanup or migration.
- If Claude CLI changes stream-json event shapes, the parser needs version-tolerant raw fallback.

## Rollout

1. Implement behind the default engine config on the feature branch.
2. Deploy to dev only.
3. Smoke test with one newly created deck and one existing deck.
4. Confirm no runtime path launches `claude-agent-acp`.
5. Merge dev after browser verification.
