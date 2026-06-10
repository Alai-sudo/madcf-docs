# Test Summary

## Result

Total checks: 7
Passed: 7
Failed: 0
Skipped: 0

## Commands

- `python3` YAML parse of `.github/workflows/deploy.yml`
- `bash -n scripts/deploy.sh && bash -n scripts/migrate-remote.sh`
- `git diff --check`
- Workflow deploy-local config heredoc simulation
- `npm run typecheck --workspaces --if-present`
- `npm test --workspaces --if-present`
- `npm run build --workspaces --if-present`

## Notes

- The new deploy path is manual GitHub Actions only.
- The workflow requires `CLOUDFLARE_API_TOKEN` and `PP_D1_DATABASE_ID`.
- Talent sync additionally requires `BOOTSTRAP_TOKEN`.
- The local run did not execute Cloudflare deploy.
- Vite still reports existing large chunk warnings.
