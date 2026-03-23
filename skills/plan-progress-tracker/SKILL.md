---
name: plan-progress-tracker
description: Create and maintain a durable on-disk plan+spec workpack for ongoing multi-agent development handoff: a linked folder containing INDEX/OVERVIEW, per-module specs, and PLAN/STATUS/DECISIONS. Use when Codex should write or update a persistent doc set that will be revisited across sessions/agents, keeping overview, module boundaries, plan, status, and decisions synchronized. Do not use for one-shot chat-only planning or a single standalone spec doc.
---

# Plan Progress Tracker

## Intent

Produce and maintain a **single source of truth** folder (a "workpack") that stays usable across fresh chats and different agents:

- Quickly orient a new agent: what this is, why it exists, what is done, what is next.
- Keep **overview** and **module specs** consistent as the design evolves.
- Track **plan**, **status**, and **decisions** without rewriting history.

## Minimum Viable Workpack (MVW)

Default to the smallest durable set, then deepen only when needed:

- Always: `INDEX.md`, `STATUS.md`, `PLAN.md`, `OVERVIEW.md`, `DECISIONS.md`.
- Add `modules/` only when there are 2+ stable modules, or when a concrete module boundary/interface must be locked.
- Prefer the module *stub/thin* template early; promote to the full template only when interfaces/behavior are real or required.

## Entry Boundary (use this vs other skills)

Use this skill only when the expected deliverable is a **persistent on-disk workpack folder** that multiple sessions/agents will update.

- If the request is still vague or unstable, use `$planning-clarification` first; once the scope is stable enough, write/update the workpack.
- If the request only needs a one-shot plan or a single spec doc, do not scaffold a full workpack unless the user explicitly asks.

## Operating Contract

### Inputs (ask minimally)

- If `workpack_root` is not explicitly provided, ask **once** for the exact folder path where the workpack docs should live.
  - For init: the folder should be empty or non-existent.
  - For update: the folder should already contain `INDEX.md`.
- If the user only provides a base directory, ask for the workpack subfolder name (suggest `<topic>-spec`); do not infer.
- Do not repeatedly ask for paths in later turns. In update mode, the workpack itself (via `INDEX.md`) is the stable anchor.

### Canonical ownership (prevent contradictions)

- `INDEX.md`: entrypoint, links, stable metadata for re-entry.
- `OVERVIEW.md`: background/goals, module map, **high-level** interactions, execution order, acceptance criteria.
- `modules/<module>.md`: responsibilities and **concrete interfaces**, data/state, flows, edge cases, module-level DoD.
- `PLAN.md`: task inventory with stable IDs and links.
- `STATUS.md`: session snapshot (Now/Next/Blockers/Links), not a second plan.
- `DECISIONS.md`: append-only tradeoffs/changes; superseding entries instead of rewrites.

### Init rules (keep it simple)

Treat workpack creation as having only two modes, and avoid auto-discovery:

- **Init (new workpack)**: create a new workpack folder at `workpack_root` and write docs there.
  - Precondition: the chosen `workpack_root` must be **non-existent or empty**.
  - If `workpack_root` exists and is non-empty, stop and ask the user: switch to update mode (point to the folder that contains `INDEX.md`), or choose a different empty folder.
- **Update (existing workpack)**: update docs in an existing workpack root.
  - Precondition: `workpack_root` must contain `INDEX.md`.
  - If `INDEX.md` is missing, stop and ask the user whether this folder should be treated as a workpack (create `INDEX.md` here) or whether they meant another folder.

Do not crawl/search for candidate workpacks. If the target is unclear, stop and ask the user for the exact `workpack_root` path.

Init mode goal: create the MVW structure with minimal, non-speculative content. If details are unknown, write `TBD` and add at most 1-3 concrete questions; do not invent module boundaries or interfaces.

### Layout and templates

- Read [references/workpack-layout.md](references/workpack-layout.md) when deciding file responsibilities or resolving cross-doc conflicts.
- Read [references/templates.md](references/templates.md) when creating missing docs or normalizing headings/sections.

## Workflow

### 0. Update-only fast path (avoid churn)

In update mode, if the user did not request a design/spec change:

- Update `STATUS.md` (handoff block) and `PLAN.md` task statuses.
- Do not touch `OVERVIEW.md` or `modules/*.md` unless behavior/requirements/interfaces changed.

### 1. Resolve mode and target folder (no guessing)

Resolve init vs update using the `Init rules` above. If the mode or `workpack_root` is unclear, stop and ask the user rather than guessing.

### 2. Create or refresh the workpack entrypoint (`INDEX.md`)

- Ensure `INDEX.md` exists and clearly links to every other doc in this workpack.
- Record: workpack name, workpack root path, last updated time, and "where to start" for a fresh agent.

### 3. Write/refresh overview first, then module specs

Produce `OVERVIEW.md` as the top-down truth:

- Background (problem context, user need, constraints, assumptions).
- Module map and **high-level** interactions (dependencies and interaction story; link to module docs for exact interfaces).
- Execution order (what to build first, what unlocks what).
- Acceptance criteria (deliverables + DoD + stop conditions).

Then create/update `modules/<module>.md` files using the same stable headings, but **do not duplicate** overview content: modules own the concrete interface details; overview links.

### 4. Maintain tracking docs with clear semantics

- `PLAN.md`: tasks/milestones. Update when the plan changes.
- `STATUS.md`: handoff block at the top. Update every session that changes state.
- `DECISIONS.md`: append-only. If a decision changes, add a new entry that supersedes the old one.

### 5. Consistency pass (prevent contradictions)

Before reporting back:

- Reconcile overview vs module docs: names, responsibilities, dependencies, interfaces must match.
- Ensure cross-doc links are correct and no file claims ownership of the same responsibility in conflicting ways.
- If something is uncertain, mark it as `TBD` and add a single clear question rather than speculating.

### 6. Report back in chat (short handoff)

After writing files, provide a concise report:

- What changed in this update.
- Any open questions / blockers.
- Where a fresh agent should start (`INDEX.md` + `STATUS.md`).

## Writing Rules (keep it agent-usable)

- Default spec writing style: optimize for agents (execution-oriented), not humans (narrative-oriented).
  - Prefer short bullets and checkable statements over prose.
  - Keep background/rationale to one screen; put extended tradeoffs in `DECISIONS.md`.
  - Use consistent terminology and stable names across docs; avoid synonyms for the same concept.
- Prefer **positive scope**: deliverables + DoD + stop conditions.
- Default to **no** "Non-goals" section; add it only when it prevents active scope creep, and keep it short (typically <= 3 items).
- Do not add long "not X / not Y" lists as redundant clarification when the positive description is already correct.
- Keep module boundaries crisp: one owner per responsibility; link to the owning module doc rather than duplicating details.
- Do not fork docs: prefer updating canonical files in place. If legacy docs exist under different names, pick one canonical mapping and link it from `INDEX.md` rather than creating parallel new spec files.
- Keep `STATUS.md` lightweight: when `PLAN.md` has task IDs, `STATUS.Next` should reference those IDs; do not introduce net-new tasks only inside `STATUS.md`.
- Keep open questions owned: cross-cutting questions in `OVERVIEW.md`; module-local questions in the module doc; `STATUS.md` links to them instead of restating.
- Prefer verifiable references: link to repo paths, PRs/issues, or command outputs when available.

## Boundaries

- This skill is for creating and maintaining the workpack docs and their synchronization discipline.
- Once the workpack is stable enough, switch to implementation or a more domain-specific skill for code changes.
