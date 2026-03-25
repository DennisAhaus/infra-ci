# Concourse Event Stream Timeout

Type: bug
Status: completed

## Goal
Stop the shared infra nginx proxy from closing long-lived Concourse build event streams on `concourse.dtsoft.cloud`.

## Expected Behavior
Viewing a live Concourse build should keep `/api/v1/builds/<id>/events` open long enough for normal SSE/event-stream idle periods without nginx returning upstream timeout errors.

## Actual Behavior
Grafana shows repeated `upstream timed out (110: Operation timed out) while reading upstream` errors for `GET /api/v1/builds/209996/events` on `concourse.dtsoft.cloud`.

## Reproduction Path
1. Open a live Concourse build page on `https://concourse.dtsoft.cloud`.
2. Leave the page open while the build event stream is idle for longer than the proxy read timeout.
3. Observe timeout errors from `infra-nginx` in Grafana and stalled/retried event stream requests.

## Suspected Root Cause
The shared `infra-nginx` template uses `proxy_read_timeout 90;` on the catch-all Concourse location. The Concourse build events endpoint is a long-lived stream and can legitimately stay open longer than 90 seconds between chunks.

## Fix Plan
1. Add a dedicated Concourse events location in the shared nginx template.
2. Increase stream-safe read/send timeouts for that endpoint and disable proxy buffering there.
3. Validate the nginx template locally.
4. If validation passes, prepare or perform rollout to the infra host.

## Relevant Files
- `ci/templates/infra-nginx.conf`
- `ci/pipelines/infra-nginx.yml`
- `ci/tasks/infra-nginx-deploy.yml`

## Verification
- `nginx -t` through the existing pipeline validation logic
- Manual config inspection for the Concourse events location
- Optional live smoke check against `https://concourse.dtsoft.cloud/api/v1/builds/<id>/events`

## Completion Notes
- Added a dedicated Concourse build-events location with `proxy_buffering off` and `3600s` read/send timeouts.
- Validated the updated host-mounted config on `infra.dtsoft.cloud` with a fresh `nginx:alpine` container.
- Recreated the live `infra-nginx` container so the bind-mounted file was remounted and the new location became active.