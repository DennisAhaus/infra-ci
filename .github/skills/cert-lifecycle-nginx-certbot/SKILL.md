---
name: cert-lifecycle-nginx-certbot
description: 'Standardize nginx and certbot certificate lifecycle handling across pipelines. Use for self-signed bootstrap, Lets Encrypt issuance, 4-week renewal checks, and idempotent cert operations in nginx and certbot tasks.'
argument-hint: 'Provide pipeline paths or repo names to validate/refactor cert lifecycle logic'
---

# Certificate Lifecycle for Nginx and Certbot

## When to Use
- You maintain separate nginx and certbot pipelines.
- Nginx can fail because certificates are missing.
- You need consistent logic across production and staging variants.
- You need idempotent bootstrap and renewal behavior.

## Procedure
1. Identify each nginx deploy task and certbot bootstrap/renew task in scope.
2. Ensure nginx deploy path includes a preflight certificate check.
3. If no certificate exists, generate a temporary self-signed certificate so nginx can start.
4. Ensure certbot path evaluates certificate state before action.
5. If certificate is self-signed, run certbot to issue or replace with Lets Encrypt.
6. If certificate expires within 28 days, run certbot renewal.
7. If certificate is valid and not near expiry, skip issuance/renewal.
8. Keep operations idempotent: repeated runs with unchanged cert state must be no-op.
9. Centralize shared shell logic in reusable scripts/tasks and call from all pipelines.
10. Validate with dry-run checks and pipeline-level validation commands.

## Required Checks
- Nginx starts when no trusted cert exists.
- Certbot replaces self-signed cert when domain and challenge are valid.
- Renewal runs only when self-signed or near-expiry conditions match.
- Re-running tasks does not break state or duplicate configuration.

## Output Expectations
- Unified cert management script or task template.
- Updated pipeline/task references pointing to shared logic.
- Evidence of validation commands and outcomes.
