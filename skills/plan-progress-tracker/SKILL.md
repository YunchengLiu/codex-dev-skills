---
name: plan-progress-tracker
description: >
  Create and maintain a durable on-disk plan+spec workpack for ongoing
  multi-agent development handoff: a linked folder containing INDEX/OVERVIEW,
  per-module specs, and PLAN/STATUS/DECISIONS. Use when a task needs a
  persistent doc set that will be revisited across sessions or agents,
  keeping overview, module boundaries, plan, status, and decisions
  synchronized. Do not use for one-shot discussion-only planning or a single
  standalone spec doc.
---

# Plan Progress Tracker

## Purpose

Create and maintain a durable on-disk workpack that remains usable across
sessions and agents. The workpack is a single source of truth for:

- fresh-agent entry: what this is, where to start, what is done, and what is
  next;
- top-down context: goals, constraints, module map, execution order, and
  acceptance;
- tracking state: plan, session status, and durable decisions without rewriting
  history.

Use for persistent workpack folders. For one-shot discussion planning, use
`planning-clarification`. For a single executable implementation spec, prefer a
spec-writing workflow. Once the workpack is stable enough, switch to direct
implementation or a domain-specific skill for code changes.

## Priority Model

Resolve conflicts in this order:

1. User-stated target folder, repo instructions, filesystem state, and existing
   workpack docs.
2. Workpack invariants: one canonical root, fresh-agent entry, single task
   inventory, session-status semantics, append-only decisions, and stable doc
   ownership.
3. Mode-specific gates: init, update, reconcile, or handoff.
4. Templates, naming preferences, formatting, and optional polish.

Do not invent module boundaries, interfaces, milestones, or decisions to make
the workpack look complete.

## Core Invariants

1. **One canonical workpack root.** Create or update exactly one folder that
   owns the workpack docs.
2. **`INDEX.md` is the fresh-agent entry anchor.** It points to where a new
   agent starts and links the other workpack docs.
3. **Minimum viable workpack first.** Always maintain `INDEX.md`, `STATUS.md`,
   `PLAN.md`, `OVERVIEW.md`, and `DECISIONS.md`. Add `modules/` only when there
   are two or more stable modules or a concrete module boundary/interface must
   be locked.
4. **Stable ownership prevents drift.** `OVERVIEW.md` owns high-level truth;
   `modules/*.md` owns concrete module interfaces; `PLAN.md` owns task IDs;
   `STATUS.md` owns current handoff state; `DECISIONS.md` owns durable
   decisions.
5. **`PLAN.md` is the only task inventory.** `STATUS.md` may point to plan IDs
   but must not introduce a parallel task list.
6. **`PLAN.md` follows the execution spine.** Early tasks must show how they
   locate missing repo evidence, prove the main path, stabilize a contract,
   unblock integration, or preserve behavior.
7. **`STATUS.md` is a session snapshot.** Update it when meaningful state
   changes, especially after a workpack update.
8. **`DECISIONS.md` is append-only for material decisions.** Add superseding
   entries instead of rewriting history.
9. **Init mode stays non-speculative.** Write the smallest viable docs with
   `TBD` and at most one to three concrete questions.
10. **Update mode preserves unrelated records.** Repair missing minimum docs
   with stubs, but do not adopt a different layout or rewrite unrelated history.
11. **Canonical docs are updated in place.** Do not fork parallel `*-v2.md`
    specs unless the user explicitly asks.
12. **Documentation boundary.** Edit only workpack documentation unless the user
    separately requests implementation.

## Workpack State Machine

Classify the operation before editing files:

1. **Clarify.** Use when the user wants a durable workpack but the scope,
   target folder, or mode is not stable enough to write. Ask only for missing
   information that changes whether, where, or how to write the workpack. If
   the scope, goals, acceptance, or handoff audience are still unstable, route
   to `planning-clarification` first.
2. **Init.** Create a new workpack at an explicit `workpack_root`. The folder
   must be non-existent or empty. Produce the minimum viable workpack and avoid
   speculative module docs.
3. **Update.** Modify an existing workpack root that already contains
   `INDEX.md`. Preserve existing unrelated content. Create missing minimum docs
   as stubs when needed.
4. **Reconcile.** Repair cross-doc drift: names, responsibilities,
   dependencies, interfaces, task IDs, open questions, links, and handoff state.
5. **Handoff.** Refresh `STATUS.md`, entry links, blockers, and next actions so
   a fresh agent can continue without session history.

## Decision Gates

- **Entry boundary gate:** Use only when the deliverable is a persistent
  on-disk folder that multiple sessions or agents will revisit. If the user
  needs only a one-shot plan or single spec doc, do not scaffold a workpack
  unless explicitly asked.
- **Path gate:** If `workpack_root` is not explicitly provided, ask once for the
  exact folder path. If the user gives only a base directory, ask for the
  workpack subfolder name and may suggest `<topic>-spec`; do not infer it.
- **Mode gate:** Treat creation as only init or update. Do not crawl or search
  for candidate workpacks. If the target is unclear, stop and ask for the exact
  `workpack_root`.
- **Init safety gate:** For init, the target folder must be non-existent or
  empty. If it exists and is non-empty, stop and ask whether to switch to update
  mode by pointing at the folder containing `INDEX.md`, or choose a different
  empty folder.
