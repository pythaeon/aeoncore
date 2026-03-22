# Tailscale

Tailscale VPN client running as a container on Sirius. Functions as the 
network and authentication layer for all aeoncore services.

## Access

- **Admin:** https://login.tailscale.com/admin/machines
- **No web UI** on Sirius itself — managed via Tailscale admin console

## Notes

- Uses `network_mode: host` — binds directly to host network, not Docker bridge
- Auth state is persisted in the volume, so re-authentication is not required 
  on restart
- This is a critical dependency — if Tailscale goes down, all *.aeoncore.net 
  domains become unreachable via Tailnet (LAN access still works)
- `TS_USERSPACE: false` means it uses the kernel's TUN interface rather than 
  a userspace implementation — more performant and reliable

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /srv/appdata/tailscale/state | /var/lib/tailscale | Auth state and config |
| /dev/net/tun | /dev/net/tun | Kernel TUN interface |
```

`sirius/tailscale/.gitignore`:
```
.env