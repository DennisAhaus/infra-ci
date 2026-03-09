---
name: concourse-release-gate-validator
description: 'Validate production release-triggered pipelines and staging push-triggered pipelines. Use for preventing trigger regressions in related deploy flows.'
argument-hint: 'Provide pipeline names or teams to validate trigger policy'
---

# Concourse Release Gate Validator

## When to Use
- Trigger policy may have drifted after edits.
- Production should only deploy from release events.
- Staging should stay branch push triggered.

## Procedure
1. Locate production and staging pipeline definitions.
2. Verify production uses release resources and release-triggered jobs.
3. Verify staging uses branch push resources and expected filters.
4. Confirm independent pipelines keep intended trigger behavior.
5. Check for accidental auto-trigger in protected production jobs.
6. Report mismatches and apply targeted fixes.
7. Validate all modified pipelines with `fly validate-pipeline`.

## Output
- Trigger policy compliance matrix by pipeline.
- Exact mismatches and fixes applied.
- Validation result summary.
