# File Organization

## Purpose

Use this reference when deciding how much file structure a spec needs. Its job is to keep the design easy to read and execute with the fewest documents justified by the work.

## Organization Thinking Frame

Choose the file shape by answering these questions in order:

1. **Can one document express the design clearly?**
   - Use one spec for a single slice or a small number of closely related phases.
2. **Do phases need independent execution briefs?**
   - Split briefs only when phases are independently assigned, reviewed, or resumed.
3. **Does the work need durable handoff state?**
   - Add `CURRENT.md`, progress, or decisions only for cross-session or multi-agent work where the state cannot remain obvious from the spec and repo.
4. **What is mutable?**
   - Mark stable docs, phase briefs, and frozen fixtures as read-only during implementation unless the current task authorizes spec revision.
5. **What must stay sparse?**
   - Keep progress and decisions focused on future execution judgment, not review chatter or transcript history.

## Layout Selection

Prefer the repo's existing convention. Otherwise choose the smallest fitting shape.

For a compact feature or one to two closely related phases:

```text
spec.md
```

Keep goals, design, phase order, acceptance, and verification in the same document when that remains easy to read.

For several independently executable phases:

```text
spec-root/
  overview.md
  phase-plan.md
  briefs/
    phase-01-<name>.md
    phase-02-<name>.md
```

For durable cross-session or multi-agent handoff, add only the dynamic files needed:

```text
spec-root/
  CURRENT.md
  overview.md
  phase-plan.md
  briefs/
    phase-01-<name>.md
    phase-02-<name>.md
  progress/
    progress.md
    decisions.md
```

Add fixture indexes or component documents only when their content is too substantial for the overview or phase brief. Do not create empty layers or split content solely to match this example.

## Current Pointer

When durable handoff needs a dynamic entry pointer, use `CURRENT.md` or the repo equivalent and keep it short:

```md
# Current

Current phase:
Current brief:
Progress file:
Decision file:
Blocked:
Next action:
Mainline return:
```

When the work does not require durable handoff, omit this file. When an existing repo convention uses another location, keep the needed fields there.

## Stable Layer

When the chosen layout has a stable layer, it may contain the following applicable content. This is not a required section checklist:

- collaboration model when interactive phased development needs one
- goals and non-goals
- behavior target and implementation spine
- component responsibilities and ownership
- module boundaries and public API shape
- pipeline order and input guarantees
- state, lifecycle, and failure model
- phase plan and review insertion policy
- fixture index and acceptance semantics
- edit boundary policy for planned phases

Stable docs are canonical. They should state settled design requirements, not meeting notes.

When spec correction is in scope, revise wrong, unclear, or poorly shaped canonical text directly. Record a decision first only when the change introduces or selects a new durable constraint not already captured by the corrected spec.

## Phase Brief Layer

When phases need independent execution, `spec-root/briefs/` contains execution-facing briefs. Each brief is stable for its phase but narrow to its slice.

Each brief should be independently feedable to an implementation agent and state only the applicable items:

- current phase goal
- spine/mainline position
- primary targets and frozen scope
- repo-required collateral policy
- current requirements
- acceptance and verification
- handoff

During implementation, a phase brief is read-only unless the current task explicitly includes revising that brief. If correction is in scope, correct the brief directly for clarity or accuracy. Record a decision only for material future-facing choices.

## Dynamic Layer

When durable handoff needs dynamic records, `spec-root/progress/` contains only the applicable execution state:

- phase start or finish when it affects handoff
- milestone status
- blocker introduced or cleared
- downstream entry condition changed
- verification status changed
- mainline adjustment or review insertion return point
- material decisions for spec gaps
- fixture errata

Dynamic records are append-oriented. Preserve existing entries and unrelated content. Correct stale entries by appending a later state point.

The latest dynamic state should let a new agent identify the current phase, blocker status, current brief, and next action without reading chat history.

## Mutability Gate

Before editing any spec file, ask:

- Is this stable canonical text, a phase brief, a frozen fixture, or a dynamic record?
- Does the current task explicitly authorize revising it?
- Is the change a direct correction to canonical text, or a new durable decision?
- Will a future agent need this history to choose behavior, or can the corrected spec stand alone?

Use the answer this way:

- Correct canonical specs directly when revision is in scope and no new durable constraint is introduced.
- Append decisions for material choices that affect future implementation judgment.
- Append progress only for handoff state.
- Do not record minor wording, private naming, local cleanup, or transient review details.

## Promotion Rule

When a dynamic decision changes canonical behavior:

1. Record the decision under `spec-root/progress/decisions.md`.
2. Mark that a canonical update is required.
3. Update the stable docs in a spec revision.
4. Regenerate or revise affected phase briefs.

After promotion, stable docs contain the required behavior directly. The decision ID may remain as audit context; implementation agents read stable docs for the current requirements.
