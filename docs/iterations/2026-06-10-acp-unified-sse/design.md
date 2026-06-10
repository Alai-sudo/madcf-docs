# ACP-Native Unified SSE

## Goal

Make ACP the runtime boundary for PitchPilot CF and collapse the frontend deck streaming surface to one SSE connection per open deck.

The desired runtime path is:

1. The sandbox agent adapter receives ACP JSON-RPC updates from `claude-agent-acp`.
2. The adapter forwards ACP-native updates and adds only the minimal PitchPilot system events that ACP does not provide directly.
3. The Worker forwards those events into the deck Durable Object.
4. DeckDO persists them as activity, projects them into timeline items, and broadcasts one ordered timeline stream.
5. The frontend opens one EventSource and dispatches chat, activity, preview refresh, context refresh, and connection status from that single stream.

## Current Problems

- The web app currently opens multiple EventSource connections for the same deck:
  - `useDeckEvents`
  - `useDeckChat`
  - `useDeckActivity`
- Chat and activity are rendered from separate live handlers and separate REST backfills.
- ACP updates are only partially normalized. The first ACP integration emits `driver_event`, but the frontend still maps it through the old activity-only hook.
- `/timeline` exists, but it is not the frontend source of truth yet.

## Event Model

Use ACP as the compatibility layer. Do not introduce Mosoo Driver vocabulary as a second canonical protocol.

The sandbox adapter should preserve ACP-native semantics:

- ACP `initialize` result stays runtime metadata.
- ACP `session/new` and `session/load` results stay session metadata.
- ACP `session/update` notifications remain the main live event stream.
- ACP `session/prompt` result remains the turn completion signal.
- ACP `session/request_permission` remains the permission request shape.

PitchPilot may add a small system envelope around these events so the Worker and frontend can route them consistently:

```json
{
  "source": "acp",
  "phase": "session.update",
  "turn_id": "...",
  "session_id": "...",
  "payload": { "...": "original ACP payload or result" }
}
```

Allowed PitchPilot-only events are limited to product state that ACP does not know about:

- `pp.run.started`
- `pp.run.completed`
- `pp.run.failed`
- `pp.preview.artifact_updated`
- `pp.preview.version_created`
- `pp.context.updated`
- `pp.session.resume_updated`

During rollout the sandbox adapter may continue posting legacy `/stream-delta` and `/tool-event`, but the unified frontend should rely on ACP/system timeline items for normal live rendering.

## Backend Approach

### Sandbox ACP Adapter

- Add a small ACP event forwarder inside `containers/oasis/pp-cli/lib/adapters/acp.mjs`.
- Preserve existing callback behavior for compatibility:
  - `cbs.onText()` still posts `/stream-delta`.
  - `notifyToolEvent()` still posts `/tool-event`.
  - turn finalization remains unchanged.
- Emit ACP/system timeline events in the right order:
  - before `session/prompt`, emit `pp.run.started`.
  - forward every ACP `session/update` payload as `acp.session.update`.
  - on ACP `session/request_permission`, emit `acp.permission.requested` and the selected result as `acp.permission.resolved`.
  - after successful `session/prompt`, emit `pp.run.completed` with the original prompt result.
  - on prompt failure, emit `pp.run.failed`.
- Use stable identifiers:
  - `run_id` = `PP_TURN_ID`
  - `messageId` = `PP_REPLY_MESSAGE_ID`
  - `toolCallId` from ACP when present.

### Internal Route

- Rename or generalize the current `/api/internal/decks/:id/driver-event` route to an ACP/system event endpoint.
- Accept minimal envelopes:
  - `{ kind, payload, run_id, source, turn_id, event_id?, occurred_at? }`
- `kind` should be either an ACP projection such as `acp.session.update` or a PitchPilot system event such as `pp.run.completed`.
- Validate only the structural minimum at this layer; unknown ACP event payloads should be preserved, not dropped.

### DeckDO Timeline Projection

- Keep the current additive storage model for this iteration:
  - messages table remains message source of truth.
  - activity table stores ACP/system event rows.
  - `/timeline` synthesizes ordered rows from messages and activity.
- Strengthen timeline projection shape:
  - `item_type: "message" | "activity" | "context" | "turn"`
  - `payload.kind` for activity rows.
  - stable synthetic ids: `msg:<id>` and `act:<id>`.
- Broadcast named SSE events from the same `/events` endpoint:
  - continue legacy `message`, `activity`, `context`, `turn`.
  - use `timeline` as the frontend source for chat and activity.

No schema migration is planned in this iteration. A dedicated monotonic timeline table can follow after the contract is stable.

## Frontend Approach

### New Single Hook

Create `apps/web/src/hooks/useDeckTimeline.ts`.

Responsibilities:

- Backfill from `GET /api/decks/:id/timeline?limit=...`.
- Open one `EventSource` to `GET /api/decks/:id/events`.
- Listen to named events on that one connection:
  - `timeline` for ordered message and activity rendering.
  - `context` for context refresh.
  - legacy `activity` only for preview refresh until all preview events have a timeline projection.
  - `turn` for future compatibility.
- Deduplicate by timeline id and by legacy event id.
- Expose the existing handler semantics currently split across:
  - `DeckChatHandlers`
  - `DeckActivityHandlers`
  - `DeckEventHandlers`
- Preserve reconnect behavior:
  - connection status callback.
  - missed message REST reconciliation on reconnect if needed.
  - history loaded callback after backfill.

### App Integration

- Replace `useDeckEvents`, `useDeckChat`, and `useDeckActivity` calls in `App.tsx` with one `useDeckTimeline` call.
- Reuse existing handler bodies where possible by moving local conversion helpers into the unified hook.
- Keep the old hooks in the tree for one release if they are unused, or delete them if TypeScript confirms no imports remain.

### Rendering Rules

- `message` timeline rows render user messages.
- `acp.session.update` with `sessionUpdate=agent_message_chunk` appends to the current assistant streaming bubble.
- Legacy `message_delta` rows still append to the same assistant bubble for rollback compatibility.
- `acp.session.update` with `sessionUpdate=tool_call` or `tool_call_update`, `acp.permission.*`, and legacy tool rows render as activity.
- `pp.run.completed`, `pp.run.failed`, and legacy `turn_ended` finalize the live turn.

## Test Plan

Automated:

- `node --check containers/oasis/pp-cli/lib/adapters/acp.mjs`
- `npm run typecheck --workspaces --if-present`
- `npm test --workspaces --if-present`
- `npm run build --workspaces --if-present`
- `git diff --check`

Local/browser:

- Start the local API/web dev server if practical.
- Open a deck page.
- Verify only one `/api/decks/:id/events` EventSource is open in the browser Network panel.
- Verify chat text and activity appear during generation.
- Verify preview refresh still happens after `artifact_updated` and `version_created`.
- Verify speaker notes/context refresh still works on `context` events.

Deployment loop:

- Deploy without asking for another confirmation.
- Verify the deployed Worker build.
- Run a browser smoke test against the LangGenius Worker URL.
- Capture screenshots/logs under this iteration directory.

## Rollback

- Explicit tulpa `engine_config` can still select `stdin-stream-json`.
- Legacy `message`, `activity`, and `context` SSE events remain broadcast from DeckDO.
- If the unified frontend hook fails, reverting the App import/call sites can restore the old three-hook behavior without touching the sandbox runtime.
