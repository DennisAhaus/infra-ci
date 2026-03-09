---
name: safe-fly-deploy-playbook
description: 'Run safe Concourse fly deployment workflow. Use for repeatable validate, set, unpause, trigger, and verification steps across targets while preserving team and pipeline safety checks.'
argument-hint: 'Provide target, pipeline path, and pipeline name'
---

# Safe Fly Deploy Playbook

## When to Use
- You are changing one or more Concourse pipelines.
- You need a consistent rollout checklist.
- You want explicit safety checks before and after deployment.

## Procedure
1. Confirm the correct `fly` binary and target are selected.
2. Validate pipeline syntax and vars interpolation assumptions.
3. Set pipeline with non-interactive command options.
4. Unpause pipeline when required.
5. Trigger representative jobs if policy allows.
6. Observe job status and logs until green or triaged.
7. Record commands and outcomes for change traceability.

## Safety Rules
- Use correct team target for pipeline category.
- Avoid deprecated instances and endpoints.
- Keep secret values out of command output and logs.
- Stop and report if unexpected failures or state drift appears.

## Output
- Command transcript summary.
- Validation and rollout status.
- Follow-up actions if checks fail.
