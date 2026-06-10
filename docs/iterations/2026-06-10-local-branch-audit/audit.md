---
title: Local Branch Audit Report
date: 2026-06-10
---

# Local Branch Audit Report

Baseline: `origin/dev` at `53f3f2e`. Production baseline: `origin/main` at `994caec`.

## Summary

| Classification | Count |
|---|---:|
| already-in-dev | 32 |
| candidate-for-dev | 110 |
| dirty-worktree | 7 |
| local-or-remote-gone | 18 |

## Dirty Worktrees

| Branch | Ahead dev | Behind dev | Upstream | Worktree | Subject |
|---|---:|---:|---|---|---|
| `ab/standard-4-cpu` | 1 | 78 | `origin/ab/standard-4-cpu` | `pitchpilot-cf-ab-cpu` | perf(sandbox): bump container to standard-4 (4 vCPU + 12 GiB) for v2 PPTX builds |
| `chore/local-branch-audit` | 0 | 0 | `origin/dev` | `pitchpilot-cf-branch-audit` | ci: deploy integration branch from dev |
| `docs/collaboration-sop` | 42 | 76 | `origin/main` | `pitchpilot-cf-collab-sop` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| `feat/dom-pptx-skills` | 60 | 76 | `origin/feat/dom-pptx-skills` | `pitchpilot-cf-dom-pptx-skills` | docs: record export progress deploy verification |
| `fix/restore-oasis-container` | 0 | 5 | `origin/fix/preview-load-speed` | `pitchpilot-cf-preview-perf` | test: record visual pptx deployment smoke |
| `main` | 42 | 76 | `origin/main` | `pitchpilot-cf` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| `refactor/revert-to-claude-code-sandbox` | 0 | 19 | `origin/refactor/revert-to-claude-code-sandbox` | `pitchpilot-cf-revert-sandbox` | test: record agent runtime production smoke |


## Candidate Branches With Commits Not In dev

These branches still have commits not contained in `origin/dev` and still track an existing upstream. They should be reviewed before migrating into `dev`.

