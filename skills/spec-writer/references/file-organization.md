# File Organization

## Purpose

Use this reference when creating or revising a spec document set. Its job is to make the repo-local file layout express the same thinking order: entry pointer, stable contracts, current brief, then sparse handoff records.

## Organization Thinking Frame

Build the file tree by answering these questions in order:

1. **Where does a fresh agent enter?**
   - Write `CURRENT.md` or the repo equivalent with current phase, current brief, blocker state, and next action.
2. **Which contracts are stable?**
   - Put settled behavior, component boundaries, public surfaces, phase plan, fixture semantics, and collaboration model under `spec-root/`.
3. **Which slice is executable now?**
   - Put current and planned phase briefs under `spec-root/briefs/` or the repo's established equivalent.
4. **Which records are dynamic?**
   - Put handoff-relevant progress and material decisions under `spec-root/progress/`.
5. **What is mutable?**
   - Mark stable docs, phase briefs, and frozen fixtures as read-only during implementation unless the current task authorizes spec revision.
6. **What must stay sparse?**
   - Keep progress and decisions focused on future execution judgment, not review chatter or transcript history.

## Recommended Layout

Use this layout when no existing repo convention is stronger:

```text
spec-root/
  CURRENT.md
  overview.md
  phase-plan.md
  fixtures.md
  components/
    <component>.md
  briefs/
    phase-01-<name>.md
    phase-02-<name>.md
  progress/
    progress.md
    decisions.md
```

Adapt names to the repo, but preserve fresh-agent entry and the stable/dynamic split.

## Current Pointer

`CURRENT.md` is the top-level dynamic entry pointer. Keep it short:

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

When an existing repo convention does not use `CURRENT.md`, keep the same fields in a latest-state block at the top of `progress/progress.md`.

## Stable Layer

The stable layer contains content that should change rarely after design settles:

- collaboration model for interactive spec-driven development
- goals and non-goals
- behavior target and implementation spine
- component responsibilities and ownership
- module boundaries and public API shape
- pipeline order and input guarantees
- state, lifecycle, and failure model
- phase plan and review insertion policy
- fixture index and acceptance semantics
- edit boundary policy for planned phases

Stable docs are canonical. They should read like settled design contracts, not meeting notes.

When spec correction is in scope, revise wrong, unclear, or poorly shaped canonical text directly. Record a decision first only when the change introduces or selects a new durable constraint not already captured by the corrected spec.

## Phase Brief Layer

`spec-root/briefs/` contains execution-facing briefs. Each brief is stable for its phase but narrow to its slice.

Each brief should be independently feedable to an implementation agent and should state:

- current phase goal
- spine/mainline position
- primary targets and frozen scope
- repo-required collateral policy
- current contract
- acceptance and verification
- handoff

During implementation, a phase brief is read-only unless the current task explicitly includes revising that brief. If correction is in scope, correct the brief directly for clarity or accuracy. Record a decision only for material future-facing choices.

## Dynamic Layer

`spec-root/progress/` contains sparse execution records:

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

After promotion, stable docs contain the binding behavior directly. The decision ID may remain as audit context; implementation agents read stable docs for the current contract.
