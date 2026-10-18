# 0003: Residents Only for v1

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

Note [0002](./0002-estate-assistant-open-questions.md) asked who uses the assistant. Kompleks Dtalago has residents (warga) and a management team (pengelola).

## Decision

- v1 serves residents only. The chat is for warga.
- The management does not chat with the assistant. It approves actions and reads a daily summary.
- The assistant's tone is friendly and polite (ramah dan sopan).
- The assistant answers only from the provided documents and data.

## Consequences

- `packages/agents/src/instructions.ts` is rewritten for residents, in this tone, with the documents as the only source.
- The management approval flow and the daily summary do not exist in the app yet; see note 0002.
- The agent's web search tools (`search_web`, `read_webpage`) conflict with answering only from documents; see note 0002.
