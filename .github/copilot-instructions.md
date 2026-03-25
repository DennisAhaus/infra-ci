# Copilot Instructions for infra-ci

## Short AI hints
- Read `docs/ai/hints.md` for the short repo-specific hints before starting work.
- If the task affects shared infrastructure, deployment, or pipelines, also read `/Users/dennisahaus/dev/dtsoft-office/development/docs/servers.md` and `/Users/dennisahaus/dev/dtsoft-office/development/docs/infrastructure.md`.

## Local auth workflow
- When GitHub, Vault, Concourse, `fly`, or Keycloak OIDC tokens are needed, run `source ~/dev/authenticate.sh` on the local macOS host to load the approved environment variables for that workflow.
- `fly` and `vault` are installed directly on this Mac host, so prefer the host `fly` and `vault` binaries instead of repo-local copies.

## Topic workspace protocol
- For non-trivial features, bugs, refactors, and ideas, use one shared topic folder at `requirements/open/<topic-slug>/`.
- The canonical workspace plan is `requirements/open/<topic-slug>/plan.md`.
- If the user provides or attaches a `plan.md` file in chat, treat that exact file as the active plan and stay aligned to it. Do not create, switch to, or use another plan unless the user explicitly instructs it.
- If no active plan exists yet, create or reuse `plan.md` before substantial work.
- Orchestrator agents must update the active plan after each completed work step so progress and status stay current.
- Keep follow-up notes and closeout material in the same topic folder; use `requirements/open/<topic-slug>/finished.md` when the topic is complete.

## Agent routing
All work in this repo is handled by a dedicated agent set. Use the orchestrator as the
single entry point; it routes to specialist agents automatically.

| Agent               | Invoke with         | Responsibility                                              |
|---------------------|---------------------|-------------------------------------------------------------|
| Orchestrator        | `@infra-ci`         | Entry point – routes to all other agents                    |
| Cert lifecycle      | `@cert-lifecycle`   | Nginx/certbot bootstrap, issuance, and renewal              |
| Pipeline auditor    | `@pipeline-auditor` | Consistency audit, release gate, trigger policy             |
| Fly deploy          | `@fly-deploy`       | `fly set-pipeline`, unpause, trigger, and verification      |
| Vault checker       | `@vault-checker`    | `((var))` resolution and Vault path contract verification   |
| Plan visualiser     | `@visualize`        | Dry-run execution preview without making any changes        |

Agent files live in `.github/agents/`. Each agent reads its corresponding skill(s) from
`.github/skills/` before acting.

## Git publication defaults
- For implementation work, agents should usually finalize by running
	`git add -A`, committing, and pushing after successful validation.
- Skip commit/push when there is no diff, checks fail, auth is missing, or the
	user explicitly asks not to publish.
- Commit messages should be focused and non-interactive.
- Exception: the `@visualize` agent is planning-only and never publishes code.