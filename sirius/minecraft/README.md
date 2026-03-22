# Minecraft

Minecraft server running PaperMC (Bukkit-compatible) via itzg/minecraft-server.

## Access

- **Port:** 25565 (standard Minecraft port)
- **Connect:** sirius-tailscale-ip:25565 or LAN IP:25565
- No domain proxy — connect directly via IP

## Server Type

Running PaperMC (`TYPE: PAPER`), which provides:
- Bukkit plugin compatibility
- Spigot plugin compatibility  
- Performance improvements over vanilla

## Notes

- Plugins go in `/srv/appdata/minecraft/plugins` on Sirius
- JVM memory capped at 4G — adjust `MEMORY` in compose if needed
- `stdin_open` and `tty` enable the Minecraft console via 
  `docker attach minecraft`
- To detach from console without stopping: `Ctrl+P` then `Ctrl+Q`

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /srv/appdata/minecraft | /data | World data, server config |
| /srv/appdata/minecraft/plugins | /plugins | Bukkit/Paper plugins |
```

`sirius/minecraft/.gitignore`:
```
.env