# Agent Working Agreement

This file describes how agents should work in this repository. It is about work process and constraints; durable repository and product choices live in [`docs/`](docs/README.md).

## Before changing files

- Read the related records in [`docs/decision/`](docs/decision/) and [`docs/product/`](docs/product/) before making a change. Product records say what Talago is for and which content is still pending.
- Inspect the existing implementation and nearby conventions first. Prefer extending what is already there over introducing a second pattern.
- Identify the smallest set of files needed to satisfy the request. Keep unrelated cleanup, renames, formatting, and dependency upgrades out of the change.
- Treat the user's latest instruction as the scope. Preserve existing user changes and do not overwrite work unrelated to the task.
- If requirements are incomplete, make progress on independent parts and ask only for information that blocks a consequential choice.

## Constraints

- Most "Anvia" in this repo is the framework, not the app brand: `@anvia/*` packages, Anvia Lens images, `--anvia-*` CSS variables, the Prisma `ANVIA MEMORY` markers, and the `ANVIA_LENS_*` env vars stay as they are. App-owned names use `talago` and `@talago/*`. See decisions 0001–0003.
- Do not invent product behavior, policies, amounts, API contracts, environment variables, or architectural decisions. Mark unknowns clearly or ask when they block implementation. Label fictional context data `MOCK DATA`, as the existing context files do.
- Agent instructions (`packages/agents/src/instructions.ts`), context documents (`packages/agents/src/context/`), and eval suites (`packages/agents/src/evals/`) change together: evals assert facts and numbers taken from the context documents.
- Do not add dependencies when existing workspace packages or platform APIs are sufficient. When a dependency is needed, add it to the package that uses it and update the pnpm lockfile through pnpm.
- Do not weaken supply-chain, environment, secret-handling, or other security settings to make a command pass. Explain a blocked check and its cause.
- Keep secrets out of source, logs, and commits. Local values live in the gitignored root `.env`.
- Do not commit, push, publish, deploy, or contact external people or services unless the user explicitly asks for that action.
- Do not add documentation that merely repeats existing rules. Record a decision in `docs/decision/` or `docs/product/` only when a real decision is made; follow [`docs/README.md`](docs/README.md) for numbering, status, and history.

## Local environment

- Use Node 22 or newer; pnpm fails on Node 20 with a `node:sqlite` error.
- Talago runs beside `anvia-fullstack-app` on Postgres 5434, API 3001, and web 5174 (decision 0004). A fresh database needs `docker compose up -d --pull never`, then `pnpm --filter @talago/db db:init`.
- After `docker compose up`, check that `docker ps` shows the host port. When the port is taken, Docker Desktop still reports `Started` but runs the container without it.
- `driver not connected` from `pnpm dev:api` means `DATABASE_URL` is empty: the root `.env` is missing.

## Implementation workflow

1. Read the request and identify its expected result and boundaries.
2. Inspect relevant files, scripts, and docs records before editing.
3. Make the smallest complete change that satisfies the request.
4. Review the diff or changed files for accidental scope expansion, stale references, and consistency with repository records.
5. Run the narrowest useful verification: `pnpm typecheck`, `pnpm build`, or the affected package's script. The repo has no test or lint setup. `pnpm evals` calls the LLM and Lens and costs money; run it, or a single `evals:N`, when agent instructions, context, tools, or the model change.
6. If verification cannot run, report the exact blocker. Do not claim it passed.

## Finishing a task

In the final response, summarize what changed, link the important files, and state what verification ran and its result. Mention material limitations or unresolved decisions plainly. Keep the report concise and do not claim work that was not completed.

## Pull request deliverables

When asked to create a pull request:

- Review the complete proposed diff before opening the PR. Check for correctness, regressions, security issues, missing error handling, and consistency with repository records. Fix findings and review the updated diff again. Do not open the PR while known blocking findings remain; report any finding that cannot be resolved.
- For UI changes, run the app (`pnpm dev:api` and `pnpm dev:web`, then http://localhost:5174) and use a headless browser to capture representative screenshots. Capture a short video as well when the change involves an interaction, animation, or flow that a still image cannot demonstrate. Inspect the captures to confirm they show the implemented result and contain no secrets or unintended personal data.
- Record short videos at normal human interaction speed: pace clicks, typing, and scrolling naturally, and pause long enough for reviewers to read each relevant screen and see the result of each action. Keep playback at 1× speed. Watch the video before attaching it to confirm the flow is easy to follow.
- Attach the resulting image or video evidence to the PR description so reviewers can see it without accessing local files. Do not treat a local artifact path as an attachment.
- If the app cannot run, browser capture fails, or evidence cannot be attached, explain the blocker and do not claim the PR deliverables are complete.
