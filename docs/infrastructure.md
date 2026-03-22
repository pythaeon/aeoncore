# aeoncore Infrastructure

## Overview

aeoncore is a self-hosted home services stack running on a Proxmox hypervisor 
with three VMs. All services are containerized via Docker and managed through 
Docker Compose. Access is gated entirely through Tailscale.

---

## Proxmox Host

- **Role:** Hypervisor
- **Access:** pve.aeoncore.net
- **Notes:** Hosts all three VMs. No services run directly on the host.

---

## Virtual Machines

### Sirius
- **OS:** Ubuntu LTS
- **Tailscale IP:** 100.68.121.95
- **Role:** General services
- **Compose files:** `/srv/appdata/<service>/docker-compose.yml`
- **Services:** Pihole, Nginx Proxy Manager, Tailscale, Beszel, Uptime Kuma, 
  Dozzle, Homepage, Kopia, Dockge, Minecraft

### Deneb
- **OS:** Ubuntu LTS
- **Tailscale IP:** 100.81.57.104
- **Role:** AI services
- **Compose files:** `/srv/appdata/<service>/docker-compose.yml` (in progress — 
  being consolidated from mixed locations during aeoncore setup)
- **Services:** Ollama, Open WebUI, ComfyUI, n8n, Beszel Agent

### Vega
- **OS:** TrueNAS Scale
- **Tailscale IP:** 100.102.180.38
- **Role:** Storage and file services
- **Shares:** SMB and NFS shares for LAN access
- **Apps:** Nextcloud (managed as TrueNAS app)
- **Notes:** Largely hands-off. Not managed via Docker Compose.

---

## Stack Management

| Tool | Purpose |
|------|---------|
| Docker Compose | Service definition and deployment |
| Dockge | Compose stack UI (sirius.aeoncore.net:5001) |
| Nginx Proxy Manager | Reverse proxy and SSL (Let's Encrypt) |
| Tailscale | Network access and auth layer |
| Kopia | Backup management |
| Beszel | Cross-host monitoring |
| GitHub (pythaeon/aeoncore) | Source of truth for all compose files and docs |

---

## Repository Structure
```
aeoncore/
├── sirius/
│   └── <service>/
│       ├── docker-compose.yml
│       ├── .env.example
│       └── README.md
├── deneb/
│   └── <service>/
│       ├── docker-compose.yml
│       ├── .env.example
│       └── README.md
└── docs/
    ├── service-map.md
    ├── infrastructure.md
    └── <service-specific notes>
```

---

## Naming Conventions

- **Servers** are named after stars: Sirius, Deneb, Vega
- **Personal computers** are named after spacecraft: Discovery (primary Windows desktop)
- **Domains** follow the pattern `<service>.aeoncore.net`
- **Container names** match the service name (e.g. `pihole`, `homepage`, `dockge`)

---

## Open Items

See `service-map.md` for current open items.