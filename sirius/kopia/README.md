# Kopia

Backup management. Backs up `/srv/appdata` on Sirius to a Kopia 
repository stored on Vega (TrueNAS) via network mount.

## Access

- **UI:** kopia.aeoncore.net
- **Internal port:** 51515

## Credentials

Three separate credentials are required — see `.env.example`:

| Variable | Purpose |
|----------|---------|
| KOPIA_SERVER_USERNAME | Web UI login username |
| KOPIA_SERVER_PASSWORD | Web UI login password |
| KOPIA_REPO_PASSWORD | Repository encryption key |

> ⚠️ The repository password is used to encrypt all backups. If lost,
> backups cannot be recovered. Store this somewhere safe outside of 
> this repository (e.g. a password manager).

## Backup Scope

| Source (host) | Container path | What it backs up |
|---------------|----------------|-----------------|
| /srv/appdata | /data (read-only) | All Sirius service data |
| /mnt/shared/backups/kopia | /repository | Backup destination on Vega |

## Notes

- Repository lives on Vega at `/mnt/shared/backups/kopia` via NFS/SMB mount
- `/srv/appdata` is mounted read-only — Kopia cannot modify source data
- Backup schedules and retention policies are configured in the Kopia UI
- `--insecure` flag is acceptable here since access is Tailscale-gated

## NFS Mount

The backup repository depends on an NFS mount from Vega being available at 
`/mnt/shared`. This must be present before Kopia starts or the repository 
will be inaccessible.

| Detail | Value |
|--------|-------|
| NFS server | 192.168.100.13 (Vega, LAN IP) |
| Export path | /mnt/data/shared |
| Mount point | /mnt/shared on Sirius |
| Version | NFSv4.2 |
| fstab entry | `192.168.100.13:/mnt/data/shared /mnt/shared nfs defaults,_netdev 0 0` |

The `_netdev` flag in fstab tells the OS to wait for network availability 
before mounting — important for a VM that boots before the NAS is ready.

> ⚠️ If Vega is offline or the NFS mount fails, Kopia will start but 
> backups will fail. Check mount status with `mount | grep /mnt/shared`.

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /srv/appdata/kopia | /app/config | Kopia config and metadata |
| /mnt/shared/backups/kopia | /repository | Backup repository on Vega |
| /srv/appdata | /data | Backup source (read-only) |
```

`sirius/kopia/.gitignore`:
```
.env