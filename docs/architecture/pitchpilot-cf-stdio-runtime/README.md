# Live architecture diagram

`pp-cf.mmd` is the **single source of truth** for the pitchpilot-cf box on the
live architecture site:

- **https://livedoc.greeep.com/arch/** (Standalone tab group)

The site reads this file straight from `origin/dev` (via `git show`) on every
load and re-renders it with Mermaid. pitchpilot-cf is a **standalone** project
(no arx / arx-cf), so it stands on its own group. There is no separate publish
step — **merging an update to `dev` is the publish.** The site also shows this
file's latest commit SHA / message / timestamp.

> Note: this repo otherwise runs a single environment and ships code from
> `main`. The `dev` branch exists here only so the diagram tracks the same
> branch as every other node on the live site. Land diagram updates on `dev`
> (e.g. merge `main`→`dev`, or commit straight to `dev`).

## Current Runtime Shape

As of 2026-06-16, the default agent path is a resident Cloudflare Sandbox
bridge that talks directly to Claude Code over stdio stream-json. ACP is no
longer the default runtime path.

Hot path:

```text
Browser
  -> Worker route
  -> DeckDO
  -> AgentSandbox DO
  -> pp-agent-bridge.mjs
  -> claude -p --input-format stream-json --output-format stream-json
```

Return path:

```text
Claude stream-json stdout
  -> pp-agent-bridge.mjs
  -> runtime/tool events over bridge WebSocket
  -> stream deltas and turn finalization over internal HTTP endpoints
  -> DeckDO timeline fanout
  -> Browser SSE
```

DeckDO is still the authoritative per-deck coordination point for queueing,
watchdog supervision, timeline fanout, and session/runtime cache metadata.

## The rule

**Every iteration that changes the architecture MUST update `pp-cf.mmd` in the
same PR.** Adding a route group, a Durable Object, a binding, or changing the
agent/turn path (DeckDO ↔ AgentSandbox ↔ Anthropic) — if the boxes-and-arrows
change, the diagram changes with it. A PR that alters the architecture but
leaves this file stale is incomplete. See the matching rule in the repo root
`CLAUDE.md`.

## Editing

Plain [Mermaid](https://mermaid.js.org/) `flowchart` text — diffable in review.
Keep it at the **architecture** altitude. Preserve the `classDef` styles so all
the diagrams stay visually consistent. Preview at <https://mermaid.live>.
