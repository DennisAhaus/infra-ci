---
name: feature-workspace-lifecycle
description: 'Manage feature workspaces under requirements/open and requirements/done. Use for creating plan-first feature folders, tracking in-progress work, validating completion, and archiving finished work atomically.'
argument-hint: 'Provide feature slug and desired action: create, update, verify-done, or archive'
---

# Feature Workspace Lifecycle

## When to Use
- You are starting a non-trivial change and need a structured workspace.
- You need visibility over what is currently open.
- You need a deterministic closeout and archive flow.

## Procedure
1. Create or reuse `requirements/open/<feature-slug>/`.
2. Ensure `plan.md` exists before implementation begins.
3. Keep `plan.md` updated after each completed step.
4. Add or update `finished.md` only when work is genuinely complete.
5. Verify completion criteria from `plan.md` are fully satisfied.
6. Confirm no open blockers remain in feature notes.
7. Move the entire folder to `requirements/done/<feature-slug>/`.
8. Re-check directory state so `requirements/open/<feature-slug>/` no longer exists.

## Required Files
- `requirements/open/<feature-slug>/plan.md`
- `requirements/open/<feature-slug>/finished.md` (at completion time)

## Validation Checklist
- Plan status is `completed`.
- `finished.md` contains completion date, summary, and verification notes.
- Folder move preserves all artifacts and history.

## Output Expectations
- Clear status of open vs done feature folders.
- File references for created/updated/moved artifacts.
- Explicit confirmation when archive is complete.
