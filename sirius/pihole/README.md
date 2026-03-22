# Pihole

DNS server and network-wide ad blocker.

## Access

- **Admin UI:** pihole.aeoncore.net
- **Internal port:** 8081

## Notes

- DNS upstream providers: Cloudflare (1.1.1.1 / 1.0.0.1)
- Handles DNS for all LAN devices
- Port 53 must remain available on Sirius — do not run another DNS service alongside it

## Volumes

| Host path | Container path | Purpose |
|-----------|---------------|---------|
| /srv/appdata/pihole/etc-pihole | /etc/pihole | Pihole config and database |
| /srv/appdata/pihole/etc-dnsmasq.d | /etc/dnsmasq.d | DNS config |

## Environment Variables

See `.env.example` for required variables.
```

---

Once those three files are in, we also need to create `sirius/pihole/.gitignore` to make sure the actual `.env` file never gets committed:
```
.env