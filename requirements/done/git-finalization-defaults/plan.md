# Git Finalization Defaults For Agents

Type: enhancement
Status: completed

## Goal
Make all repository agents default to `git add`, commit, and push when changes are complete and validated, unless safety conditions block publication.

## Scope
- Update all `.github/agents/*.agent.md` files.
- Update `.github/copilot-instructions.md` to align global routing behavior.

## Planned Steps
1. Audit current agent docs for git finalization behavior.
2. Add a shared policy section to each agent with default commit/push behavior.
3. Add global guidance to copilot instructions so orchestrator and specialists remain aligned.
4. Validate file consistency and summarize resulting workflow.

## Completion Criteria
- Every agent file includes explicit default behavior for add/commit/push.
- Policy includes safety checks for failed validation/auth/no changes.
- Global instruction file reflects the same expectation.

## Completion Notes
- Added `Git finalization policy` sections to all agent definitions.
- Added global `Git publication defaults` to `.github/copilot-instructions.md`.
- Kept `@visualize` explicitly read-only with no commit/push behavior.
