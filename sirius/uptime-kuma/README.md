# Uptime Kuma

Self-hosted service monitoring and uptime tracking with alerting.

## Access

- **UI:** uptime-kuma.aeoncore.net
- **Internal port:** 3001

## Notes

- No environment variables required for basic operation
- Monitors are configured entirely through the web UI
- Alert configuration (email, Telegram, etc.) is done through the UI
- Originally installed via CasaOS — recreated as a clean compose stack
  during aeoncore setup

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /srv/appdata/uptime-kuma/data | /app/data | Database and config |
```

`sirius/uptime-kuma/.gitignore`:
```
.env