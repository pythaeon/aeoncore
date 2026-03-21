# aeoncore Service Map

## Network Architecture

All services are accessed exclusively via Tailscale, with Nginx Proxy Manager 
routing traffic from `*.aeoncore.net` subdomains to their respective hosts. 
Direct IP:port access is reserved for initial deployment testing only.

Tailscale functions as both a network layer and a lightweight auth layer — 
only devices explicitly enrolled in the Tailnet can reach any service.

---

## Hosts

| Name | Type | Tailscale IP | Role |
|------|------|--------------|------|
| Proxmox | Bare metal | 100.74.96.13 | Hypervisor |
| Sirius | Ubuntu VM | 100.68.121.95 | General services |
| Deneb | Ubuntu VM | 100.81.57.104 | AI services |
| Vega | TrueNAS VM | 100.102.180.38 | Storage, Nextcloud |

> **Naming convention:** Servers are named after stars. Personal computers 
> are named after spacecraft (e.g. Discovery = primary Windows desktop).

---

## Services

### Sirius (100.68.121.95)

| Domain | Port | Service | Notes |
|--------|------|---------|-------|
| beszel.aeoncore.net | 8090 | Beszel | Server monitoring UI |
| dockge.aeoncore.net | 5001 | Dockge | Container stack manager |
| homepage.aeoncore.net | 3002 | Homepage | Personal dashboard |
| kopia.aeoncore.net | 51515 | Kopia | Backup management |
| npm.aeoncore.net | 81 | Nginx Proxy Manager | Reverse proxy admin |
| pihole.aeoncore.net | 8081 | Pihole | DNS + ad blocking |
| sirius.aeoncore.net | 8082 | CasaOS | Server UI (legacy, under review) |

### Deneb (100.81.57.104)

| Domain | Port | Service | Notes |
|--------|------|---------|-------|
| tau.aeoncore.net | 3000 | Open WebUI | LLM front-end (Ollama) |
| ceti.aeoncore.net | 8188 | ComfyUI | Image generation |
| n8n.aeoncore.net | 5678 | n8n | Workflow automation |

### Vega / TrueNAS (100.102.180.38)

| Domain | Port | Service | Notes |
|--------|------|---------|-------|
| nas.aeoncore.net | 443 | TrueNAS UI | Primary alias |
| vega.aeoncore.net | 443 | TrueNAS UI | Secondary alias |
| nextcloud.aeoncore.net | 30027 | Nextcloud | File sync, runs as TrueNAS app |

### Proxmox (100.74.96.13)

| Domain | Port | Service | Notes |
|--------|------|---------|-------|
| pve.aeoncore.net | 8006 | Proxmox UI | Currently routed via LAN IP — todo: switch to Tailscale IP |

---

## Open Items

- [ ] Update `pve.aeoncore.net` NPM entry to use Tailscale IP (100.74.96.13:8006)
- [ ] Evaluate removing CasaOS from Sirius once aeoncore workflow is established
- [ ] Evaluate migrating from Dockge to Komodo for GitOps-style deployments