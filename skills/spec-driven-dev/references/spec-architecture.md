# Spec Architecture

## Purpose

Use this reference before drafting or reorganizing a non-trivial spec. Turn the user's goal and repo evidence into a clear whole, a practical plan, and only the detail needed for correct implementation.

The analysis used to reach the design stays internal. The spec contains the resulting decisions, not a reasoning transcript, system survey, or explanation of unaffected code.

A compact task still needs repo inspection, a goal, a short whole-system explanation, and a plan. It does not need architecture artifacts or extra files for completeness.

## Top-Down Method

### 1. Start from the repo and the result

Inspect the evidence that shapes this change:

- applicable repo instructions;
- relevant entry points, existing facilities, callers, modules, tests, fixtures, and public surfaces;
- current execution, data scale, lifecycle, compatibility, and failure rules when they matter;
- existing specs and planning conventions when relevant.

Settle repo-specific design only after this inspection. If the repo cannot be inspected, say which conclusions are provisional. Cite repo-relative sources instead of copying ordinary instructions, workflows, existing-code explanations, or machine-specific paths into the spec.

Use the current user request, active spec or brief, repo instructions and contracts, and current code and tests as the primary sources. Treat historical material, analogy, and inference as evidence rather than active requirements. The latest explicit instruction controls current scope while compatible accepted requirements remain in force; resolve or report conflicts that affect the current work before relying on a source.

State the intended result before naming components, helpers, files, or planning groups. Existing source structure is evidence and a possible facility, not a default plan.

### 2. Explain one run from start to result

Before component detail, show how the new behavior proceeds from entry or input to its visible result. Include only what affects this change:

- the code or component that owns the operation;
- important branches;
- data or state at important boundaries;
- identity, ownership, lifetime, and runtime organization where they change implementation;
- important differences from the repo's current design.

One sentence may be enough for a simple flow. Use a short ordered or branched list when needed. A list of component duties is not a substitute if the reader still cannot reconstruct how the behavior works.

### 3. Place responsibility and fix contracts

Put behavior and state with the code that owns their lifecycle and rules. State the public interfaces, what one component may assume about another, inputs, outputs, failure behavior, and acceptance that must remain stable across reasonable implementations.

Stop at the last boundary that changes a design decision. Private decomposition below it comes from repo conventions during implementation.

### 4. Plan the work

Use the minimum plan shape in `SKILL.md`. Order its steps by the actual path from entry through owners and handoffs to the result, then by hard dependencies and useful feedback; choose commit boundaries only after the steps are clear.

A phase is a meaningful slice of the goal with its own result and acceptance. List its ordered steps directly; compact work can list steps without naming a phase. If a phase is too large for one clear, manageable list, group those steps into tasks, each with its own ordered steps. Each step completes one concrete result and normally maps to one commit. If one result needs adjacent commits for a real dependency, review or integration boundary, useful feedback, or repo/user policy, list them in order under the same step. A step may be part of a larger approved commit when repo or user policy calls for it. Do not split by source files or to reach a count.

A bounded investigation may be a step when its result is evidence or a decision. A clearly bounded step may sit beside the main order when its purpose, boundary, result, and checks are already clear; shared feature membership or its code category is not enough. If later integration must decide its behavior or interface, keep only its goal in the future plan. For a current phase, outline the reasonably knowable steps and their order now, and defer private details that depend on later design. Future phases stay at goal and dependency depth. Do not add another planning level by default; if one is genuinely needed, state its concrete benefit. The agent chooses and explains the simplest order and granularity.

### 5. Create only the files the work needs

Use one spec while it remains clear. Add a standalone implementation brief only when the current step must be assigned, reviewed, or resumed on its own. Add current-state, progress, or decision files only when future work would otherwise be ambiguous. Follow `file-organization.md`.

Lower-level details that the current discussion has not reached are later work, not missing architecture.

## Report the Design

When summarizing the architecture, main development order, or an existing spec, begin with the intended result and the repo-based understanding of the whole. Then show the parts that serve it, what must come first versus what is merely a preferred order, and why the design, grouping, and order fit the repo and task.

For a phase, show its result and ordered steps; mention adjacent commits and their reasons only when a step is split. For a task grouping, show only its local goal and ordered steps. At the whole-task level, also include how one run works, important contracts, acceptance, and verification. Do not create empty headings for compact work.

## When to Split Work

Split the work into separate execution steps only when the split provides at least one real benefit:

