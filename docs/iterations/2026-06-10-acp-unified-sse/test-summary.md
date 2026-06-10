# Test Summary

## Result

- Total checks: 10
- Passed: 8
- Failed: 0
- Blocked: 1
- Interrupted: 1
- Skipped: 0

## Passed

- Dependency install with `npm ci`.
- ACP adapter JavaScript syntax check.
- API and web TypeScript checks.
- Workspace test command.
- API and web production build.
- `git diff --check`.
- Source inspection for unified App-level SSE usage.
- Post-Dockerfile-fix `git diff --check` and TypeScript checks.

## Interrupted

- First deployment attempt was interrupted after the container npm install layer hit `ECONNRESET` under qemu. Investigation found and fixed a Dockerfile retry-loop bug that could otherwise hide repeated npm failures.

## Blocked

- Second deployment attempt confirmed the same qemu npm failure pattern on `@agentclientprotocol/claude-agent-acp`. The host can reach the npm tarball directly, but the amd64 container build under qemu fails after a long CPU-bound install. Deployment should continue from an amd64 builder or a prebuilt amd64 container image path.

## Notes

- npm audit findings pre-exist this patch: 8 moderate, 1 critical.
- Vite large chunk warnings pre-exist this patch.
- Browser and production deployment smoke results will be added after deploy.
