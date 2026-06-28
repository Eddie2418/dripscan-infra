# Dripscan: Infrastructure

I built Dripscan as a real e-commerce marketplace not a tutorial, an actual live thing with real customers. This repo is the infrastructure that runs it, cleaned up so you can see exactly how it's wired without me leaking my passwords to the internet.

Every password, key, and domain has been swapped for a placeholder. The architecture is fully visible; nothing sensitive is exposed.

Built and operated by me on a self managed VPS.

## What this demonstrates

Containerised, multi-service architecture with Docker Compose
A reverse proxy (Traefik) handling routing and HTTPS
Managed Postgres, Redis caching, and workflow automation (n8n)
Secrets management config externalised to environment variables
Production hygiene `.gitignore` discipline, no credentials in source

## Architecture

The stack runs five containers behind a single reverse proxy:

**Traefik**  : reverse proxy; terminates TLS, routes traffic to services
**Medusa** : headless commerce backend (the marketplace itself)
**Postgres** : primary database
**Redis** : caching layer
**n8n**  : self hosted workflow automation

A request hits Traefik over HTTPS, then gets routed by hostname to the right container across the internal Docker network.

## Security note

This is a deliberately sanitised repo. All real values passwords, API
keys, domains live in a `.env` file that is **never** committed (see
`.gitignore`). 

What you see here is the structure, not the secrets.

`.env.example` documents every variable the stack expects, with safe
placeholder values.

## Running it

1. Clone the repo
2. Copy `.env.example` to `.env` and fill in real values
3. `docker compose up -d`

## Notes

Five containers, one reverse proxy, zero tutorials  I broke it, fixed it, and learned what every line does the hard way. The full build-and-operate story is documented separately.

