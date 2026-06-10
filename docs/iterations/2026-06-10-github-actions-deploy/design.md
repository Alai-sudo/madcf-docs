# GitHub Actions Deploy

## Goal

Move production deployment off the current ARM host so the Cloudflare Sandbox
container image is built on a native `linux/amd64` runner instead of via QEMU.

## Approach

- Add a GitHub Actions workflow that deploys automatically when `main` changes.
- Keep `workflow_dispatch` as an operator fallback for manual redeploys.
- Run on `ubuntu-latest`, which provides an amd64 Linux runner.
- Keep `wrangler.toml` free of account-specific IDs.
- Generate `wrangler.deploy.local.toml` from GitHub secrets during the job.
- Reuse the existing deployment scripts:
  - `scripts/migrate-remote.sh` for D1 migrations.
  - `scripts/deploy.sh` for Wrangler deploy.
  - `scripts/bootstrap-talents.mjs` for system talent sync.
- Run D1 migrations and system talent sync by default on `main` deploys.
- Let manual redeploys choose whether to run migrations and talent sync.

## Required GitHub Configuration

Repository secrets:

- `CLOUDFLARE_API_TOKEN`
- `PP_D1_DATABASE_ID`
- `BOOTSTRAP_TOKEN` if talent sync is enabled

Repository variables:

- `PP_BASE` optional. Defaults to
  `https://pitchpilot-api.langgenius-opc.workers.dev` when unset.

## Scope

In scope:

- Add `.github/workflows/deploy.yml`.
- Trigger deployment on `push` to `main` and on manual `workflow_dispatch`.
- Document this deployment path.

Out of scope:

- Changing Worker runtime behavior.
- Changing Cloudflare container image contents.
- Moving to a Cloudflare-native remote image builder, because the current
  Wrangler container path still builds from the repository Dockerfile.

## Test Plan

- Validate the workflow YAML is syntactically loadable.
- Verify push-trigger and manual-trigger condition expressions.
- Run local typecheck and build.
- Confirm no account-specific secrets are committed.
