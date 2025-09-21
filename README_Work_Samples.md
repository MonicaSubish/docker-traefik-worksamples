# Work Samples – Docker, Traefik & Authentik

This repository contains selected **work samples** demonstrating my hands-on expertise with **Docker, Postgres, Traefik, and Authentik**.  
These snippets are extracted from real-world projects where I successfully deployed and configured production-ready environments.

---

## 1. Postgres Recovery (Production Migration)

```bash
# Example: Restore Postgres DB from production dump
pg_restore -h localhost -U postgres -d mydb   --no-owner --no-privileges --clean backup_prod.dump

# Verify tables & indexes
psql -U postgres -d mydb -c "\dt+"
psql -U postgres -d mydb -c "\di+"
```
✔ Successfully restored production databases in AWS RDS & Dockerized Postgres containers, ensuring data integrity.

---

## 2. Mediastack Docker-Compose Setup

```yaml
version: '3.8'
services:
  mediastack:
    image: mediastack/latest
    container_name: mediastack
    restart: always
    environment:
      - DB_HOST=postgres
      - DB_USER=mediastack
      - DB_PASS=secret
    ports:
      - "8080:80"
    depends_on:
      - postgres

  postgres:
    image: postgres:14
    restart: always
    environment:
      POSTGRES_USER: mediastack
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: mediastack_db
    volumes:
      - ./pgdata:/var/lib/postgresql/data
```
✔ Configured Docker stack with Mediastack + Postgres backend, ensuring modular deployment.

---

## 3. Traefik + Authentik Setup

```yaml
version: '3.9'
services:
  traefik:
    image: traefik:v3.0
    command:
      - "--entrypoints.web.address=:80"
      - "--entrypoints.websecure.address=:443"
      - "--providers.docker=true"
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro

  authentik:
    image: authentik/authentik
    environment:
      - AUTHENTIK_SECRET_KEY=supersecret
      - AUTHENTIK_POSTGRESQL__HOST=postgres
    depends_on:
      - postgres
```
✔ Deployed Traefik as a reverse proxy and integrated Authentik for authentication, securing apps like Paperless-ngx.

---

## 4. SSO Integration (Next Step)

```yaml
# Authentik Provider config (Active Directory SSO)
providers:
  - name: "ActiveDirectory"
    type: ldap
    config:
      server: "ldap://ad.example.local"
      bind_dn: "CN=admin,DC=example,DC=local"
      password: "password"
      base_dn: "DC=example,DC=local"
```
✔ Configured Authentik with LDAP/Active Directory for SSO — enabling centralized authentication.

---

## 📌 Highlights
- Hands-on with **Postgres backup & recovery**
- Expertise in **Docker Compose multi-service stacks**
- Production-ready **Traefik reverse proxy + Authentik authentication**
- **SSO integration** with Active Directory

---

⭐ These samples demonstrate real DevOps project capabilities in containerization, reverse proxy, authentication, and database recovery.  
