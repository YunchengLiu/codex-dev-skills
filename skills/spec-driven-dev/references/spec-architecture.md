# Spec Architecture

## Purpose

Use this reference before drafting or reorganizing a non-trivial spec. Its job is to turn repo evidence and user intent into settled architecture, implementation path, phase order, and design checks before detailed requirements are written.

Treat the architecture pass as internal structured thinking. Write the resulting decisions in the order another agent needs them; do not reproduce the full reasoning process or its temporary terminology.

## Non-trivial Threshold

Treat a spec as non-trivial when it changes public behavior, crosses meaningful ownership boundaries, adds or changes fixtures, changes pipeline boundaries, affects failure/state/lifecycle behavior, or needs phase handoff. Use by a fresh agent does not by itself require a heavier spec.

For a trivial single-slice spec, still inspect the target file and adjacent tests, then use a compact version of the same thinking frame.

## Architecture Thinking Frame

Follow this order. Each step has a question to answer and an artifact to write.

1. **Classify the task.**
   - Ask: Is this a refactor, incremental feature, new development, repair, or spec revision?
   - Write: task type and why that classification controls depth.
2. **Collect repo evidence.**
   - Ask: Which applicable repo instructions, modules, tests, fixtures, public APIs, existing specs, and conventions already constrain the work?
   - Ask: What current callers, data volume, execution model, lifecycle, compatibility surface, and failure obligations are established by the request or repo?
   - Write: only the repo landing points, operating envelope, and constraints that materially affect this spec. Do not invent or restate repo rules unnecessarily.
3. **Name the behavior target.**
   - Ask: What observable behavior, output, state transition, command, API result, or acceptance signal proves success?
   - Write: behavior target before component names.
4. **Choose the implementation spine.**
   - Ask: Which repo-local route owns the behavior: user flow, API call chain, pipeline/data path, migration path, lifecycle transition, CLI command flow, compiler pass, or equivalent?
   - Ask: Which capabilities must already exist at each handoff, what is the simplest functionally correct path, and which evidenced optimization can follow later?
   - Write: spine, owner/consumer/assembler/coordinator, immediate upstream, immediate downstream, dependency order, and correctness-first phase outline.
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

Produce a concise architecture analysis before drafting when it materially helps the task. Use this form selectively or follow the repo's stronger convention:

