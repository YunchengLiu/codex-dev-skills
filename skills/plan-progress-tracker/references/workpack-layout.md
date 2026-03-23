# Workpack Layout and Responsibilities

## Default layout

```
<workpack-root>/
  INDEX.md
  OVERVIEW.md
  PLAN.md
  STATUS.md
  DECISIONS.md
  modules/
    <module>.md
```

`INDEX.md`

- Purpose: Entry point and stable anchor for future chats/agents.
- Must include: links to all docs, last-updated time, and "where to start".
- Should include: short "maintenance rules" so new agents know how to update without creating conflicts.

`OVERVIEW.md`

- Purpose: Top-down truth.
- Owns: background, goals, constraints/assumptions, module map + interactions, execution order, acceptance criteria.
- Must not: duplicate detailed interfaces already specified in module docs (link instead).

`modules/<module>.md`

- Purpose: Detailed spec for one module.
- Owns: responsibilities, interfaces, dependencies, data/state, flows, edge cases, module-level DoD.
- Must be consistent with: module names and interactions described in `OVERVIEW.md`.

`PLAN.md`

- Purpose: Planned work (milestones + tasks) with stable IDs and links.
- Update when: scope/tasks/milestones change.
- Must remain compatible with: `OVERVIEW.md` execution order and module inventory.

`STATUS.md`

- Purpose: "state of the world" for handoff.
- Update when: any meaningful state changes (at least once per working session).
- Must start with: a fixed-format handoff block (Now/Next/Blockers/Links).
- Must not: become a second task inventory. When tasks exist in `PLAN.md`, `STATUS.Next` should reference task IDs.

`DECISIONS.md`

- Purpose: Decision log to prevent design drift and repeated debates.
- Append-only: never rewrite history; add a new entry to supersede older decisions.
- Link decisions to: the affected overview/module sections and any relevant PRs/issues.

## Conflict-avoidance rules (single source of truth)

- Keep the canonical definition of a module's responsibilities in `modules/<module>.md`.
- Keep the canonical module map and interaction story in `OVERVIEW.md` (link to module docs for detail).
- Avoid copy-pasting the same interface definition across multiple files; choose one owner and link.
- Prefer updating canonical docs in place. Avoid creating parallel `*-v2.md` spec files unless explicitly requested.
- Keep open questions owned: cross-cutting questions in `OVERVIEW.md`; module-local questions in the relevant module doc; `STATUS.md` links instead of restating.
- Avoid doc sprawl: do not add extra top-level docs (for example `ARCHITECTURE.md`, `NOTES.md`) unless explicitly requested; prefer linking into the canonical docs above.
- Add a new module doc only when it has a distinct responsibility boundary and at least one real interface or independent milestone; otherwise keep it as a stub or keep it in the overview module map.
- When a module boundary or interface changes:
  - Update the module doc.
  - Update `OVERVIEW.md` module map/interactions.
  - Update `PLAN.md` if tasks/milestones are impacted.
  - Add a `DECISIONS.md` entry if it is a real decision (tradeoff/behavior change).
  - Update `STATUS.md` handoff block.
