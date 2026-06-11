# Spec Architecture

## Purpose

Use this reference before drafting or reorganizing a non-trivial spec. Its job is to turn repo evidence and user intent into a document architecture, implementation spine, phase order, and gate results before detailed contracts are written.

Treat the architecture pass as structured thinking. Write the result in the same order another agent should read it.

## Non-trivial Threshold

Treat a spec as non-trivial when it changes public behavior, crosses more than one file, adds or changes fixtures, changes pipeline boundaries, affects failure/state/lifecycle behavior, needs phase handoff, or will be implemented by a fresh agent.

For a trivial single-slice spec, still inspect the target file and adjacent tests, then use a compact version of the same thinking frame.

## Architecture Thinking Frame

Follow this order. Each step has a question to answer and an artifact to write.

1. **Classify the task.**
   - Ask: Is this a refactor, incremental feature, new development, repair, or spec revision?
   - Write: task type and why that classification controls depth.
2. **Collect repo evidence.**
   - Ask: Which modules, tests, fixtures, public APIs, existing specs, repo instructions, and conventions already constrain the work?
   - Write: repo landing points and conventions. Do not invent repo rules.
3. **Name the behavior target.**
   - Ask: What observable behavior, output, state transition, command, API result, or acceptance signal proves success?
   - Write: behavior target before component names.
4. **Choose the implementation spine.**
   - Ask: Which repo-local route owns the behavior: user flow, API call chain, pipeline/data path, migration path, lifecycle transition, CLI command flow, compiler pass, or equivalent?
   - Write: spine, owner/consumer/assembler/coordinator, immediate upstream, and immediate downstream.
5. **Run the gates.**
   - Ask: Does the design pass simplification, spine order, review-sized phase scope, edit boundary policy, mutability, and material decision handling?
   - Write: short pass/fail notes and any required redesign.
6. **Choose the spec layout.**
   - Ask: Which stable docs, current pointer, phase briefs, fixtures, and progress records are needed for fresh-agent entry?
   - Write: `spec-root/` structure or the repo's stronger convention.
7. **Route open gaps.**
   - Ask: Is each gap safe to default, defer with a current-phase default, or block?
   - Write: one handling path for each gap before drafting continues.

## Spec Shape Output

Produce a concise architecture analysis before drafting. Use this form or the repo's stronger convention:

```md
## Spec Shape

Task type:
Repo landing points:
Existing conventions:
Behavior target:
Implementation spine:
Owner/consumer/assembler:
Immediate upstream:
Immediate downstream:
Gate results:
Collaboration model:
Stable spec root:
Stable docs:
Phase briefs:
Fixtures:
Progress records:
Current pointer:
Edit boundary policy:
Frozen strategy:
Generality boundary:
Review insertion policy:
Open spec gaps:
```

Keep this analysis short. Its job is to place the spec in the repo and assign unresolved details to a handling path.

Use repo conventions when they preserve fresh-agent entry, stable/dynamic separation, phase sliceability, and fixture acceptance. When a convention weakens those properties, adapt it minimally and state the adaptation.

## Open Gap Routing

Assign every open spec gap one path before drafting continues:

- `default`: write the binding default into the relevant contract or phase brief.
- `defer`: record a deferred decision with a current-phase default and decision point.
- `block`: stop the spec or phase until the user resolves the gap.

Use repo evidence for defaults. Use `defer` or `block` when repo evidence is insufficient. A missing safe default blocks the current phase.

## Repo Evidence

Identify the implementation surface before writing contracts:

- source files, packages, generated surfaces, or configuration likely to change
- tests and fixtures that define behavior
- public API, command, UI, data format, or integration surface
- public entry points, top-level consumers, assemblers, coordinators, or lifecycle roots that own the behavior
- upstream and downstream pipeline stages
- naming, error, lifecycle, dependency, build, test, and export conventions
- current spec or planning directories

If repo evidence conflicts with the requested shape, state the conflict and choose the smallest compatible layout.

## Gate Details

### Design Simplification Gate

Run this before component contracts and phase briefs.

Ask:

- Which behavior or acceptance signal justifies each component, facade, phase, or helper?
- Can responsibility move to the owning entry point, consumer, assembler, coordinator, or lifecycle root to remove local awkwardness?
- Is a bounded stub on the spine better than a helper-first phase that guesses future interfaces?
- Is any abstraction present only to make a local micro-task convenient?
- Does unusual glue, adapter layering, fallback behavior, or indirection indicate a boundary problem?

