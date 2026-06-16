# Test Summary

## Commands

- `node --check containers/oasis/pp-cli/bin/pp-agent-bridge.mjs && node --check containers/oasis/pp-cli/bin/pp-run-agent.mjs`
- `npm run typecheck --workspace=@pp/api`
- `npm run typecheck --workspace=@pp/web`
- `npx tsx --test apps/api/src/agent/runtimeCache.test.ts apps/api/src/durable/bridgeEvents.test.ts`

## Results

- Total tests: 12
- Passed: 12
- Failed: 0
- Skipped: 0

## Notes

- Bridge JavaScript syntax checks passed.
- API TypeScript typecheck passed.
- Web TypeScript typecheck passed.
- Runtime cache and bridge event normalization tests passed.
- Browser and deployed sandbox smoke tests were not run in this iteration.
