---
title: Local-Only Branch Risk Audit
date: 2026-06-10
---

# Local-Only Branch Risk Audit

This report filters the full branch inventory down to local state that is not safely represented by an existing remote branch. Baseline: `origin/dev` at `53f3f2e`.

## Summary

- Dirty worktrees: 7
- Local risk branches: 30
- Local branches already contained in `origin/dev`: 2

## Local Risk Branches

| Risk | Branch | Ahead upstream | Ahead dev | Behind dev | Upstream | Worktree | Subject |
|---|---|---:|---:|---:|---|---|---|
| dirty | `ab/standard-4-cpu` | 0 | 1 | 78 | `origin/ab/standard-4-cpu` | `pitchpilot-cf-ab-cpu` | perf(sandbox): bump container to standard-4 (4 vCPU + 12 GiB) for v2 PPTX builds |
| dirty | `chore/local-branch-audit` | 0 | 0 | 0 | `origin/dev` | `pitchpilot-cf-branch-audit` | ci: deploy integration branch from dev |
| dirty | `docs/collaboration-sop` | 0 | 42 | 76 | `origin/main` | `pitchpilot-cf-collab-sop` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| dirty | `feat/dom-pptx-skills` | 0 | 60 | 76 | `origin/feat/dom-pptx-skills` | `pitchpilot-cf-dom-pptx-skills` | docs: record export progress deploy verification |
| dirty | `fix/restore-oasis-container` | 0 | 0 | 5 | `origin/fix/preview-load-speed` | `pitchpilot-cf-preview-perf` | test: record visual pptx deployment smoke |
| dirty | `main` | 0 | 42 | 76 | `origin/main` | `pitchpilot-cf` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| dirty | `refactor/revert-to-claude-code-sandbox` | 0 | 0 | 19 | `origin/refactor/revert-to-claude-code-sandbox` | `pitchpilot-cf-revert-sandbox` | test: record agent runtime production smoke |
| ahead-upstream | `feat/deck-create-perf` | 2 | 1 | 87 | `origin/feat/deck-create-perf` |  | feat(perf): skip 2 redundant roundtrips in deck-create-to-enter |
| ahead-upstream | `feat/parity-knowledge-panels-frontend` | 15 | 1 | 190 | `origin/feat/parity-knowledge-panels-frontend` | `pitchpilot-cf-knowledge-fe` | Merge remote-tracking branch 'origin/main' into feat/parity-knowledge-panels-frontend |
| ahead-upstream | `fix/panel-tab-stickiness` | 1 | 44 | 76 | `origin/fix/panel-tab-stickiness` | `pitchpilot-cf-panel-logic` | docs: review notes for panel-tab-stickiness |
| ahead-upstream | `spike/svg-to-pptx` | 1 | 43 | 76 | `origin/main` | `pitchpilot-cf-pptx-spike` | spike(pptx): SVG->editable PPTX in the Worker (pure JS, no python/sandbox) |
| no-upstream | `backup/revert-sandbox-before-dom-pptx` |  | 0 | 58 | _none_ |  | docs(inventory): snapshot 2026-06-05 past-week cherry-picks (#139-#153) |
| no-upstream | `feat/author-svg-worker-native` |  | 52 | 76 | _none_ | `pitchpilot-cf-author-svg` | fix(web): workspace preview thumbnails — use /versions, render via deck-group |
| no-upstream | `feat/svg-to-pptx-p1` |  | 47 | 76 | _none_ | `pitchpilot-cf-svgpptx-p1` | feat(svg-pptx): P1.5 — wire /export.pptx to render SVG decks via the converter |
| no-upstream | `feat/unified-deck-ir` |  | 1 | 58 | _none_ | `pitchpilot-cf-unified-ir` | docs(design): unified deck IR — one path, deterministic HTML+PPTX, round-trippable import (DRAFT) |
| no-upstream | `fix/deck-output-assets` |  | 39 | 76 | _none_ | `pitchpilot-cf-deck-assets` | fix(talents): load 8 image talents (toml->json) + vendor Dify logo SVGs |
| upstream-gone | `ci/auto-deploy-main` |  | 43 | 76 | `origin/ci/auto-deploy-main` (gone) |  | ci: deploy automatically from main |
| upstream-gone | `dev/production-sync-2026-06-09` |  | 106 | 76 | `origin/dev/production-sync-2026-06-09` (gone) | `pitchpilot-cf-dev-sync` | chore: support toml talent bootstrap |
| upstream-gone | `docs/inventory-update` |  | 1 | 119 | `origin/docs/inventory-update` (gone) | `pitchpilot-cf-deploy` | docs: update alignment inventory with PR #82-#86 |
| upstream-gone | `feat/activity-pagination` |  | 2 | 247 | `origin/feat/activity-pagination` (gone) | `pitchpilot-cf-activity` | docs: activity pagination test summary |
| upstream-gone | `feat/admin-gating-deck-members-ui` |  | 3 | 246 | `origin/feat/admin-gating-deck-members-ui` (gone) | `pitchpilot-cf-final-gaps` | docs: admin gating + deck-members API + hotfix test summary |
| upstream-gone | `feat/admin-routes-2` |  | 2 | 248 | `origin/feat/admin-routes-2` (gone) | `pitchpilot-cf-admin-routes` | docs: admin routes test summary |
| upstream-gone | `feat/context-files-in-prompt` |  | 2 | 244 | `origin/feat/context-files-in-prompt` (gone) | `pitchpilot-cf-context-prompt` | docs: memory-in-prompt test summary |
| upstream-gone | `feat/deck-members` |  | 2 | 249 | `origin/feat/deck-members` (gone) | `pitchpilot-cf-deck-members` | docs: deck-members test summary |
| upstream-gone | `feat/import-into-context` |  | 2 | 243 | `origin/feat/import-into-context` (gone) | `pitchpilot-cf-import-context` | feat(talents): PP-convention wrappers for source converters |
| upstream-gone | `feat/members-toolbar` |  | 3 | 245 | `origin/feat/members-toolbar` (gone) | `pitchpilot-cf-members-ui` | docs: members toolbar test summary |
| upstream-gone | `feat/ppt-master-talents` |  | 5 | 251 | `origin/feat/ppt-master-talents` (gone) |  | docs: ppt-master + brand-design test summary |
| upstream-gone | `feat/tulpa-bind-ppt-master` |  | 3 | 250 | `origin/feat/tulpa-bind-ppt-master` (gone) | `pitchpilot-cf-tulpa-binding` | docs: tulpa-binding test summary |
| upstream-gone | `feat/tulpa-talents-sandbox` |  | 10 | 252 | `origin/feat/tulpa-talents-sandbox` (gone) |  | docs: refresh test summary with admin wsId fix + final worker version |
| upstream-gone | `fix/bootstrap-skip-non-manifest` |  | 44 | 76 | `origin/fix/bootstrap-skip-non-manifest` (gone) |  | fix: skip non-manifest talent directories during bootstrap |


## Dirty Status Details

### main

Worktree: `/home/ubuntu/pitchpilot-cf`

```text
?? artifacts/
```

### ab/standard-4-cpu

Worktree: `/home/ubuntu/pitchpilot-cf-ab-cpu`

```text
?? apps/api/node_modules
?? apps/web/node_modules
?? node_modules
```

### chore/local-branch-audit

Worktree: `/home/ubuntu/pitchpilot-cf-branch-audit`

```text
?? docs/iterations/2026-06-10-local-branch-audit/
```

### docs/collaboration-sop

Worktree: `/home/ubuntu/pitchpilot-cf-collab-sop`

```text
?? docs/iterations/2026-06-08-collaboration-sop/
```

### feat/dom-pptx-skills

Worktree: `/home/ubuntu/pitchpilot-cf-dom-pptx-skills`

```text
?? docs/iterations/2026-06-08-dual-runner-modes/
```

### fix/restore-oasis-container

Worktree: `/home/ubuntu/pitchpilot-cf-preview-perf`

```text
 M apps/api/src/agent/composePrompt.ts
 M apps/api/src/router.ts
 M apps/api/src/routes/admin.ts
 M containers/oasis/Dockerfile
```

### refactor/revert-to-claude-code-sandbox

Worktree: `/home/ubuntu/pitchpilot-cf-revert-sandbox`

```text
?? docs/iterations/2026-06-04-revert-to-sandbox/
?? docs/iterations/2026-06-08-responsive-html-slide-contract/
```
