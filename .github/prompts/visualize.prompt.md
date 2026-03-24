---
description: "Visualize prompt - Shows the tasks, actions, files, checks, and execution order that would be used to implement the current plan without making changes"
---

# Visualize Plan

## Role
Planning-only dry-run prompt that turns the current plan or request into an explicit execution preview for this repository. Show what would be done, in what order, and what would be validated, without implementing anything.

## Context Loading
Before answering, read:
1. `.github/copilot-instructions.md` if it exists
2. `docs/ai/hints.md` if it exists
3. The active plan file, requirement note, or user-referenced files for this repo

## Rules
- Stay in "would do" mode throughout.
- Do not edit files, run commands, stage changes, commit, push, deploy, or access external systems.
- Keep the visualization scoped to this repository unless the user explicitly asks for cross-repo dependencies.
- If the source plan is incomplete, state the missing assumptions before continuing.
- Prefer concrete file paths, checks, and sequencing over generic advice.

## What to Visualize
1. Goal and scope
2. Ordered phases or tasks
3. Concrete actions per phase
4. Likely files, folders, or configs affected
5. Commands, checks, or builds that would be run
6. Validation and rollback checkpoints
7. Risks, blockers, and open questions

## Output
```markdown
### Plan Visualization
Goal: [what would be implemented]
Scope: [repo-local scope and assumptions]

### Execution Sequence
1. [Phase or task]
   Would inspect: [...]
   Would change: [...]
   Would run: [...]
   Would validate: [...]

2. [Phase or task]
   Would inspect: [...]
   Would change: [...]
   Would run: [...]
   Would validate: [...]

### Likely Files
- [file or directory]
- [file or directory]

### Risks / Blockers
- [risk or unknown]

### Not Executed
- No files were changed
- No commands were run
- No git, deployment, secret, or external-system actions were performed
```