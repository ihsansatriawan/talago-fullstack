# 0006: Mock Data Sources for v1

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

Note [0002](./0002-estate-assistant-open-questions.md) asked whether v1 uses mock data or the real house rules.

## Decision

v1 uses:

- Sample documents labelled `MOCK DATA`, written by the product owner: payment rates and complex rules.
- The "Recap" and "Transaksi" sheets, with resident names anonymized.

The real rules replace them after the data pipeline runs.

## Consequences

- The data is not in the repo yet; the product owner will provide it. Instructions, context, and evals are replaced once it arrives ([0001](./0001-estate-assistant-direction.md)).
- Context files keep the `MOCK DATA` label.
- How the sheets reach the agent, as static context or through a lookup tool, is open; see note 0002.
