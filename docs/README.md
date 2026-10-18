# Docs

Records of durable choices and their history. [`decision/`](./decision/) holds architecture and repository decisions; [`product/`](./product/) holds product decisions and notes. Each folder numbers its records separately.

## Decision records

Record choices that affect the repository over time: package boundaries, frameworks, code organization, shared tooling, infrastructure, ports, environment variables, and security settings. Routine implementation details need no record.

### Status

- `Accepted`: the decision is active.
- `Superseded`: a later record replaces it. Link to the new record; the new record names the old one under **Supersedes**.
- `Deprecated`: no longer recommended and has no direct replacement. Explain the migration or removal plan when one exists.

### Rules

- Name files with the next four-digit number and a short kebab-case title: `0005-short-title.md`. Never reuse a number, including for a deprecated record.
- Keep each record to one decision: its context, the decision, and its consequences. Include the relevant paths and commands so agents can connect the record to the code.
- Write the record close to the code change that implements it. Call out security and operational tradeoffs explicitly.
- Accepted records are history. When a decision changes, write a new record and mark the old one `Superseded`; leave the old decision text as it was.
- Update the index below whenever a record is added or its status changes.

### Template

```markdown
# NNNN: Decision title

**Status:** Accepted
**Date:** YYYY-MM-DD
**Supersedes:** None

## Context

Why this decision is needed.

## Decision

What the repository will do.

## Consequences

Effects, tradeoffs, and follow-up work.
```

### Index

| ID                                                       | Decision                         | Status   |
| -------------------------------------------------------- | -------------------------------- | -------- |
| [0001](./decision/0001-anvia-framework-dependency.md)    | Anvia framework stays a dependency | Accepted |
| [0002](./decision/0002-talago-package-scope.md)          | `@talago` package scope and names | Accepted |
| [0003](./decision/0003-keep-anvia-lens-env-names.md)     | Keep `ANVIA_LENS_*` env names    | Accepted |
| [0004](./decision/0004-dev-ports-alongside-anvia.md)     | Dev ports beside Anvia           | Accepted |

## Product records

Product records capture what Talago is for and how it should behave for its users. Each record sets its **Type**:

- `Decision`: a product choice, such as audience, scope, behavior, or wording. It uses the same statuses, naming, and history rules as decision records.
- `Note`: working material, such as context, findings, and open questions. A note has no status and may be updated in place. When a note's question is answered, record the outcome as a product decision and link it from the note.

### Templates

```markdown
# NNNN: Product decision title

**Type:** Decision
**Status:** Accepted
**Date:** YYYY-MM-DD
**Supersedes:** None

## Context

Who is affected and why the choice is needed.

## Decision

What the product will do.

## Consequences

What changes in the app, and what follow-up work remains.
```

```markdown
# NNNN: Note title

**Type:** Note
**Date:** YYYY-MM-DD

What was learned, observed, or still needs an answer. Link the related decisions.
```

### Index

| ID                                                          | Record                           | Type     | Status   |
| ----------------------------------------------------------- | -------------------------------- | -------- | -------- |
| [0001](./product/0001-estate-assistant-direction.md)        | Estate assistant for Kompleks Dtalago | Decision | Accepted |
| [0002](./product/0002-estate-assistant-open-questions.md)   | Estate assistant open questions  | Note     | —        |
