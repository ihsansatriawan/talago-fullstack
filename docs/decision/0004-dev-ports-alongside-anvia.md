# 0004: Dev Ports Beside Anvia

**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

`anvia-fullstack-app` and Talago run on the same machine. With identical ports they clashed: Postgres on 5433, the API on 3000, and web on 5173. The web dev proxy also pointed at `localhost:3000`, so Talago's web app would quietly call Anvia's API. When a host port is taken, Docker Desktop still reports the container as `Started` but runs it without the port.

## Decision

Talago uses its own dev ports. Anvia keeps 5433, 3000, and 5173.

| Service  | Port | Set in                                                                   |
| -------- | ---- | ------------------------------------------------------------------------ |
| Postgres | 5434 | `docker-compose.yaml` (`"5434:5432"`), `DATABASE_URL` in root `.env`     |
| API      | 3001 | `PORT` in root `.env`, fallback in `apps/api/src/index.ts`               |
| Web      | 5174 | `server.port` and the `/api` proxy target in `apps/web/vite.config.ts`   |

## Consequences

- Both stacks can run at the same time.
- Changing a port means updating every place listed for it; the API port appears in three places, including the web proxy target.
- After `docker compose up -d --pull never`, confirm that `docker ps` shows `5434->5432`.
