# NFS Mounts

NFS shares exported from Vega (TrueNAS, 192.168.100.13) and mounted 
on other hosts.

## Sirius

| Mount point | NFS export | Purpose |
|-------------|-----------|---------|
| /mnt/shared | /mnt/data/shared | Kopia backup repository |

### fstab entry
```
192.168.100.13:/mnt/data/shared  /mnt/shared  nfs  defaults,_netdev  0  0
```

### Notes
- `_netdev` ensures mount waits for network before attempting
- Verify mount is active before starting Kopia: `mount | grep /mnt/shared`
- If mount drops: `sudo mount -a` to remount all fstab entries

## Deneb

No NFS mounts currently configured.