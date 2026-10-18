# 0007: Five Topics and Eval Suites

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

Note [0002](./0002-estate-assistant-open-questions.md) proposed four topics, one per eval suite, to replace working time, leave, payroll, and benefits.

## Decision

The assistant covers five topics, each with its own eval suite:

1. IPL and payments: rates, late fees (denda), how to pay, and unit payment status.
2. Security, guests, and parking.
3. Facilities and cleanliness: opening hours, the hall (aula), and waste.
4. Renovation and complaints.
5. Emergencies and escalation: the assistant hands the resident to a human right away.

## Consequences

- Five eval suites replace the four HR suites in `packages/agents/src/evals/`, with `evals:1` to `evals:5` scripts in the root `package.json`.
- The emergency suite checks that the assistant points to a human contact immediately rather than handling the emergency itself. It needs those contacts from the mock documents.
- Unit payment status depends on knowing the asker's unit ([0004](./0004-resident-privacy.md)).