Pass when the planned design makes the smallest executable behavior path obvious. Fail when small local slices create distorted code, premature abstractions, or likely rework at the owner/consumer boundary.

### Implementation Spine Gate

Derive the implementation tree from the behavior target:

1. observable behavior or acceptance signal
2. task-shaped implementation spine
3. owning public entry point, caller, consumer, assembler, coordinator, or lifecycle root
4. handoff points and component contracts along the spine
5. minimal facades or stubs needed to keep the current spine executable
6. component internals
7. private helpers and leaf mechanics

Plan phases in this order. A helper-first phase is valid only when the caller contract already exists and is stable, or the task is an isolated repair under a frozen public surface. State that justification in the phase plan.

Example: `Phase 01: implement timestamp formatter helper` is invalid when no report command, output contract, or caller path exists. `Phase 01: add report command skeleton with a formatter stub` is valid when it verifies the command/output path and names the later formatter fill-in phase.

### Edit Boundary Policy Gate

Use edit boundaries to focus implementation without blocking required repo integration.

State:

```md
Edit boundary:
- Primary targets:
- Tests/fixtures:
- Repo-required collateral policy:
- Frozen:
- Escalation rule:
- Reporting:
```

Primary targets are expected implementation anchors, not an exhaustive closed list unless the spec explicitly says they are closed.

Repo-required collateral is allowed only when it is directly caused by the current phase, required by observed repo conventions, minimal, mechanical, and behavior-neutral. Examples include build/test registration, export/index files, manifests, or generated registries required to make new files visible. Treat these as examples, not guessed requirements.

Escalate when the needed edit broadens the phase, changes contract or fixture meaning, restructures unrelated systems, moves ownership across components, or is not clearly required by repo convention.

### Review-sized Phase Gate

A phase is valid when it has:

- one focused behavior surface, integration point, contract, fixture set, or cleanup boundary
- a named spine/mainline position
- local acceptance and verification
- a handoff condition
- a review surface that can reasonably land as one coherent commit unless repo practice requires otherwise

A phase is too early when it implements private leaf behavior before the owner, public entry point, consumer, assembler, coordinator, lifecycle root, or minimal executable spine exists.

### Mutability and Record Gate

Stable specs, phase briefs, and frozen fixtures are read-only during implementation unless the current task explicitly authorizes spec revision. Dynamic records are append-oriented and sparse.

When spec correction is in scope, correct wrong or unclear canonical text directly. Record a decision only when the work introduces or selects a new durable constraint not already captured by the corrected spec.

## Collaboration Model

For interactive spec-driven development, put a short collaboration model at the top of the stable entry or overview:

```md
## How To Use This Spec

- Entry: start in the repo, read `CURRENT.md`, the current brief, relevant stable spec docs, repo instructions, and the touched code.
- Before coding: summarize the current phase goal, implementation spine, edit boundary policy, frozen paths, acceptance, verification, and first action.
- Approval: wait for user approval before modifying code when the workflow is interactive.
- Execution: implement only the current phase; do not pull future-phase work forward.
- Verification: run repo-configured checks or the phase's verification commands.
- Review handoff: report changes, verification, boundaries, blockers, and next mainline phase.
```

Keep this operational. It tells a fresh implementation agent how to cooperate with the user; it is not a project introduction.

## Task Type Depth

### Refactor

Define:

- exact edit boundary policy and frozen behavior
- compatibility and migration constraints
- verification proving unchanged behavior outside the target
- repo-required collateral principles based on observed conventions

### Incremental Feature

Define:

- where new behavior attaches
- public surface change
- upstream input guarantees
- downstream output expectations
- fixture additions
- phase boundary between integration, fill-in, and cleanup

### New Development

Define:

- planned file paths or module ownership
- public interface, command, data format, or externally visible shape when it is part of the contract
- fixture paths
- verification commands
- first usable phase and later integration phases

Do not prescribe private class names, private method names, helper decomposition, or repo-style choices that should come from implementation context.

## Generality Classification

Classify implementation depth from repo evidence:

- `repo-local`: serves this repo's workflow and stated fixtures
- `limited-domain`: supports a defined input domain or DSL with bounded syntax and callers
- `general-purpose`: intentionally supports broad external use, extensibility, or unknown callers

Default to `repo-local` or `limited-domain`. Use `general-purpose` only when the user request or existing public API requires broad external behavior.

When broader capability may be useful later, record the extension trigger and keep the current phase at the selected depth.
