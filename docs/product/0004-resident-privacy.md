# 0004: Resident Privacy

**Type:** Decision
**Status:** Accepted
**Date:** 2026-10-18
**Supersedes:** None

## Context

The payment data ([0006](./0006-mock-data-sources.md)) covers every unit in the complex. A resident asking about payments must not learn about other households.

## Decision

The assistant never shows another unit's data, and never shows a resident's email address or WhatsApp number.

## Consequences

- Payment status answers cover only the asker's own unit. The app has no login, so it cannot yet tell which unit the asker owns; see note [0002](./0002-estate-assistant-open-questions.md).
- The eval suites include cases that ask for another unit's data, an email address, or a WhatsApp number, and expect a refusal.
