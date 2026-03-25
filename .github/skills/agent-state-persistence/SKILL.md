---
name: agent-state-persistence
description: 'Persist multi-agent execution state per feature. Use for per-agent status files, restart-safe handoff, activity logging, and crash recovery under requirements/open/<feature-slug>/.'
argument-hint: 'Provide feature slug and active agents to initialise or resume state tracking'
---

# Agent State Persistence

## When to Use
- Multiple agents collaborate on one feature.
- You need crash recovery and resumable execution.
- You need transparent tracking of active and blocked work.

## Procedure
1. Ensure feature workspace exists at `requirements/open/<feature-slug>/`.
2. Create or update orchestrator state file:
   `requirements/open/<feature-slug>/orchestrator-agent.md`.
3. Create or update per-agent state files as needed:
   - `cert-lifecycle-agent.md`
   - `pipeline-auditor-agent.md`
   - `fly-deploy-agent.md`
   - `vault-checker-agent.md`
   - `visualize-agent.md`
4. Use the same state schema in each file:
   - Agent name
   - Status (`not-started|in-progress|blocked|done`)
   - Current step
   - Last completed step
   - Next step
   - Inputs/outputs
   - Blockers
   - Resume instructions
   - Last updated timestamp
5. Append execution milestones to `activity.log`.
6. Record inter-agent dependencies and unresolved decisions in `handoff.md`.
7. On restart, read `orchestrator-agent.md` first, then continue from each file's `Next step`.

## Recommended Artifacts
- `requirements/open/<feature-slug>/activity.log`
- `requirements/open/<feature-slug>/handoff.md`
- `requirements/open/_index.md` (global open-work dashboard)

## Validation Checklist
- Every active agent has a current state file.
- At most one orchestrator-selected active execution focus exists at a time.
- Blockers are visible in both agent state and handoff notes.
- Restart path is explicit and executable without guesswork.

## Output Expectations
- Current active agent and next action.
- Last checkpoint and resume point after interruption.
- Clear list of open blockers and owners.
