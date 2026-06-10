# Review

## Findings

No blocking findings in the local review pass.

## Review Notes

- The frontend deck page now imports `useDeckTimeline` only.
- The old `useDeckEvents`, `useDeckChat`, and `useDeckActivity` hook files were removed.
- ACP runtime events are preserved as ACP/system events (`runtime_event`) instead of being translated through Mosoo Driver vocabulary.
- The old `/driver-event` route remains as compatibility, but the sandbox adapter posts to `/runtime-event`.
- Legacy `message`, `activity`, `context`, and `turn` SSE broadcasts remain server-side for rollback and non-App callers.
- The container runtime install now fails explicitly after repeated npm failures and verifies both runtime binaries during image build.

## Residual Risk

- `api.chatStream` still exists as a legacy fallback, but the current App path does not use it while `useStreamArch` is `true`.
- The timeline endpoint is still synthesized from existing message/activity rows rather than backed by a dedicated monotonic table.
- Production smoke is still required to verify Cloudflare container image build and ACP runtime behavior.
- Current deployment is blocked on this arm64 host because Wrangler builds a linux/amd64 container and npm install under qemu repeatedly hits `ECONNRESET`.