- **Update safety gate:** For update, `workpack_root` must contain `INDEX.md`.
  If `INDEX.md` is missing, stop and ask for the correct root or a different
  empty init folder. Do not adopt a non-empty folder by creating `INDEX.md` in
  place.
- **Minimum-doc repair gate:** In update mode, if `STATUS.md`, `PLAN.md`,
  `OVERVIEW.md`, or `DECISIONS.md` is missing, create stub versions using the
  templates instead of stopping.
- **Module gate:** Add thin module stubs when stable responsibility boundaries
  exist. Promote to full module docs when real interfaces, independent
  milestones, data/state, flows, or locked boundaries must be specified.
- **Decision gate:** Record a decision only when it affects constraints,
  behavior, interfaces, execution order, or repeated debate. Do not use
  `DECISIONS.md` as a changelog.

## Structured Workpack Loop

1. **Resolve mode and root.** Determine clarify, init, update, reconcile, or
   handoff. Apply the path and mode gates before editing.
2. **Anchor fresh-agent entry.** Ensure `INDEX.md` exists in valid modes and
   links to every canonical doc. Record the workpack name, root path, update
   time, and start point.
3. **Preserve or create the minimum viable workpack.** Maintain `INDEX.md`,
   `STATUS.md`, `PLAN.md`, `OVERVIEW.md`, and `DECISIONS.md`. Use stubs for
   unknowns instead of inventing content.
4. **Refresh top-down truth first.** Update `OVERVIEW.md` for background,
   goals, constraints, assumptions, module map, high-level interactions,
   execution order, acceptance, DoD, and stop conditions.
5. **Update module contracts only when real.** Create or update
   `modules/<module>.md` for concrete responsibilities, interfaces, data/state,
   flows, edge cases, and module-level DoD. Keep overview high-level and link
   rather than duplicating interface detail.
6. **Maintain tracking semantics.** Update `PLAN.md` when milestones or tasks
   change. Keep task order tied to `OVERVIEW.md` execution order and
   acceptance. Update `STATUS.md` as the current handoff snapshot. Append
   material decisions to `DECISIONS.md`.
7. **Run a consistency pass.** Reconcile names, responsibilities,
   dependencies, interfaces, task IDs, links, open questions, and ownership
   across docs.
8. **Report the handoff.** Tell the user what changed, open questions or
   blockers, and where a fresh agent should start (`INDEX.md` and `STATUS.md`).

## Canonical Ownership

- `INDEX.md`: entrypoint, links, stable metadata, and maintenance invariants for
  re-entry.
- `OVERVIEW.md`: background, goals, constraints/assumptions, high-level module
  map and interactions, execution order, acceptance criteria, DoD, and stop
  conditions.
- `modules/<module>.md`: one module's responsibilities, concrete interfaces,
  dependencies, data/state, flows, edge cases, and module-level DoD.
- `PLAN.md`: milestones and task inventory with stable IDs and links.
- `STATUS.md`: session snapshot with Now/Next/Blockers/Links; references plan
  IDs instead of creating tasks.
- `DECISIONS.md`: append-only tradeoffs and material changes, with superseding
  entries instead of rewrites.

## Reference Routing

Load only the reference files needed for the current workpack task:

- `references/workpack-layout.md`: use when deciding file responsibilities,
  resolving single-source-of-truth conflicts, or repairing cross-doc drift.
- `references/templates.md`: use when initializing a workpack, creating missing
  docs, normalizing headings, or choosing between thin and full module docs.

## Writing Rules

- Optimize for later agents: short bullets, checkable statements, stable terms
  and IDs, and minimal narrative filler.
- Keep background and rationale to one screen; put extended tradeoffs in
  `DECISIONS.md`.
- Prefer positive scope: deliverables, DoD, and stop conditions.
- Default to no `Non-goals` section. Add it only when it prevents active scope
  creep, and keep it short, typically no more than three items.
- Avoid long "not X / not Y" lists when the positive description is already
  clear.
- Use one stable name for each concept. Avoid synonyms for the same module,
  task, interface, state, or decision.
- Keep open questions owned: cross-cutting questions in `OVERVIEW.md`,
  module-local questions in the module doc, and `STATUS.md` links instead of
  restating them.
- Prefer verifiable references to repo paths, PRs, issues, or command outputs
  when available.

## Self-check

Before finalizing a workpack update, verify:

- the task genuinely needs a persistent workpack rather than discussion-only
  planning or a single spec;
- edits stayed within workpack documentation unless implementation was
  separately requested;
- the mode and `workpack_root` satisfied the path, init, and update gates;
- `INDEX.md` lets a fresh agent find current state and next steps;
- all minimum viable workpack docs exist or were created as stubs in valid
  update/init modes;
- `PLAN.md` remains the only task inventory;
- early `PLAN.md` tasks state their role in locating missing evidence or
  advancing the execution spine, or remain deferred;
- `STATUS.md` is a lightweight handoff snapshot and points to plan IDs when
  tasks exist;
- `DECISIONS.md` contains only material durable decisions and remains
  append-only;
- overview and module docs agree on names, responsibilities, dependencies,
  interfaces, execution order, and acceptance;
- uncertain content is marked `TBD` with at most one to three concrete
  questions instead of being invented;
- no parallel doc fork, duplicate interface definition, or conflicting source
  of truth was introduced.
