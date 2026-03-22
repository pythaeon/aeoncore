# Dozzle

Real-time Docker container log viewer. Runs in hub mode, aggregating 
logs from all aeoncore hosts.

## Access

- **UI:** dozzle.aeoncore.net
- **Internal port:** 8083 (mapped from container port 8080)

## Architecture

Dozzle uses a hub + agent model, similar to Beszel.
- Hub runs on Sirius and provides the unified web UI
- Agent runs on Deneb (see deneb/dozzle-agent)
- Hub connects to agents over port 7007

## Notes

- Read-only access to Docker socket — no ability to start/stop containers
- No authentication by default — access is gated by Tailscale
- Log level set to `info` — change `DOZZLE_LEVEL` to `debug` if needed
- Previously accessed via CasaOS UI — now has a dedicated NPM entry

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /var/run/docker.sock | /var/run/docker.sock | Docker log access (read-only) |

## Related

- See `deneb/dozzle-agent` for the Deneb agent configuration