| Branch | Ahead dev | Behind dev | Upstream | Worktree | Subject |
|---|---:|---:|---|---|---|
| `chore/dev-standard-sandbox-image` | 34 | 76 | `origin/chore/dev-standard-sandbox-image` |  | chore(dev): use stock @cloudflare/sandbox image, drop per-deploy docker build |
| `chore/talents-sync` | 1 | 131 | `origin/chore/talents-sync` |  | chore(talents): rename pp-confluence/main.md → SKILL.md for naming consistency |
| `docs/inventory-2` | 1 | 116 | `origin/docs/inventory-2` |  | docs: PR #88/#89 + #73/#99/#100/#102/#103/#124 audits |
| `docs/inventory-tier2` | 1 | 111 | `origin/docs/inventory-tier2` |  | docs: tier 2 closed — pp-methodology + specialists + dispatch templates (PRs #91-#94) |
| `docs/inventory-tier3` | 1 | 106 | `origin/docs/inventory-tier3` |  | docs: tier 3 closed — onboarding-zh + admin telemetry + MCP PAT + admin users email |
| `docs/inventory-tier4` | 1 | 103 | `origin/docs/inventory-tier4` |  | docs: tier 4 closed — pptx-v2 SVG assembler + builder talent |
| `docs/onboarding-zh` | 1 | 110 | `origin/docs/onboarding-zh` |  | docs: onboarding-zh.md — Chinese new-user guide (aligns PP main #133) |
| `docs/pp-main-inventory` | 1 | 123 | `origin/docs/pp-main-inventory` |  | docs: PP main alignment inventory — running ledger |
| `feat/admin-anthropic-key` | 1 | 81 | `origin/feat/admin-anthropic-key` |  | feat(admin): global Anthropic API key with per-workspace override |
| `feat/admin-email-stats` | 1 | 109 | `origin/feat/admin-email-stats` |  | feat(admin): Users email column + dynamic phase breakdown (aligns PP main #148) |
| `feat/admin-sandbox-inspector` | 2 | 76 | `origin/feat/admin-sandbox-inspector` |  | feat(admin): Sandbox Inspector — diagnose agent state per deck |
| `feat/admin-settings` | 1 | 98 | `origin/feat/admin-settings` |  | feat(admin): Configuration + Connections tabs with OAuth + skill keys + feature flags |
| `feat/admin-telemetry` | 2 | 108 | `origin/feat/admin-telemetry` |  | fix(telemetry): await recordEvent so CF Worker doesn't kill the D1 INSERT |
| `feat/agent-loop-poc` | 26 | 76 | `origin/main` |  | refactor(agent): M4b batch5 — remove claude-code from the image |
| `feat/anthropic-key-panel` | 1 | 88 | `origin/feat/anthropic-key-panel` |  | feat(settings): add Workspace AI panel for per-workspace Anthropic key |
| `feat/artifact-grouper-signals` | 1 | 128 | `origin/feat/artifact-grouper-signals` |  | feat(generic-viewer): backend signals.artifacts[] + artifact-grouper (Stage 2 of #87 alignment) |
| `feat/arx-governance-federation` | 50 | 76 | `origin/feat/arx-governance-federation` | `pitchpilot-cf-arx-federation` | docs: record diff stats vs the M1 net-negative criterion + final status |
| `feat/assemble-svg-deck` | 1 | 106 | `origin/feat/assemble-svg-deck` |  | feat(assembler): SVG-mode deck preview pipeline (aligns PP main 752b3c5) |
| `feat/chat-scroll-batch1` | 6 | 122 | `origin/feat/chat-scroll-batch1` |  | feat(persona): Tier 2 — language-match + pp-cli mandate + audience-not-on-slide (aligns PP main #117/#126) |
| `feat/conceptcloud-race-fix` | 1 | 84 | `origin/feat/conceptcloud-race-fix` |  | fix(perf): ConceptCloud race — wait for contextHydratedDeckId before reading prefetched |
| `feat/confluence-panel-port` | 1 | 89 | `origin/feat/confluence-panel-port` |  | feat(confluence): port PP main zen redesign verbatim |
| `feat/conversation-checkpoint` | 1 | 77 | `origin/feat/conversation-checkpoint` |  | feat(persistence): conversation checkpoint — survive sandbox idle eviction |
| `feat/deck-create-perf` | 1 | 87 | `origin/feat/deck-create-perf` |  | feat(perf): skip 2 redundant roundtrips in deck-create-to-enter |
| `feat/deckdo-prewarm` | 1 | 83 | `origin/feat/deckdo-prewarm` |  | feat(perf): pre-warm DeckDO inside POST createDeck |
| `feat/dedupe-deck-fetches` | 1 | 86 | `origin/feat/dedupe-deck-fetches` |  | feat(perf): dedupe ctx/arts fetch + skip route-effect getDeck on prefetched path |
| `feat/dedupe-deck-fetches-pt2` | 1 | 85 | `origin/feat/dedupe-deck-fetches-pt2` |  | feat(perf): dedupe listDeckMembers internal getDeck + ConceptCloud listContext |
| `feat/dispatch-templates` | 1 | 112 | `origin/feat/dispatch-templates` |  | feat(methodology): dispatch templates + persona hint (Stage D of #90) |
| `feat/edit-comment-cards` | 1 | 117 | `origin/feat/edit-comment-cards` |  | feat(chat): collapse [user-edit] and [user-comment] into cards (aligns PP main #104) |
| `feat/embedded-slide-nav` | 2 | 118 | `origin/feat/embedded-slide-nav` |  | fix(chat): import useLayoutEffect — runtime crash on deck open |
| `feat/force-sandbox-and-skill-mount` | 4 | 142 | `origin/feat/force-sandbox-and-skill-mount` |  | feat(engine): force-sandbox — drop in-Worker anthropic path |
| `feat/generic-viewer-frontend` | 3 | 127 | `origin/feat/generic-viewer-frontend` |  | fix(client): adaptDeck — forward signals.artifacts + active_artifact_id |
| `feat/inspect-anywhere` | 4 | 76 | `origin/feat/inspect-anywhere` |  | feat(deck): AdminRail on left of deck view — Inspector always reachable |
| `feat/inspector-drawer` | 3 | 76 | `origin/feat/inspector-drawer` |  | feat(deck): admin-only Inspector drawer on the preview toolbar |
| `feat/inspector-file-browser` | 5 | 76 | `origin/feat/inspector-file-browser` |  | feat(inspector): Phase 1 file browser + open to deck owners |
| `feat/inspector-file-edit` | 6 | 76 | `origin/feat/inspector-file-edit` |  | feat(inspector): Phase 2 — write text files with ETag concurrency |
| `feat/knowledge-panel` | 1 | 97 | `origin/feat/knowledge-panel` |  | feat(settings): Knowledge sources panel — Confluence + Droploft connect/disconnect |
| `feat/lazy-sandbox-boot` | 28 | 76 | `origin/feat/lazy-sandbox-boot` |  | fix(agent): address review — turn-scoped boot guard + retry on failure |
| `feat/mcp-pat` | 1 | 107 | `origin/feat/mcp-pat` |  | feat(auth): MCP Personal Access Tokens + Settings UI (aligns PP main #135) |
| `feat/memory-proposals` | 43 | 76 | `origin/feat/memory-proposals` |  | docs(memory-proposals): post-review re-verification (decide-first accept + 409) |
| `feat/my-memory-panel` | 1 | 92 | `origin/feat/my-memory-panel` |  | feat(settings+memory): user-scope memory routes + My Memory panel (PP main /dev) |
| `feat/parity-context-files` | 1 | 257 | `origin/feat/parity-context-files` | `pitchpilot-cf-context` | feat(api,web): context files (memory/context/skills) with R2 binary upload |
| `feat/parity-folders-phase-mode` | 1 | 258 | `origin/feat/parity-folders-phase-mode` | `pitchpilot-cf-folders` | feat(api,web): folders + deck.phase + deck.mode/theme + folder_id |
| `feat/parity-foundation` | 3 | 259 | `origin/feat/parity-foundation` | `pitchpilot-cf-parity` | fix(web): adapt SSE hooks + send body to CF event/contract shape |
| `feat/parity-knowledge-panels-frontend` | 1 | 190 | `origin/feat/parity-knowledge-panels-frontend` | `pitchpilot-cf-knowledge-fe` | Merge remote-tracking branch 'origin/main' into feat/parity-knowledge-panels-frontend |
| `feat/parity-multi-tulpa-fanout` | 1 | 180 | `origin/feat/parity-multi-tulpa-fanout` |  | fix(slice-11): scope sandbox fan-out to primary tulpa + echo fan-out |
| `feat/parity-profiles-share` | 2 | 256 | `origin/feat/parity-profiles-share` | `pitchpilot-cf-profiles` | fix(shares): await view_count bump so subsequent reads see it |
| `feat/parity-task-status-cleanup` | 1 | 254 | `origin/feat/parity-task-status-cleanup` | `pitchpilot-cf-task-status` | feat(web): task_status SSE translation + cut confluence + arx admin tabs |
| `feat/persona-10-traits` | 1 | 121 | `origin/feat/persona-10-traits` |  | feat(persona): 10 traits of a great pitch deck (aligns PP main #123) |
| `feat/persona-pp-main-align` | 1 | 132 | `origin/feat/persona-pp-main-align` |  | feat(persona): align pp-writer with PP main 4-phase workflow + Scene awareness |
| `feat/port-pp-talents` | 1 | 233 | `origin/feat/port-pp-talents` |  | feat(talents): port 10 PP talents (pitch-gather, narrative, deck-*, etc.) |
| `feat/pp-cli-scope-flag` | 1 | 92 | `origin/feat/pp-cli-scope-flag` |  | feat(pp-cli): pp save memory --scope flag (aligns PP main #140 + #145) |
| `feat/pp-main-parity` | 40 | 76 | `origin/feat/pp-main-parity` |  | docs(parity): browser verification results for speaker-notes pane |
| `feat/pp-methodology-talent` | 1 | 116 | `origin/feat/pp-methodology-talent` |  | feat(methodology): vendor pp-methodology talent + reference set (Stage A of #90) |
| `feat/pp-writer-persona-v2` | 1 | 113 | `origin/feat/pp-writer-persona-v2` |  | feat(pp-writer): mission-first persona + build doctrine + failure modes (Stage C of #90) |
| `feat/pptx-fix-viewer-quality` | 44 | 76 | `origin/feat/pptx-fix-viewer-quality` |  | fix(review): drop redundant sha256sum in binary self-test; add review notes |
| `feat/pptx-preview-port` | 6 | 210 | `origin/feat/pptx-preview-port` | `pitchpilot-cf-pptx-preview` | fix(pptx): export route doesn't require a presentations row for R2 path |
| `feat/pptx-v2-default` | 1 | 79 | `origin/feat/pptx-v2-default` |  | feat(agent): default to pp-deck-builder-pptx-v2 (SVG/ppt-master) for new decks |
| `feat/pptx-v2-talent` | 1 | 104 | `origin/feat/pptx-v2-talent` |  | feat(pptx-v2): vendor pp-deck-builder-pptx-v2 talent + bind to pp-writer (aligns PP main #1cb287c) |
| `feat/sandbox-faster-cold-start` | 1 | 80 | `origin/feat/sandbox-faster-cold-start` |  | perf(sandbox): bump instance_type to standard + drop unused engine binaries |
| `feat/scoped-memory` | 1 | 95 | `origin/feat/scoped-memory` |  | feat(memory): four-scope agent memory + admin Memory tab (aligns PP main #141) |
| `feat/slide-safe-area-dual-nav` | 41 | 76 | `origin/feat/slide-safe-area-dual-nav` |  | docs(quality): verification — dual-nav live, safe-area fix confirmed (structural) |
| `feat/specialist-tulpas-registry` | 1 | 114 | `origin/feat/specialist-tulpas-registry` |  | feat(tulpas): register 5 specialist tulpas (Stage B of #90) |
| `feat/sprint-1-admin` | 2 | 260 | `origin/feat/sprint-1-admin` |  | docs: README + Phase D test artifacts (10/10 admin checks pass) |
| `feat/sprint-1-auth-workspaces-decks` | 6 | 264 | `origin/feat/sprint-1-auth-workspaces-decks` | `pitchpilot-cf-sprint-1-auth` | fix(crypto): drop PBKDF2 to 100k for CF Workers cap; deploy + smoke-test pass |
| `feat/sprint-1-deckdo-chat` | 4 | 263 | `origin/feat/sprint-1-deckdo-chat` | `pitchpilot-cf-sprint-1-deckdo` | docs: Phase B.1 test artifacts — 6/6 smoke green on prod |
| `feat/sprint-1-frontend` | 3 | 261 | `origin/feat/sprint-1-frontend` | `pitchpilot-cf-web` | docs: Phase C design + test artifacts — 10/10 browser checks pass |
| `feat/sprint-1-real-agent` | 2 | 262 | `origin/feat/sprint-1-real-agent` | `pitchpilot-cf-sprint-1-real-agent` | feat(agent): real Anthropic streaming + echo fallback |
| `feat/stats-chip` | 1 | 94 | `origin/feat/stats-chip` |  | feat(nav): active-time DeckTimeChip + DeckStatsPopover (aligns PP main StatsChip) |
| `feat/storyboard-preview-edit-export` | 6 | 253 | `origin/feat/storyboard-preview-edit-export` | `pitchpilot-cf-storyboard-edit` | docs: capture review findings + resolution for storyboard PR |
| `feat/storyboard-tab-md-title` | 1 | 121 | `origin/feat/storyboard-tab-md-title` |  | feat(preview): Storyboard tab renames to doc title (aligns PP main #129) |
| `feat/sync-dev-tulpas` | 1 | 76 | `origin/feat/sync-dev-tulpas` |  | feat(talents): sync 8 new design-format talents from PP main dev |
| `feat/talents-native-tools-dify-sop` | 41 | 76 | `origin/feat/talents-native-tools-dify-sop` |  | docs(quality): verification PASS — native-tool build + on-brand Dify palette |
| `feat/workspace-rail-profile` | 12 | 76 | `origin/main` |  | fix(oasis): surface ALL engine errors, not just auth |
| `fix/acp-auth-bailout` | 1 | 140 | `origin/fix/acp-auth-bailout` |  | fix(acp): don't bail on advertised authMethods — let session/new decide |
| `fix/acp-force-kill` | 1 | 139 | `origin/fix/acp-force-kill` |  | fix(acp): force-kill engine after session/prompt — escalate SIGTERM/SIGKILL |
| `fix/acp-kill-not-error` | 1 | 138 | `origin/fix/acp-kill-not-error` |  | fix(acp): don't surface SIGTERM/SIGKILL as turn error when stopReason was clean |
| `fix/acp-prompt-timeout` | 2 | 137 | `origin/fix/acp-prompt-timeout` |  | fix(acp): null stopReason — surface as cold-boot error, not 'killed by SIGTERM' |
| `fix/acp-turn-stall` | 2 | 141 | `origin/fix/acp-turn-stall` |  | fix(acp): don't bail on advertised authMethods — let session/new decide |
| `fix/admin-decks-shape` | 2 | 102 | `origin/fix/admin-decks-shape` |  | fix(admin): rewrite SystemManager for PP-CF health shape |
| `fix/build-artifact-cwd` | 28 | 76 | `origin/fix/build-artifact-cwd` |  | fix(agent): guide builds to write under the deck root |
| `fix/cold-boot-retry` | 1 | 135 | `origin/fix/cold-boot-retry` |  | fix(sandbox): retry once on cold-boot engine failure |
| `fix/cold-retry-v2` | 1 | 134 | `origin/fix/cold-retry-v2` |  | fix(sandbox): retry cold-boot twice (was once) — catches sluggish containers |
| `fix/confluence-auto-prompt` | 1 | 99 | `origin/fix/confluence-auto-prompt` |  | fix(confluence): auto-prompt connect panel once per session on unconfigured deck |
| `fix/confluence-event-listener` | 1 | 96 | `origin/fix/confluence-event-listener` |  | fix(confluence): listen for KnowledgePanel's pp:open-confluence-connect event |
| `fix/d1-sync-regressions` | 1 | 133 | `origin/fix/d1-sync-regressions` |  | fix(d1-sync): inline text memory + auto phase advance + slides_count recount |
| `fix/deck-open-signals` | 39 | 76 | `origin/fix/deck-open-signals` |  | docs(deck-open): browser verification PASS |
| `fix/deck-switch-workspace-state` | 29 | 76 | `origin/fix/deck-switch-workspace-state` |  | fix(web): reset Workspace state on deck switch |
| `fix/deck-view-remount-on-switch` | 30 | 76 | `origin/fix/deck-view-remount-on-switch` |  | fix(web): clear+reload per-deck state on back/forward navigation |
| `fix/droploft-panel-parity` | 1 | 100 | `origin/fix/droploft-panel-parity` |  | fix(droploft): port PP main panel verbatim — simpler single-connection setup |
| `fix/enable-confluence-panel` | 1 | 101 | `origin/fix/enable-confluence-panel` |  | fix(confluence): re-enable panel — clicking button silently did nothing |
| `fix/export-pptx-bug` | 1 | 125 | `origin/fix/export-pptx-bug` |  | fix(export): rewrite /export.pptx + add /export for HTML download |
| `fix/google-oauth-config` | 1 | 90 | `origin/fix/google-oauth-config` |  | fix(auth): Google OAuth — correct URL + admin Configuration takes effect |
| `fix/hide-pickmode-ui` | 2 | 131 | `origin/fix/hide-pickmode-ui` |  | fix(docker): retry npm install on transient EPIPE under QEMU buildx |
| `fix/lazyslide-hoist` | 1 | 93 | `origin/fix/lazyslide-hoist` |  | fix(dashboard): hoist LazySlide out of DeckDashboard (aligns PP main #120) |
| `fix/nav-axis-aware` | 44 | 76 | `origin/fix/nav-axis-aware` | `pitchpilot-cf-nav-axis` | docs(review): nav-axis-aware review + fix two stale comments (current->target, bottom->axis-aware) |
| `fix/panel-tab-stickiness` | 44 | 76 | `origin/fix/panel-tab-stickiness` | `pitchpilot-cf-panel-logic` | docs: review notes for panel-tab-stickiness |
| `fix/pp-writer-sandbox-prompt` | 2 | 136 | `origin/fix/pp-writer-sandbox-prompt` |  | fix(prompt): plug two more reverse-overwrite paths |
| `fix/preview-toolbar-grouping` | 32 | 76 | `origin/fix/preview-toolbar-grouping` |  | fix(preview): group toolbar into Export / More dropdowns (was overlapping) |
| `fix/preview-version-switch` | 31 | 76 | `origin/fix/preview-version-switch` |  | fix(preview): version switch follows current_version (was stuck on newest) |
| `fix/session-resume-fallback` | 1 | 131 | `origin/fix/session-resume-fallback` |  | fix(resume): inject Previous Conversation into CLAUDE.md so turn N+1 has context when --resume fails |
| `fix/sse-context-refresh` | 43 | 76 | `origin/fix/sse-context-refresh` |  | docs: test artifacts + SSE evidence for context-refresh fix |
| `fix/stuck-building-on-reopen` | 33 | 76 | `origin/fix/stuck-building-on-reopen` |  | fix(web): clear stuck 'Building' indicator on deck reopen |
| `fix/stuck-turn-recovery` | 1 | 255 | `origin/fix/stuck-turn-recovery` | `pitchpilot-cf-stuck-turn` | fix(deckdo): stuck-turn auto-recovery + /reset escape hatch + 50s timeout |
| `perf/assemble-parallel` | 1 | 125 | `origin/perf/assemble-parallel` |  | perf(preview): parallelize R2 fetches in assembleDeck (~5x speedup) |
| `refactor/agent-turn-memory` | 38 | 76 | `origin/refactor/agent-turn-memory` | `pitchpilot-cf-agent-memory` | fix(talents): address review — manifest desc, yaml WebSearch refs, dead export |
| `refactor/cleanup-buildmodepicker` | 1 | 126 | `origin/refactor/cleanup-buildmodepicker` |  | refactor(generic-viewer): retire BuildModePicker + mode_required gate (Stage 4 of #87 alignment) |
| `refactor/worker-side-artifact-sync` | 41 | 76 | `origin/refactor/worker-side-artifact-sync` |  | docs(boot): browser verification PASS + test report/summary |
| `revert/deckdo-prewarm` | 1 | 82 | `origin/revert/deckdo-prewarm` |  | revert: 'feat(perf): pre-warm DeckDO inside POST createDeck' (#123) |
| `spike/svg-to-pptx` | 43 | 76 | `origin/main` | `pitchpilot-cf-pptx-spike` | spike(pptx): SVG->editable PPTX in the Worker (pure JS, no python/sandbox) |
| `v2-dev` | 5 | 102 | `origin/v2-dev` | `pitchpilot-cf-v2-dev` | docs: add attention-first focus prototype |


## Local Or Remote-Gone Branches

These branches either have no upstream or their tracked remote branch is gone. Keep only if the branch contains useful work.

| Branch | Ahead dev | Behind dev | Upstream | Worktree | Subject |
|---|---:|---:|---|---|---|
| `ci/auto-deploy-main` | 43 | 76 | `origin/ci/auto-deploy-main` (gone) |  | ci: deploy automatically from main |
| `dev/production-sync-2026-06-09` | 106 | 76 | `origin/dev/production-sync-2026-06-09` (gone) | `pitchpilot-cf-dev-sync` | chore: support toml talent bootstrap |
| `docs/inventory-update` | 1 | 119 | `origin/docs/inventory-update` (gone) | `pitchpilot-cf-deploy` | docs: update alignment inventory with PR #82-#86 |
| `feat/activity-pagination` | 2 | 247 | `origin/feat/activity-pagination` (gone) | `pitchpilot-cf-activity` | docs: activity pagination test summary |
| `feat/admin-gating-deck-members-ui` | 3 | 246 | `origin/feat/admin-gating-deck-members-ui` (gone) | `pitchpilot-cf-final-gaps` | docs: admin gating + deck-members API + hotfix test summary |
| `feat/admin-routes-2` | 2 | 248 | `origin/feat/admin-routes-2` (gone) | `pitchpilot-cf-admin-routes` | docs: admin routes test summary |
| `feat/author-svg-worker-native` | 52 | 76 | _none_ | `pitchpilot-cf-author-svg` | fix(web): workspace preview thumbnails — use /versions, render via deck-group |
| `feat/context-files-in-prompt` | 2 | 244 | `origin/feat/context-files-in-prompt` (gone) | `pitchpilot-cf-context-prompt` | docs: memory-in-prompt test summary |
| `feat/deck-members` | 2 | 249 | `origin/feat/deck-members` (gone) | `pitchpilot-cf-deck-members` | docs: deck-members test summary |
| `feat/import-into-context` | 2 | 243 | `origin/feat/import-into-context` (gone) | `pitchpilot-cf-import-context` | feat(talents): PP-convention wrappers for source converters |
| `feat/members-toolbar` | 3 | 245 | `origin/feat/members-toolbar` (gone) | `pitchpilot-cf-members-ui` | docs: members toolbar test summary |
| `feat/ppt-master-talents` | 5 | 251 | `origin/feat/ppt-master-talents` (gone) |  | docs: ppt-master + brand-design test summary |
| `feat/svg-to-pptx-p1` | 47 | 76 | _none_ | `pitchpilot-cf-svgpptx-p1` | feat(svg-pptx): P1.5 — wire /export.pptx to render SVG decks via the converter |
| `feat/tulpa-bind-ppt-master` | 3 | 250 | `origin/feat/tulpa-bind-ppt-master` (gone) | `pitchpilot-cf-tulpa-binding` | docs: tulpa-binding test summary |
| `feat/tulpa-talents-sandbox` | 10 | 252 | `origin/feat/tulpa-talents-sandbox` (gone) |  | docs: refresh test summary with admin wsId fix + final worker version |
| `feat/unified-deck-ir` | 1 | 58 | _none_ | `pitchpilot-cf-unified-ir` | docs(design): unified deck IR — one path, deterministic HTML+PPTX, round-trippable import (DRAFT) |
| `fix/bootstrap-skip-non-manifest` | 44 | 76 | `origin/fix/bootstrap-skip-non-manifest` (gone) |  | fix: skip non-manifest talent directories during bootstrap |
| `fix/deck-output-assets` | 39 | 76 | _none_ | `pitchpilot-cf-deck-assets` | fix(talents): load 8 image talents (toml->json) + vendor Dify logo SVGs |


## All Non-Integrated Branches

| Branch | Ahead dev | Behind dev | Upstream | Worktree | Subject |
|---|---:|---:|---|---|---|
| `ab/standard-4-cpu` | 1 | 78 | `origin/ab/standard-4-cpu` | `pitchpilot-cf-ab-cpu` | perf(sandbox): bump container to standard-4 (4 vCPU + 12 GiB) for v2 PPTX builds |
| `chore/local-branch-audit` | 0 | 0 | `origin/dev` | `pitchpilot-cf-branch-audit` | ci: deploy integration branch from dev |
| `docs/collaboration-sop` | 42 | 76 | `origin/main` | `pitchpilot-cf-collab-sop` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| `feat/dom-pptx-skills` | 60 | 76 | `origin/feat/dom-pptx-skills` | `pitchpilot-cf-dom-pptx-skills` | docs: record export progress deploy verification |
| `fix/restore-oasis-container` | 0 | 5 | `origin/fix/preview-load-speed` | `pitchpilot-cf-preview-perf` | test: record visual pptx deployment smoke |
| `main` | 42 | 76 | `origin/main` | `pitchpilot-cf` | fix(sse): route agent context_updated to the context channel (panel auto-refresh) (#153) |
| `refactor/revert-to-claude-code-sandbox` | 0 | 19 | `origin/refactor/revert-to-claude-code-sandbox` | `pitchpilot-cf-revert-sandbox` | test: record agent runtime production smoke |
| `ci/auto-deploy-main` | 43 | 76 | `origin/ci/auto-deploy-main` (gone) |  | ci: deploy automatically from main |
| `dev/production-sync-2026-06-09` | 106 | 76 | `origin/dev/production-sync-2026-06-09` (gone) | `pitchpilot-cf-dev-sync` | chore: support toml talent bootstrap |
| `docs/inventory-update` | 1 | 119 | `origin/docs/inventory-update` (gone) | `pitchpilot-cf-deploy` | docs: update alignment inventory with PR #82-#86 |
| `feat/activity-pagination` | 2 | 247 | `origin/feat/activity-pagination` (gone) | `pitchpilot-cf-activity` | docs: activity pagination test summary |
| `feat/admin-gating-deck-members-ui` | 3 | 246 | `origin/feat/admin-gating-deck-members-ui` (gone) | `pitchpilot-cf-final-gaps` | docs: admin gating + deck-members API + hotfix test summary |
| `feat/admin-routes-2` | 2 | 248 | `origin/feat/admin-routes-2` (gone) | `pitchpilot-cf-admin-routes` | docs: admin routes test summary |
| `feat/author-svg-worker-native` | 52 | 76 | _none_ | `pitchpilot-cf-author-svg` | fix(web): workspace preview thumbnails — use /versions, render via deck-group |
| `feat/context-files-in-prompt` | 2 | 244 | `origin/feat/context-files-in-prompt` (gone) | `pitchpilot-cf-context-prompt` | docs: memory-in-prompt test summary |
| `feat/deck-members` | 2 | 249 | `origin/feat/deck-members` (gone) | `pitchpilot-cf-deck-members` | docs: deck-members test summary |
| `feat/import-into-context` | 2 | 243 | `origin/feat/import-into-context` (gone) | `pitchpilot-cf-import-context` | feat(talents): PP-convention wrappers for source converters |
| `feat/members-toolbar` | 3 | 245 | `origin/feat/members-toolbar` (gone) | `pitchpilot-cf-members-ui` | docs: members toolbar test summary |
| `feat/ppt-master-talents` | 5 | 251 | `origin/feat/ppt-master-talents` (gone) |  | docs: ppt-master + brand-design test summary |
| `feat/svg-to-pptx-p1` | 47 | 76 | _none_ | `pitchpilot-cf-svgpptx-p1` | feat(svg-pptx): P1.5 — wire /export.pptx to render SVG decks via the converter |
| `feat/tulpa-bind-ppt-master` | 3 | 250 | `origin/feat/tulpa-bind-ppt-master` (gone) | `pitchpilot-cf-tulpa-binding` | docs: tulpa-binding test summary |
| `feat/tulpa-talents-sandbox` | 10 | 252 | `origin/feat/tulpa-talents-sandbox` (gone) |  | docs: refresh test summary with admin wsId fix + final worker version |
| `feat/unified-deck-ir` | 1 | 58 | _none_ | `pitchpilot-cf-unified-ir` | docs(design): unified deck IR — one path, deterministic HTML+PPTX, round-trippable import (DRAFT) |
| `fix/bootstrap-skip-non-manifest` | 44 | 76 | `origin/fix/bootstrap-skip-non-manifest` (gone) |  | fix: skip non-manifest talent directories during bootstrap |
| `fix/deck-output-assets` | 39 | 76 | _none_ | `pitchpilot-cf-deck-assets` | fix(talents): load 8 image talents (toml->json) + vendor Dify logo SVGs |
| `chore/dev-standard-sandbox-image` | 34 | 76 | `origin/chore/dev-standard-sandbox-image` |  | chore(dev): use stock @cloudflare/sandbox image, drop per-deploy docker build |
| `chore/talents-sync` | 1 | 131 | `origin/chore/talents-sync` |  | chore(talents): rename pp-confluence/main.md → SKILL.md for naming consistency |
| `docs/inventory-2` | 1 | 116 | `origin/docs/inventory-2` |  | docs: PR #88/#89 + #73/#99/#100/#102/#103/#124 audits |
| `docs/inventory-tier2` | 1 | 111 | `origin/docs/inventory-tier2` |  | docs: tier 2 closed — pp-methodology + specialists + dispatch templates (PRs #91-#94) |
| `docs/inventory-tier3` | 1 | 106 | `origin/docs/inventory-tier3` |  | docs: tier 3 closed — onboarding-zh + admin telemetry + MCP PAT + admin users email |
| `docs/inventory-tier4` | 1 | 103 | `origin/docs/inventory-tier4` |  | docs: tier 4 closed — pptx-v2 SVG assembler + builder talent |
| `docs/onboarding-zh` | 1 | 110 | `origin/docs/onboarding-zh` |  | docs: onboarding-zh.md — Chinese new-user guide (aligns PP main #133) |
| `docs/pp-main-inventory` | 1 | 123 | `origin/docs/pp-main-inventory` |  | docs: PP main alignment inventory — running ledger |
| `feat/admin-anthropic-key` | 1 | 81 | `origin/feat/admin-anthropic-key` |  | feat(admin): global Anthropic API key with per-workspace override |
| `feat/admin-email-stats` | 1 | 109 | `origin/feat/admin-email-stats` |  | feat(admin): Users email column + dynamic phase breakdown (aligns PP main #148) |
| `feat/admin-sandbox-inspector` | 2 | 76 | `origin/feat/admin-sandbox-inspector` |  | feat(admin): Sandbox Inspector — diagnose agent state per deck |
| `feat/admin-settings` | 1 | 98 | `origin/feat/admin-settings` |  | feat(admin): Configuration + Connections tabs with OAuth + skill keys + feature flags |
| `feat/admin-telemetry` | 2 | 108 | `origin/feat/admin-telemetry` |  | fix(telemetry): await recordEvent so CF Worker doesn't kill the D1 INSERT |
| `feat/agent-loop-poc` | 26 | 76 | `origin/main` |  | refactor(agent): M4b batch5 — remove claude-code from the image |
| `feat/anthropic-key-panel` | 1 | 88 | `origin/feat/anthropic-key-panel` |  | feat(settings): add Workspace AI panel for per-workspace Anthropic key |
| `feat/artifact-grouper-signals` | 1 | 128 | `origin/feat/artifact-grouper-signals` |  | feat(generic-viewer): backend signals.artifacts[] + artifact-grouper (Stage 2 of #87 alignment) |
| `feat/arx-governance-federation` | 50 | 76 | `origin/feat/arx-governance-federation` | `pitchpilot-cf-arx-federation` | docs: record diff stats vs the M1 net-negative criterion + final status |
| `feat/assemble-svg-deck` | 1 | 106 | `origin/feat/assemble-svg-deck` |  | feat(assembler): SVG-mode deck preview pipeline (aligns PP main 752b3c5) |
| `feat/chat-scroll-batch1` | 6 | 122 | `origin/feat/chat-scroll-batch1` |  | feat(persona): Tier 2 — language-match + pp-cli mandate + audience-not-on-slide (aligns PP main #117/#126) |
| `feat/conceptcloud-race-fix` | 1 | 84 | `origin/feat/conceptcloud-race-fix` |  | fix(perf): ConceptCloud race — wait for contextHydratedDeckId before reading prefetched |
| `feat/confluence-panel-port` | 1 | 89 | `origin/feat/confluence-panel-port` |  | feat(confluence): port PP main zen redesign verbatim |
| `feat/conversation-checkpoint` | 1 | 77 | `origin/feat/conversation-checkpoint` |  | feat(persistence): conversation checkpoint — survive sandbox idle eviction |
| `feat/deck-create-perf` | 1 | 87 | `origin/feat/deck-create-perf` |  | feat(perf): skip 2 redundant roundtrips in deck-create-to-enter |
| `feat/deckdo-prewarm` | 1 | 83 | `origin/feat/deckdo-prewarm` |  | feat(perf): pre-warm DeckDO inside POST createDeck |
| `feat/dedupe-deck-fetches` | 1 | 86 | `origin/feat/dedupe-deck-fetches` |  | feat(perf): dedupe ctx/arts fetch + skip route-effect getDeck on prefetched path |
| `feat/dedupe-deck-fetches-pt2` | 1 | 85 | `origin/feat/dedupe-deck-fetches-pt2` |  | feat(perf): dedupe listDeckMembers internal getDeck + ConceptCloud listContext |
| `feat/dispatch-templates` | 1 | 112 | `origin/feat/dispatch-templates` |  | feat(methodology): dispatch templates + persona hint (Stage D of #90) |
| `feat/edit-comment-cards` | 1 | 117 | `origin/feat/edit-comment-cards` |  | feat(chat): collapse [user-edit] and [user-comment] into cards (aligns PP main #104) |
| `feat/embedded-slide-nav` | 2 | 118 | `origin/feat/embedded-slide-nav` |  | fix(chat): import useLayoutEffect — runtime crash on deck open |
| `feat/force-sandbox-and-skill-mount` | 4 | 142 | `origin/feat/force-sandbox-and-skill-mount` |  | feat(engine): force-sandbox — drop in-Worker anthropic path |
| `feat/generic-viewer-frontend` | 3 | 127 | `origin/feat/generic-viewer-frontend` |  | fix(client): adaptDeck — forward signals.artifacts + active_artifact_id |
| `feat/inspect-anywhere` | 4 | 76 | `origin/feat/inspect-anywhere` |  | feat(deck): AdminRail on left of deck view — Inspector always reachable |
| `feat/inspector-drawer` | 3 | 76 | `origin/feat/inspector-drawer` |  | feat(deck): admin-only Inspector drawer on the preview toolbar |
| `feat/inspector-file-browser` | 5 | 76 | `origin/feat/inspector-file-browser` |  | feat(inspector): Phase 1 file browser + open to deck owners |
| `feat/inspector-file-edit` | 6 | 76 | `origin/feat/inspector-file-edit` |  | feat(inspector): Phase 2 — write text files with ETag concurrency |
| `feat/knowledge-panel` | 1 | 97 | `origin/feat/knowledge-panel` |  | feat(settings): Knowledge sources panel — Confluence + Droploft connect/disconnect |
| `feat/lazy-sandbox-boot` | 28 | 76 | `origin/feat/lazy-sandbox-boot` |  | fix(agent): address review — turn-scoped boot guard + retry on failure |
| `feat/mcp-pat` | 1 | 107 | `origin/feat/mcp-pat` |  | feat(auth): MCP Personal Access Tokens + Settings UI (aligns PP main #135) |
| `feat/memory-proposals` | 43 | 76 | `origin/feat/memory-proposals` |  | docs(memory-proposals): post-review re-verification (decide-first accept + 409) |
| `feat/my-memory-panel` | 1 | 92 | `origin/feat/my-memory-panel` |  | feat(settings+memory): user-scope memory routes + My Memory panel (PP main /dev) |
| `feat/parity-context-files` | 1 | 257 | `origin/feat/parity-context-files` | `pitchpilot-cf-context` | feat(api,web): context files (memory/context/skills) with R2 binary upload |
| `feat/parity-folders-phase-mode` | 1 | 258 | `origin/feat/parity-folders-phase-mode` | `pitchpilot-cf-folders` | feat(api,web): folders + deck.phase + deck.mode/theme + folder_id |
| `feat/parity-foundation` | 3 | 259 | `origin/feat/parity-foundation` | `pitchpilot-cf-parity` | fix(web): adapt SSE hooks + send body to CF event/contract shape |
| `feat/parity-knowledge-panels-frontend` | 1 | 190 | `origin/feat/parity-knowledge-panels-frontend` | `pitchpilot-cf-knowledge-fe` | Merge remote-tracking branch 'origin/main' into feat/parity-knowledge-panels-frontend |
| `feat/parity-multi-tulpa-fanout` | 1 | 180 | `origin/feat/parity-multi-tulpa-fanout` |  | fix(slice-11): scope sandbox fan-out to primary tulpa + echo fan-out |
| `feat/parity-profiles-share` | 2 | 256 | `origin/feat/parity-profiles-share` | `pitchpilot-cf-profiles` | fix(shares): await view_count bump so subsequent reads see it |
| `feat/parity-task-status-cleanup` | 1 | 254 | `origin/feat/parity-task-status-cleanup` | `pitchpilot-cf-task-status` | feat(web): task_status SSE translation + cut confluence + arx admin tabs |
| `feat/persona-10-traits` | 1 | 121 | `origin/feat/persona-10-traits` |  | feat(persona): 10 traits of a great pitch deck (aligns PP main #123) |
| `feat/persona-pp-main-align` | 1 | 132 | `origin/feat/persona-pp-main-align` |  | feat(persona): align pp-writer with PP main 4-phase workflow + Scene awareness |
| `feat/port-pp-talents` | 1 | 233 | `origin/feat/port-pp-talents` |  | feat(talents): port 10 PP talents (pitch-gather, narrative, deck-*, etc.) |
| `feat/pp-cli-scope-flag` | 1 | 92 | `origin/feat/pp-cli-scope-flag` |  | feat(pp-cli): pp save memory --scope flag (aligns PP main #140 + #145) |
| `feat/pp-main-parity` | 40 | 76 | `origin/feat/pp-main-parity` |  | docs(parity): browser verification results for speaker-notes pane |
| `feat/pp-methodology-talent` | 1 | 116 | `origin/feat/pp-methodology-talent` |  | feat(methodology): vendor pp-methodology talent + reference set (Stage A of #90) |
| `feat/pp-writer-persona-v2` | 1 | 113 | `origin/feat/pp-writer-persona-v2` |  | feat(pp-writer): mission-first persona + build doctrine + failure modes (Stage C of #90) |
| `feat/pptx-fix-viewer-quality` | 44 | 76 | `origin/feat/pptx-fix-viewer-quality` |  | fix(review): drop redundant sha256sum in binary self-test; add review notes |
| `feat/pptx-preview-port` | 6 | 210 | `origin/feat/pptx-preview-port` | `pitchpilot-cf-pptx-preview` | fix(pptx): export route doesn't require a presentations row for R2 path |
| `feat/pptx-v2-default` | 1 | 79 | `origin/feat/pptx-v2-default` |  | feat(agent): default to pp-deck-builder-pptx-v2 (SVG/ppt-master) for new decks |
| `feat/pptx-v2-talent` | 1 | 104 | `origin/feat/pptx-v2-talent` |  | feat(pptx-v2): vendor pp-deck-builder-pptx-v2 talent + bind to pp-writer (aligns PP main #1cb287c) |
| `feat/sandbox-faster-cold-start` | 1 | 80 | `origin/feat/sandbox-faster-cold-start` |  | perf(sandbox): bump instance_type to standard + drop unused engine binaries |
| `feat/scoped-memory` | 1 | 95 | `origin/feat/scoped-memory` |  | feat(memory): four-scope agent memory + admin Memory tab (aligns PP main #141) |
| `feat/slide-safe-area-dual-nav` | 41 | 76 | `origin/feat/slide-safe-area-dual-nav` |  | docs(quality): verification — dual-nav live, safe-area fix confirmed (structural) |
| `feat/specialist-tulpas-registry` | 1 | 114 | `origin/feat/specialist-tulpas-registry` |  | feat(tulpas): register 5 specialist tulpas (Stage B of #90) |
| `feat/sprint-1-admin` | 2 | 260 | `origin/feat/sprint-1-admin` |  | docs: README + Phase D test artifacts (10/10 admin checks pass) |
| `feat/sprint-1-auth-workspaces-decks` | 6 | 264 | `origin/feat/sprint-1-auth-workspaces-decks` | `pitchpilot-cf-sprint-1-auth` | fix(crypto): drop PBKDF2 to 100k for CF Workers cap; deploy + smoke-test pass |
| `feat/sprint-1-deckdo-chat` | 4 | 263 | `origin/feat/sprint-1-deckdo-chat` | `pitchpilot-cf-sprint-1-deckdo` | docs: Phase B.1 test artifacts — 6/6 smoke green on prod |
| `feat/sprint-1-frontend` | 3 | 261 | `origin/feat/sprint-1-frontend` | `pitchpilot-cf-web` | docs: Phase C design + test artifacts — 10/10 browser checks pass |
| `feat/sprint-1-real-agent` | 2 | 262 | `origin/feat/sprint-1-real-agent` | `pitchpilot-cf-sprint-1-real-agent` | feat(agent): real Anthropic streaming + echo fallback |
| `feat/stats-chip` | 1 | 94 | `origin/feat/stats-chip` |  | feat(nav): active-time DeckTimeChip + DeckStatsPopover (aligns PP main StatsChip) |
| `feat/storyboard-preview-edit-export` | 6 | 253 | `origin/feat/storyboard-preview-edit-export` | `pitchpilot-cf-storyboard-edit` | docs: capture review findings + resolution for storyboard PR |
| `feat/storyboard-tab-md-title` | 1 | 121 | `origin/feat/storyboard-tab-md-title` |  | feat(preview): Storyboard tab renames to doc title (aligns PP main #129) |
| `feat/sync-dev-tulpas` | 1 | 76 | `origin/feat/sync-dev-tulpas` |  | feat(talents): sync 8 new design-format talents from PP main dev |
| `feat/talents-native-tools-dify-sop` | 41 | 76 | `origin/feat/talents-native-tools-dify-sop` |  | docs(quality): verification PASS — native-tool build + on-brand Dify palette |
| `feat/workspace-rail-profile` | 12 | 76 | `origin/main` |  | fix(oasis): surface ALL engine errors, not just auth |
| `fix/acp-auth-bailout` | 1 | 140 | `origin/fix/acp-auth-bailout` |  | fix(acp): don't bail on advertised authMethods — let session/new decide |
| `fix/acp-force-kill` | 1 | 139 | `origin/fix/acp-force-kill` |  | fix(acp): force-kill engine after session/prompt — escalate SIGTERM/SIGKILL |
| `fix/acp-kill-not-error` | 1 | 138 | `origin/fix/acp-kill-not-error` |  | fix(acp): don't surface SIGTERM/SIGKILL as turn error when stopReason was clean |
| `fix/acp-prompt-timeout` | 2 | 137 | `origin/fix/acp-prompt-timeout` |  | fix(acp): null stopReason — surface as cold-boot error, not 'killed by SIGTERM' |
| `fix/acp-turn-stall` | 2 | 141 | `origin/fix/acp-turn-stall` |  | fix(acp): don't bail on advertised authMethods — let session/new decide |
| `fix/admin-decks-shape` | 2 | 102 | `origin/fix/admin-decks-shape` |  | fix(admin): rewrite SystemManager for PP-CF health shape |
| `fix/build-artifact-cwd` | 28 | 76 | `origin/fix/build-artifact-cwd` |  | fix(agent): guide builds to write under the deck root |
| `fix/cold-boot-retry` | 1 | 135 | `origin/fix/cold-boot-retry` |  | fix(sandbox): retry once on cold-boot engine failure |
| `fix/cold-retry-v2` | 1 | 134 | `origin/fix/cold-retry-v2` |  | fix(sandbox): retry cold-boot twice (was once) — catches sluggish containers |
| `fix/confluence-auto-prompt` | 1 | 99 | `origin/fix/confluence-auto-prompt` |  | fix(confluence): auto-prompt connect panel once per session on unconfigured deck |
| `fix/confluence-event-listener` | 1 | 96 | `origin/fix/confluence-event-listener` |  | fix(confluence): listen for KnowledgePanel's pp:open-confluence-connect event |
| `fix/d1-sync-regressions` | 1 | 133 | `origin/fix/d1-sync-regressions` |  | fix(d1-sync): inline text memory + auto phase advance + slides_count recount |
| `fix/deck-open-signals` | 39 | 76 | `origin/fix/deck-open-signals` |  | docs(deck-open): browser verification PASS |
| `fix/deck-switch-workspace-state` | 29 | 76 | `origin/fix/deck-switch-workspace-state` |  | fix(web): reset Workspace state on deck switch |
| `fix/deck-view-remount-on-switch` | 30 | 76 | `origin/fix/deck-view-remount-on-switch` |  | fix(web): clear+reload per-deck state on back/forward navigation |
| `fix/droploft-panel-parity` | 1 | 100 | `origin/fix/droploft-panel-parity` |  | fix(droploft): port PP main panel verbatim — simpler single-connection setup |
| `fix/enable-confluence-panel` | 1 | 101 | `origin/fix/enable-confluence-panel` |  | fix(confluence): re-enable panel — clicking button silently did nothing |
| `fix/export-pptx-bug` | 1 | 125 | `origin/fix/export-pptx-bug` |  | fix(export): rewrite /export.pptx + add /export for HTML download |
| `fix/google-oauth-config` | 1 | 90 | `origin/fix/google-oauth-config` |  | fix(auth): Google OAuth — correct URL + admin Configuration takes effect |
| `fix/hide-pickmode-ui` | 2 | 131 | `origin/fix/hide-pickmode-ui` |  | fix(docker): retry npm install on transient EPIPE under QEMU buildx |
| `fix/lazyslide-hoist` | 1 | 93 | `origin/fix/lazyslide-hoist` |  | fix(dashboard): hoist LazySlide out of DeckDashboard (aligns PP main #120) |
| `fix/nav-axis-aware` | 44 | 76 | `origin/fix/nav-axis-aware` | `pitchpilot-cf-nav-axis` | docs(review): nav-axis-aware review + fix two stale comments (current->target, bottom->axis-aware) |
| `fix/panel-tab-stickiness` | 44 | 76 | `origin/fix/panel-tab-stickiness` | `pitchpilot-cf-panel-logic` | docs: review notes for panel-tab-stickiness |
| `fix/pp-writer-sandbox-prompt` | 2 | 136 | `origin/fix/pp-writer-sandbox-prompt` |  | fix(prompt): plug two more reverse-overwrite paths |
| `fix/preview-toolbar-grouping` | 32 | 76 | `origin/fix/preview-toolbar-grouping` |  | fix(preview): group toolbar into Export / More dropdowns (was overlapping) |
| `fix/preview-version-switch` | 31 | 76 | `origin/fix/preview-version-switch` |  | fix(preview): version switch follows current_version (was stuck on newest) |
| `fix/session-resume-fallback` | 1 | 131 | `origin/fix/session-resume-fallback` |  | fix(resume): inject Previous Conversation into CLAUDE.md so turn N+1 has context when --resume fails |
| `fix/sse-context-refresh` | 43 | 76 | `origin/fix/sse-context-refresh` |  | docs: test artifacts + SSE evidence for context-refresh fix |
| `fix/stuck-building-on-reopen` | 33 | 76 | `origin/fix/stuck-building-on-reopen` |  | fix(web): clear stuck 'Building' indicator on deck reopen |
| `fix/stuck-turn-recovery` | 1 | 255 | `origin/fix/stuck-turn-recovery` | `pitchpilot-cf-stuck-turn` | fix(deckdo): stuck-turn auto-recovery + /reset escape hatch + 50s timeout |
| `perf/assemble-parallel` | 1 | 125 | `origin/perf/assemble-parallel` |  | perf(preview): parallelize R2 fetches in assembleDeck (~5x speedup) |
| `refactor/agent-turn-memory` | 38 | 76 | `origin/refactor/agent-turn-memory` | `pitchpilot-cf-agent-memory` | fix(talents): address review — manifest desc, yaml WebSearch refs, dead export |
| `refactor/cleanup-buildmodepicker` | 1 | 126 | `origin/refactor/cleanup-buildmodepicker` |  | refactor(generic-viewer): retire BuildModePicker + mode_required gate (Stage 4 of #87 alignment) |
| `refactor/worker-side-artifact-sync` | 41 | 76 | `origin/refactor/worker-side-artifact-sync` |  | docs(boot): browser verification PASS + test report/summary |
| `revert/deckdo-prewarm` | 1 | 82 | `origin/revert/deckdo-prewarm` |  | revert: 'feat(perf): pre-warm DeckDO inside POST createDeck' (#123) |
| `spike/svg-to-pptx` | 43 | 76 | `origin/main` | `pitchpilot-cf-pptx-spike` | spike(pptx): SVG->editable PPTX in the Worker (pure JS, no python/sandbox) |
| `v2-dev` | 5 | 102 | `origin/v2-dev` | `pitchpilot-cf-v2-dev` | docs: add attention-first focus prototype |


## Raw Data

See `branch-audit.tsv` in this directory for the full branch list including branches already contained in `dev`.
