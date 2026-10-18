# 0003: Keep `ANVIA_LENS_*` Env Names

**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

`packages/agents/src/lens.ts` reads the Lens tracing credentials from environment variables whose names came from the source repository. Lens is an Anvia product ([0001](./0001-anvia-framework-dependency.md)), not part of the Talago brand.

## Decision

Keep `ANVIA_LENS_BASE_URL`, `ANVIA_LENS_PUBLIC_KEY`, and `ANVIA_LENS_SECRET_KEY` as the variable names.

## Consequences

- The names describe the service they configure, and the same Lens values work for both `anvia-fullstack-app` and Talago.
- `lens.ts` and the root `.env` must use the same names. Renaming them later needs a new record that supersedes this one.
