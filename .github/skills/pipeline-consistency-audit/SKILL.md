---
name: pipeline-consistency-audit
description: 'Audit and align pipeline structure across repos and environments. Use for detecting drift in job topology, task interfaces, cert handling patterns, and trigger wiring between related pipelines.'
argument-hint: 'Provide repos, pipeline names, or categories to compare'
---

# Pipeline Consistency Audit

## When to Use
- Multiple pipelines implement the same lifecycle differently.
- You need one canonical structure for repeated pipeline types.
- You want to refactor with low risk and clear diff boundaries.

## Procedure
1. Collect candidate pipelines by category and environment.
2. Compare job names, ordering, and gating semantics.
3. Compare task parameters, expected inputs, and output contracts.
4. Flag deviations that are intentional versus accidental drift.
5. Propose a canonical baseline for each pipeline family.
6. Refactor out duplicated shell blocks into shared scripts/tasks.
7. Update all pipelines to consume the shared assets consistently.
8. Validate each pipeline with `fly validate-pipeline`.

## Deliverables
- Drift report: what differs and why it matters.
- Canonical pattern for each pipeline family.
- Minimal refactor patch set with consistency improvements.
- Validation summary and residual risks.
