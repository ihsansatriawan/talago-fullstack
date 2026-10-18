# 0005: Landed Housing Context

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

Note [0002](./0002-estate-assistant-open-questions.md) asked what kind of complex Kompleks Dtalago is, which decides the rules that replace the labor-law context.

## Decision

- Kompleks Dtalago is D'talago Regency, a landed housing estate (perumahan tapak) with six blocks, A to F.
- For the MVP, the rule basis is the internal paguyuban rules.
- Rumah susun rules, including PPPSRS, do not apply.
- UU 1/2011 on housing and settlements (perumahan dan kawasan permukiman) is the legal basis to verify later.

## Consequences

- The labor-law context (`packages/agents/src/context/indonesia-labor-rules.ts`) is replaced by the paguyuban rules. The MVP needs no national regulation document.
- Answers cite the paguyuban rules, not national law.
