# Bidirectional Bridge WSS Hot Path

## Goal

Move the browser-to-agent transport to bidirectional WebSockets so browser-visible agent traffic is no longer gated by per-event HTTP callbacks.

Principle: the browser-to-agent path should be as direct as the current Cloudflare topology allows. DeckDO remains the relay, queue, watchdog, and fanout boundary, but persistence is a side effect of the hot path instead of the hot path itself.

## Target Flow

User prompt:

```text
Browser
  -> Worker route (WebSocket upgrade)
  -> DeckDO live websocket relay
  -> bridge WebSocket command
  -> pp-agent-bridge.mjs
  -> Claude Code stdin
```

Agent output:

```text
Claude Code stdout
  -> pp-agent-bridge.mjs
  -> bridge WebSocket frames
  -> DeckDO immediate websocket fanout
  -> Browser
```

Bridge WebSocket frames:

- `bridge_ready`
- `bridge_command`
- `command_result`
- `stream_delta`
- `turn_finalize`
- `runtime_event`
- `tool_event`

Browser live WebSocket frames:

- `deck_command`
- `command_result`
- `timeline`
- `context`
- `connected`

## Scope

Included:

- Make `/agent-events-ws` bidirectional.
- Add `/live-ws` as the browser deck channel for send, interrupt, timeline, and context events.
- Prefer `/live-ws` in the frontend and keep HTTP/SSE fallback.
- Store the active bridge socket in DeckDO.
- Send `prompt`, `warmup`, and `cancel` commands from DeckDO to the bridge over WSS.
- Send `stream_delta` and `turn_finalize` from bridge to DeckDO over WSS.
- Keep internal HTTP endpoints as compatibility fallback when the socket is unavailable.
- Fan out stream deltas before local message-content persistence.
- Keep runtime/tool event persistence deferred.
- Update live architecture docs.

Not included:

- Removing legacy ACP compatibility paths.
- Removing internal HTTP fallback endpoints.
- Deploy smoke test.

## Persistence Rule

DeckDO remains the authoritative place to project the timeline and supervise turns, but write operations are not the transport gate:

- Runtime/tool events already enqueue deferred persistence before SQLite writes.
- Message deltas now publish to browser listeners before appending to DO SQLite.
- Turn finalization still performs required state transitions synchronously because it closes the turn and updates session pointers.

## Test Plan

- JavaScript syntax check for bridge and runner.
- API TypeScript typecheck.
- Runtime cache tests.
- Bridge event normalization tests.
