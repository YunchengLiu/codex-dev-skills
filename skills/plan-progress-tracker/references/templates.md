# Workpack Doc Templates

Use these templates as defaults. Keep headings stable so future agents can diff and update safely.

Template usage rules:

- Delete any section that would be empty or speculative; do not keep placeholder sections for completeness.
- Init mode should be skeletal: prefer `TBD` + 1-3 concrete questions over invented module boundaries/interfaces.
- Start new modules as stubs/thin docs; promote to the full module template only when interfaces/behavior are real or required.
- Write for agents (execution-oriented): bullet-first, concrete nouns, checkable statements, stable terms/IDs; avoid narrative filler.

## Contents

- `INDEX.md`
- `OVERVIEW.md`
- `modules/<module>.md` (full)
- `modules/<module>.md` (thin, early-stage)
- `PLAN.md`
- `STATUS.md`
- `DECISIONS.md`

## `INDEX.md`

```md
# <Workpack Name>

Workpack ID: <folder-name>
Workpack root: <absolute path>

Last updated: <YYYY-MM-DD HH:MM TZ>

## Start Here

- Read: `STATUS.md` (Now/Next/Blockers)
- Then: `OVERVIEW.md` (background + module map)

## Documents

- `OVERVIEW.md` - Top-down spec and module map
- `PLAN.md` - Milestones and task list
- `STATUS.md` - Handoff-focused progress
- `DECISIONS.md` - Append-only decision log
- `modules/` - Per-module detailed specs

## Modules

- `modules/<ModuleA>.md`
- `modules/<ModuleB>.md`

## Current Links

- Repo: <path or URL if available>
- Tracking: <issues/PRs/etc>

## Invariants (single source of truth)

- `PLAN.md` is the only task inventory. Add/change tasks there, then reference IDs elsewhere.
- `STATUS.md` is a session snapshot. Do not turn it into a second plan.
- `DECISIONS.md` is append-only for real decisions (constraints/behavior/interfaces or preventing repeated debate).
- `OVERVIEW.md` stays high-level; concrete interfaces live in `modules/*.md`.
- New modules start as stubs; promote to full only when needed.
```

## `OVERVIEW.md`

````md
# Overview: <Workpack Name>

Last updated: <YYYY-MM-DD HH:MM TZ>

## Background

<One screen: what problem, for whom, why now>

## Goals

- <Goal 1>
- <Goal 2>

## Constraints and Assumptions

- <Constraint/assumption>

## Deliverables, Acceptance Criteria, and DoD

- Deliverables:
  - <What artifacts/features must exist>
- Acceptance criteria:
  - <observable pass/fail checks>
- Definition of Done (DoD):
  - `<What must be true to call it done>`
- Stop conditions:
  - `<When to stop expanding scope>`

## Module Map

Concrete interfaces live in `modules/*.md`. `OVERVIEW.md` describes responsibilities and interactions at a high level.

Modules:

- `<ModuleA>`: `<one-line responsibility>` (see `modules/<ModuleA>.md`)
- `<ModuleB>`: `<one-line responsibility>` (see `modules/<ModuleB>.md`)

Interactions (high level):

```mermaid
flowchart LR
  A["<ModuleA>"] --> B["<ModuleB>"]
```

## Execution Order

1. `<First build... why it unlocks others>`
1. `<Next...>`

## Risks and Validation

- `<Risk>`: `<mitigation>`
- Validation:
  - `<how to test/verify at a high level>`

## Open Questions

- [ ] `<TBD>`

## References

- `<repo paths, PRs, docs>`

````

## `modules/<module>.md`

```md
# Module: <Module Name>

Last updated: <YYYY-MM-DD HH:MM TZ>

## Purpose

<One paragraph>

## Responsibilities (In Scope)

- <positive responsibilities>

## Interfaces

- Inputs:
  - <API/event/function>
- Outputs:
  - <API/event/function>

## Dependencies

- Upstream: <Module(s)>
- Downstream: <Module(s)>

## Data and State

- <schemas/state, persistence>

## Main Flows

1. <step>
2. <step>

## Edge Cases and Errors

- <case> -> <behavior>

## DoD (Module Level)

- <tests, observable behavior>

## Open Questions

- [ ] <TBD>

## References

- <repo paths, PRs, docs>
```

## `modules/<module>.md` (thin, early-stage)

```md
# Module: <Module Name>

Last updated: <YYYY-MM-DD HH:MM TZ>

Stub status: <what is missing / what is still TBD>

## Purpose

<One paragraph>

## Responsibilities (In Scope)

- <positive responsibilities>

## Interfaces (minimal)

- <one-line input/output or link to code>

## Open Questions

- [ ] <TBD>
```

## `PLAN.md`

```md
# Plan: <Workpack Name>

Last updated: <YYYY-MM-DD HH:MM TZ>

Invariant: this is the only task inventory. Keep task IDs stable.

## Milestones

- M0: <definition>
- M1: <definition>

## Task List

| ID | Status | Area | Task | Owner | Links |
|---:|:------:|:-----|:-----|:------|:------|
| T001 | TODO | <Module/Area> | <Task> | <agent/human> | <PR/issue/path> |

Notes:
- Keep task IDs stable; do not renumber.
- Prefer updating `Status` over deleting rows.
- Suggested status vocabulary: `TODO`, `IN_PROGRESS`, `BLOCKED`, `DONE`, `CANCELLED`.
```

## `STATUS.md`

```md
# Status: <Workpack Name>

Last updated: <YYYY-MM-DD HH:MM TZ>

Invariant: session snapshot only. Add/change tasks in `PLAN.md`, then reference task IDs here.

## Handoff

- Now: <current state in 2-5 lines>
- Next:
  - <prefer referencing PLAN task IDs, e.g. T001: ...>
  - <T002: ...>
- Blockers:
  - <blocker or "None">
- Links:
  - <most relevant doc/PR/path>

## Notes (optional)

- <recent changes, context, quick logs>
```

## `DECISIONS.md`

```md
# Decisions: <Workpack Name>

Append-only log. If a decision changes, add a new entry that supersedes the old one.

Invariant: log decisions that change constraints/behavior/interfaces or prevent repeated debate; do not use as a general changelog.

## D001 YYYY-MM-DD: <Decision Title>

- Decision: <what we decided>
- Context: <what forced the decision>
- Rationale: <why>
- Supersedes: <D000 or "None">
- Consequences: <what changes, what becomes easier/harder>
- Links: <OVERVIEW section, module doc, PR/issue>
```