- a clear goal, capability, or responsibility;
- a real dependency or useful risk or feedback order;
- a result that can be checked honestly at that point;
- a useful boundary for assignment, review, or resuming work;
- isolation of a risk that would otherwise obscure the work.

Several files or components alone do not justify a split. When applicable, keep the declarations, implementation, tests, and wiring for one step result together. If a step result is packaged into multiple commits, follow the user or repo policy and state the order and real boundary; commit packaging does not define the plan.

## Open Questions

Raise only an unresolved point that prevents the current level from becoming clear or makes current work unsafe. Resolve it by choosing a repo-supported default, deferring it with a safe confirmed default, or blocking when no safe choice exists.

Do not inventory lower-level details that have not been reached. A proposed default that changes behavior, interfaces, ownership, acceptance, or policy still needs confirmation before the spec or implementation relies on it.

## Design Checks

### Keep the design small

Add a component, abstraction, stage, or special mechanism only when current behavior, acceptance, repo constraints, observed failure, or integration risk calls for it. Internal helpers remain ordinary implementation details unless a real consumer or accepted design gives them an independent compatibility promise.

Unexpected glue, adapters, fallback paths, or machinery are reasons to recheck ownership and scope. They are not automatic proof that another abstraction is needed.

### Design new development as new development

First identify whether the work is new development, an incremental feature, a refactor, or a migration. New development starts from the requested target, real owners and entries, key interfaces, and first usable result. Existing code and its file layout are not a one-to-one work breakdown. Transition components, compatibility layers, adapters, and replacement sequences belong only to an actual existing-system constraint. A refactor or migration is planned by the behavior being preserved or changed, not by copying every old component unless that component is itself a stable contract or integration boundary.

Use mature systems and domain practice to understand proven ideas and tradeoffs. Copy an organizational pattern or abstraction only when it solves a current need, fits this repo and scale, and is better than a simpler local design. Reputation alone does not establish fit.

### Fit compatibility to actual commitments

First identify what, if anything, must remain compatible. Evidence includes released or installed public surfaces, real downstream users, persisted data or wire formats, repo policy, and explicit user commitments. Existing code or names alone do not create a compatibility obligation; tests carry compatibility weight only when they represent one of these commitments.

For new or unreleased work with no such commitment, prefer correcting an unsuitable design directly unless the user asks to preserve it. For an internal refactor behind a stable external contract, keep the promised surface and behavior while replacing the internals. Temporary use of the old path is acceptable to keep development runnable and verifiable, but the plan should converge on one implementation rather than preserve two permanent systems.

When an external contract must change, discuss the affected users and transition before settling the spec. For real downstream users, normally recommend a bounded period in which old and new surfaces coexist, preferably sharing the new internals where practical, followed by removal of the legacy surface. A direct break, version boundary, adapter, or another transition may fit better depending on release policy, migration cost, and user direction. State what remains compatible, how migration works, and what condition allows the old path to be removed.

### Keep performance at the requested depth

Treat performance as a current requirement when the request or repo supplies a workload and measurable target that this work must meet. State the relevant time, memory, throughput, or latency limit and how it will be checked.

A broad future scale estimate means the initial design should avoid obvious waste and hard-to-change limits without sacrificing clear ownership, low coupling, or a correct first system. It does not by itself require streaming, parallelism, sharding, caching, recovery systems, or another large-scale design. Specific optimization normally follows a working system and measurements in a separate task and spec.

### Keep current implementation boundaries useful

For a current implementation step, name only what focuses the work:

- expected source and test locations;
- behavior or files that must remain unchanged;
- minimal registration, export, build, or generated-file edits required by observed repo practice;
- changes that require a new decision or approval.

Expected locations are anchors, not a brittle exhaustive file list unless the user explicitly makes them one.

### Keep specs and records current

The main spec and accepted current brief state the active requirements. Revise them only when spec revision is authorized. Correct wrong or unclear text directly. Use decisions and progress records only as described in `progress-and-decisions.md`.

## Task Types

- **Refactor:** identify the external behavior or surface that must remain stable, then replace the internals toward one final implementation and verify the preserved contract.
- **Incremental feature:** define where behavior attaches, changed interfaces or assumptions, and the route to a usable result.
- **New development:** define the target directly, including ownership, real entries, visible shape, first usable result, and only enough later planning to show feasibility and dependencies.

Private class names, helper layouts, line-level edits, and ordinary repo mechanics remain implementation choices unless they are themselves public requirements.
