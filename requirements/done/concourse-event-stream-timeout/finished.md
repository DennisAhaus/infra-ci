# Concourse Event Stream Timeout

Completed on 2026-03-10.

- Root cause: the shared `infra-nginx` Concourse vhost only had `proxy_read_timeout 90;` on the catch-all proxy location, which is too short for long-lived build event streams.
- Fix: added a dedicated `location ~ ^/api/v1/builds/[0-9]+/events$` block with `proxy_buffering off`, `proxy_send_timeout 3600s`, and `proxy_read_timeout 3600s`.
- Verification: validated the updated config on the infra host with `nginx -t` in a fresh container, then recreated the live `infra-nginx` container and confirmed the running config contains the new events location.