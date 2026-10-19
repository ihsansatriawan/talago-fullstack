# Talago

Talago Estate Assistant — an assistant for managing Kompleks Dtalago. It provides chat with saved sessions, answers grounded in context documents, web search, Lens tracing, and eval suites. It runs on the [Anvia](https://www.npmjs.com/org/anvia) fullstack framework.

Product direction and scope live in [`docs/product/`](docs/product/); architecture and repository decisions live in [`docs/decision/`](docs/decision/). Start with [`docs/README.md`](docs/README.md) for the record index.

## Requirements

- Node 22 or newer (pnpm fails on Node 20 with a `node:sqlite` error)
- pnpm
- Docker (Postgres only)

## Workspace layout

| Package                                                    | What it is                                                                     |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [`apps/web`](apps/web) (`@talago/web`)                     | React UI: Vite, TanStack Router, Tailwind CSS, `@anvia/react-ui`                |
| [`apps/api`](apps/api) (`@talago/api`)                     | Hono API on `@anvia/server`, serves the agent                                  |
| [`packages/db`](packages/db) (`@talago/db`)                | Prisma 8 schema and migrations on Postgres                                     |
| [`packages/agents`](packages/agents) (`@talago/agents`)    | Agent definition, context documents, tools, and eval suites                    |

Framework dependencies keep the `@anvia/*` scope; app-owned identifiers use `talago` (decisions [0001](docs/decision/0001-anvia-framework-dependency.md) and [0002](docs/decision/0002-talago-package-scope.md)).

## Getting started

1. Install dependencies:

   ```sh
   pnpm install
   ```

2. Start Postgres:

   ```sh
   docker compose up -d --pull never
   ```

   Then confirm `docker ps` shows `5434->5432`. When the host port is taken, Docker Desktop still reports `Started` but runs the container without it.

3. Create a root `.env` (gitignored) with:

   ```sh
   DATABASE_URL=postgresql://talago:talago@localhost:5434/talago
   OPENROUTER_API_KEY=...
   TAVILY_API_KEY=...
   ANVIA_LENS_BASE_URL=...
   ANVIA_LENS_PUBLIC_KEY=...
   ANVIA_LENS_SECRET_KEY=...
   ```

4. Initialize a fresh database:

   ```sh
   pnpm --filter @talago/db db:init
   ```

5. Run the API and web app:

   ```sh
   pnpm dev:api
   pnpm dev:web
   ```

   The web app is at http://localhost:5174.

`driver not connected` from `pnpm dev:api` means `DATABASE_URL` is empty: the root `.env` is missing.

## Ports

Talago uses the following dev ports (decision [0004](docs/decision/0004-dev-ports-alongside-anvia.md)):

| Service  | Port |
| -------- | ---- |
| Postgres | 5434 |
| API      | 3001 |
| Web      | 5174 |

## Scripts

| Script          | What it runs                              |
| --------------- | ----------------------------------------- |
| `pnpm dev:api`  | API dev server                            |
| `pnpm dev:web`  | Web dev server                            |
| `pnpm build`    | Build every workspace package             |
| `pnpm typecheck`| Typecheck every workspace package          |
| `pnpm evals`    | All eval suites (`evals:1` … `evals:4` run one) |

`pnpm evals` calls the LLM and Lens and costs money. Run it, or a single `evals:N`, only when agent instructions, context documents, tools, or the model change.

## Environment variables

| Variable                   | Used by                                            |
| -------------------------- | -------------------------------------------------- |
| `DATABASE_URL`             | `@talago/db` — Postgres connection                 |
| `PORT`                     | `@talago/api` — defaults to 3001                  |
| `OPENROUTER_API_KEY`       | `@talago/agents` — model calls                    |
| `TAVILY_API_KEY`           | `@talago/agents` — web search tool                |
| `ANVIA_LENS_BASE_URL`      | `@talago/agents` — Lens tracing (decision [0003](docs/decision/0003-keep-anvia-lens-env-names.md)) |
| `ANVIA_LENS_PUBLIC_KEY`    | `@talago/agents` — Lens tracing                   |
| `ANVIA_LENS_SECRET_KEY`    | `@talago/agents` — Lens tracing                   |

Local values live in the gitignored root `.env`; keep secrets out of source, logs, and commits.
