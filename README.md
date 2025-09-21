# Docker + Traefik + Authentik (Sample Stack)

This sample shows how to run a production-style reverse proxy (**Traefik**) with **Authentik** for SSO, plus example apps (**Paperless-ngx** and a placeholder for Mediastack).

## Quick Start
1. Copy `.env.example` to `.env` and set strong secrets and your domain.
2. Create the ACME storage file for Traefik:
   ```bash
   mkdir -p traefik/letsencrypt && touch traefik/letsencrypt/acme.json
   chmod 600 traefik/letsencrypt/acme.json
   ```
3. Launch:
   ```bash
   docker compose up -d
   ```
4. Visit:
   - Traefik Dashboard: `https://traefik.${DOMAIN}`
   - Authentik: `https://sso.${DOMAIN}`
   - Paperless-ngx: `https://docs.${DOMAIN}` (can be protected with Authentik forward auth)
   - Mediastack placeholder: `https://media.${DOMAIN}`

> Notes:
> - Replace images and environment variables for Mediastack with your actual app.
> - Do not commit real secrets. Keep `.env` private.
