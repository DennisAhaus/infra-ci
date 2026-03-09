---
name: vault-vars-contract-check
description: 'Verify Concourse variable contracts against Vault paths. Use for detecting missing vars, stale keys, unresolved interpolations, and path mismatches before pipeline deploy.'
argument-hint: 'Provide pipeline files or team targets to check'
---

# Vault Variable Contract Check

## When to Use
- Pipelines fail due to missing `((var))` values.
- Secrets were renamed or moved in Vault.
- You need a pre-deploy credentials contract check.

## Procedure
1. Extract all interpolated vars from target pipeline and task files.
2. Map vars to expected Vault lookup order for the team and pipeline.
3. Verify each required key exists at the resolved Vault path.
4. Identify unused or duplicate keys that should be cleaned up.
5. Report unresolved keys with exact file references.
6. Propose minimal key additions or pipeline key renames.
7. Re-validate pipelines after updates.

## Output
- Missing keys list.
- Unused keys list.
- Suggested Vault update operations.
- Post-fix validation status.
