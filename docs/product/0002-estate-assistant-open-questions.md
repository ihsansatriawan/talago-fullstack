# 0002: Estate Assistant Open Questions

**Type:** Note
**Date:** 2026-10-18

These questions block replacing the HR content listed in product decision [0001](./0001-estate-assistant-direction.md). Record each answer as a product decision and link it here.

## Answered

1. **Users.** Residents only for v1; the management approves actions and reads a daily summary. See [0003](./0003-residents-only-v1.md) and [0004](./0004-resident-privacy.md).
2. **Complex type.** Landed housing, D'talago Regency, blocks A to F, under the internal paguyuban rules. See [0005](./0005-landed-housing-context.md).
3. **Data source.** `MOCK DATA` documents plus anonymized "Recap" and "Transaksi" sheets, provided later. See [0006](./0006-mock-data-sources.md).
4. **Topics.** The four proposed topics plus emergencies and escalation. See [0007](./0007-five-topics.md).

## Open

1. **Unit identity.** The app has no login. To answer unit payment status without showing another unit's data ([0004](./0004-resident-privacy.md)), the assistant must know which unit the asker owns. Options: a resident login bound to a unit, a per-unit access link or code, or leaving unit status out of v1.
2. **Management approvals and daily summary.** Neither exists in the app ([0003](./0003-residents-only-v1.md)). Which actions need approval (for example renovation permits, hall bookings, or complaints), where the daily summary appears, and whether either is part of v1.
3. **Web search.** Answering only from documents ([0003](./0003-residents-only-v1.md)) conflicts with the agent's `search_web` and `read_webpage` tools. Remove them from the agent, or keep them for a narrow case?
4. **Sheet access.** As static context, the model receives every unit's payment data and only the prompt keeps it private. A lookup tool that returns only the asker's unit enforces [0004](./0004-resident-privacy.md) in code. This depends on question 1.
