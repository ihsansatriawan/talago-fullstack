# 0001: Estate Assistant for Kompleks Dtalago

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

The app was copied from an HR assistant for PT Maju Jaya Sakti, a fictional company. Talago serves a different purpose: managing Kompleks Dtalago (pengelolaan Kompleks Dtalago).

## Decision

Talago is an assistant for managing Kompleks Dtalago. Its name in the UI is "Talago Estate Assistant".

The features stay the same as the HR version: chat with saved sessions, answers grounded in context documents, web search, Lens tracing, and eval suites. Only the content changes.

## Consequences

Done:

- UI header renamed in `apps/web/src/routes/index.tsx` and `apps/web/src/routes/s.$id.tsx`.

Still HR content, to be replaced:

- Role, sources, rules, and HR contact in `packages/agents/src/instructions.ts`.
- Context documents in `packages/agents/src/context/company-policies.ts` and `indonesia-labor-rules.ts`.
- The four eval suites in `packages/agents/src/evals/` and the `evals:*` scripts in the root `package.json`.
- Composer placeholder "Ask about leave, payroll, BPJS..." in both routes.
- Lens service name `talago-hr-agent` in `packages/agents/src/lens.ts`.

Instructions, context, and evals must be replaced together. The open questions that block this are in note [0002](./0002-estate-assistant-open-questions.md).
