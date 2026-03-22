# Nginx Proxy Manager

Reverse proxy handling all *.aeoncore.net subdomain routing and 
Let's Encrypt SSL certificate management.

## Access

- **Admin UI:** npm.aeoncore.net
- **Internal port:** 81

## Notes

- All aeoncore services are routed through NPM via their Tailscale IPs
- SSL certificates are issued via Let's Encrypt
- Ports 80 and 443 must remain available on Sirius
- NPM is a critical dependency — if it goes down, all *.aeoncore.net 
  domains become unreachable (services still accessible via IP:port)

## Volumes

| Host path | Container path | Purpose |
|-----------|----------------|---------|
| /srv/appdata/nginx-proxy-manager/data | /data | NPM database and config |
| /srv/appdata/nginx-proxy-manager/letsencrypt | /etc/letsencrypt | SSL certificates |
```

`sirius/nginx-proxy-manager/.gitignore`:
```
.env