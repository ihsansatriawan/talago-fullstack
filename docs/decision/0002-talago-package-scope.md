# 0002: `@talago` Package Scope and Names

**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

The workspace packages and other app-owned identifiers carried the `anvia` name from the source repository. Talago needs its own names so the two apps stay distinguishable in imports, traces, and local Docker resources.

## Decision

Use `@talago/<name>` for workspace packages: `@talago/api`, `@talago/web`, `@talago/db`, and `@talago/agents`. The root package is `talago-fullstack`.

Other app-owned names also use `talago`:

- Agent id `talago-assistant` (`packages/agents/src/agent.ts`).
- Lens service name `talago-hr-agent` (`packages/agents/src/lens.ts`).
- API health name `talago-api` (`apps/api/src/index.ts`).
- Docker Compose project `talago-dev`, with Postgres user, password, and database `talago` (`docker-compose.yaml`).

## Consequences

- Imports, `pnpm --filter` commands, `workspace:*` dependencies, and the lockfile use the `@talago` scope.
- Framework packages keep the `@anvia` scope ([0001](./0001-anvia-framework-dependency.md)).
- The Lens service name still says `hr`; product decision [0001](../product/0001-estate-assistant-direction.md) lists it with the other HR leftovers.
