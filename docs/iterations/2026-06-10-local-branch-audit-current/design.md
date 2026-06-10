---
title: Local Branch Audit
date: 2026-06-10
---

# Goal

Audit local PitchPilot CF branches and worktrees after creating the `dev` integration branch.

# Approach

- Use `origin/dev` as the current integration baseline.
- Compare every local branch and remote branch against `origin/dev` and `origin/main`.
- Identify local branches with commits not included in `origin/dev`.
- Identify worktrees with uncommitted files.
- Classify branch state as already integrated, candidate for migration, or archival.

# Scope

This iteration only records git state and recommendations. It does not merge, cherry-pick, delete, or rewrite any branch.

# Test Plan

- Fetch and prune `origin`.
- Capture `git branch -vv`.
- Capture all local worktrees.
- Capture per-branch ahead/behind counts versus `origin/dev` and `origin/main`.
- Capture worktree dirty status.
