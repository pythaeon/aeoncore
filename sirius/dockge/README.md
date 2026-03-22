# Dockge

Container stack management UI.

## Access

- **UI:** dockge.aeoncore.net
- **Internal port:** 5001

## Notes

- Stacks directory mapped to `/srv/appdata` — Dockge treats each 
  subdirectory as a potential stack
- Docker socket mounted for container management
- Under review for replacement with Komodo once aeoncore GitOps 
  workflow is established
- No secrets required

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /var/run/docker.sock | /var/run/docker.sock | Docker access |
| /srv/appdata/dockge | /app/data | Dockge config and data |
| /srv/appdata | /opt/stacks | Stack definitions |
```

`sirius/dockge/.gitignore`:
```
.env