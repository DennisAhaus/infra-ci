# Git Finalization Defaults For Agents

Completed on 2026-03-25.

- Updated all repository agent definitions to default to `git add -A`, commit,
  and push after successful validation.
- Added safety conditions to skip publication when no diff exists, checks fail,
  auth is missing, or publication is intentionally paused.
- Added an explicit read-only exception for `@visualize` so it never stages,
  commits, or pushes.
- Updated `.github/copilot-instructions.md` with global git publication defaults.