```md
## Spec Shape

Task type:
Repo landing points:
Existing conventions:
Behavior target:
Operating envelope:
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

Keep this analysis short. Its job is to place the spec in the repo and assign unresolved details to a handling path. Omit fields that do not affect the design; do not emit an empty form.

Use repo conventions when they preserve fresh-agent entry, stable/dynamic separation, phase sliceability, and fixture acceptance. When a convention weakens those properties, adapt it minimally and state the adaptation.

## Open Gap Routing

Assign every open spec gap one path before drafting continues:

- `default`: write the settled default into the relevant requirements or phase brief.
- `defer`: record a deferred decision with a current-phase default and decision point.
- `block`: stop the spec or phase until the user resolves the gap.

Use repo evidence for defaults. Use `defer` or `block` when repo evidence is insufficient. A missing safe default blocks the current phase.

## Repo Evidence

Read the applicable repo instructions and identify the implementation surface before writing requirements:

- source files, packages, generated surfaces, or configuration likely to change
- tests and fixtures that define behavior
- public API, command, UI, data format, or integration surface
- public entry points, top-level consumers, assemblers, coordinators, or lifecycle roots that own the behavior
- upstream and downstream pipeline stages
- naming, error, lifecycle, dependency, build, test, and export conventions
- current spec or planning directories

If repo evidence conflicts with the requested shape, state the conflict and choose the smallest compatible layout.

Use repo evidence to shape the design; do not copy general repo instructions, ordinary workflows, or local absolute paths into the spec. Record only a task-specific exception, a design-relevant constraint, a useful repo-relative landing point, or verification that is not already evident from the repo.

## Gate Details

### Design Simplification Gate

Run this before component designs and phase briefs.

Ask:

- Which behavior or acceptance signal justifies each component, facade, phase, or helper?
- Which current requirement, repo constraint, fixture, observed failure,
  acceptance signal, or integration risk justifies abstraction depth, defensive
  behavior, performance work, or extensibility?
- What evidenced scale, caller set, execution model, lifecycle, compatibility surface, or failure obligation requires concurrency control, asynchronous coordination, recovery, caching, generalized state machinery, or large-scale optimization?
- Can an internal helper remain an ordinary implementation detail instead of being treated as a compatibility surface?
- Can responsibility move to the owning entry point, consumer, assembler, coordinator, or lifecycle root to remove local awkwardness?
- Is a bounded stub on the spine better than a helper-first phase that guesses future interfaces?
- Is any abstraction present only to make a local micro-task convenient?
- Does unusual glue, adapter layering, fallback behavior, or indirection indicate a boundary problem?

Pass when the planned design makes the smallest executable behavior path obvious for the evidenced operating envelope. Fail when it introduces hypothetical scale, callers, concurrency, recovery, compatibility, or state machinery without a current requirement or repo-based integration risk.

### Implementation Spine Gate

Analyze the implementation path from the behavior target:

1. observable behavior or acceptance signal
2. task-shaped implementation spine
3. owning public entry point, caller, consumer, assembler, coordinator, or lifecycle root
4. design-relevant handoff points along the spine
5. minimal facades or stubs needed to keep the current spine executable

Stop the written design at the last design-relevant handoff. Production decomposition below that boundary is re-derived from repo conventions during implementation. Plan the whole spec in dependency order before detailing the current phase. A phase is valid only when everything required for its acceptance already exists or lands no later than that phase. A helper-first phase is valid only when the caller surface already exists and is stable, or the task is an isolated repair under a frozen public surface. State that justification in the phase plan.

Example: `Phase 01: implement timestamp formatter helper` is invalid when no report command, output requirement, or caller path exists. `Phase 01: add report command skeleton with a formatter stub` is valid only when its acceptance is limited to the command/output path and does not claim correct formatted output before the formatter fill-in phase.

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

Escalate when the needed edit broadens the phase, changes required behavior or fixture meaning, restructures unrelated systems, moves ownership across components, or is not clearly required by repo convention.

### Review-sized Phase Gate

A phase is valid when it has:

- one focused behavior surface, integration point, public requirement, fixture set, or cleanup boundary
- a named spine/mainline position
- dependencies that already exist or land no later than the phase
- local acceptance and verification
- a handoff condition
- a review surface that can reasonably land as one coherent commit unless repo practice requires otherwise

A phase is too early when it implements private leaf behavior before the owner, public entry point, consumer, assembler, coordinator, lifecycle root, or minimal executable spine exists.

Establish a functionally correct result for the declared current domain before optimization. A later phase may improve performance, scale, or generality only when the earlier result remains correct without it. Record the later phase or concrete extension trigger when the current mechanism is intentionally non-optimal; do not defer behavior required by current acceptance.

### Mutability and Record Gate

Stable specs, phase briefs, and frozen fixtures are read-only during implementation unless the current task explicitly authorizes spec revision. Dynamic records are append-oriented and sparse.

When spec correction is in scope, correct wrong or unclear canonical text directly. Record a decision only when the work introduces or selects a new durable constraint not already captured by the corrected spec.

## Collaboration Model

For gated copilot execution, put a short collaboration model at the top of the stable entry or overview only when the spec itself needs to carry that execution policy:

```md
## How To Use This Spec

- Entry: start in the repo, read `CURRENT.md`, the current brief, relevant stable spec docs, repo instructions, and the touched code.
- Before coding: summarize the current phase goal, implementation spine, edit boundary policy, frozen paths, acceptance, verification, and first action.
- Approval: wait for user approval before modifying code when the workflow is interactive.
- Execution: implement only the current phase; do not pull future-phase work forward.
- Verification: run repo-configured checks or the phase's verification commands.
- Review handoff: report changes, verification, boundaries, blockers, and next mainline phase.
```

Keep this operational and omit it when repo instructions or the selected execution mode already supply the same policy. Do not duplicate a standard workflow in every spec.

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
- public interface, command, data format, or externally visible shape when it is an explicit requirement
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
