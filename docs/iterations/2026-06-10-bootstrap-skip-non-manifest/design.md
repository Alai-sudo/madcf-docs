# Bootstrap Skip Non-Manifest Talent Directories

## Goal

Make production deploy green after the Worker deploy succeeds.

## Problem

`scripts/bootstrap-talents.mjs` assumes every directory under
`containers/oasis-talents/` contains `manifest.json`. Current `main` includes
some newer talent directories that use `talent.toml` and do not have
`manifest.json`. The deploy run successfully deployed the Worker and Sandbox
container, then failed during talent sync because these directories were counted
as hard failures.

## Approach

- Treat missing `manifest.json` as a skipped directory.
- Keep other talent loading errors as hard failures.
- Preserve the existing manifest-based sync behavior for all current production
  talents.
- Fix local bootstrap-token fallback for this ESM script by using
  `readFileSync` instead of `require`.

## Test Plan

- Run `node --check scripts/bootstrap-talents.mjs`.
- Run `node scripts/bootstrap-talents.mjs --dry-run` and confirm missing
  manifest directories are skipped.
- Confirm dry-run works through the local token fallback.
