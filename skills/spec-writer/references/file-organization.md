# File Organization

## Binding Rules

- Use `spec-root/` for stable, low-frequency spec content.
- Use `spec-root/progress/` for dynamic execution records.
- Keep phase execution briefs under `spec-root/briefs/`; use the repo's established convention when it is clearer.
- Stable docs contain canonical behavior directly and may cite promoted decisions by ID.
- Promote a dynamic decision into stable docs through an explicit spec revision.
- The spec set must have a clear fresh-agent entry path: current pointer, stable plan, current brief, and progress status.
- Every document starts with a concise requirements summary, then scoped detail.
- Stable docs, phase briefs, and frozen fixtures are read-only to implementation agents unless the current phase explicitly authorizes a spec revision.
- Dynamic records are append-oriented. Preserve existing entries and content outside the current responsibility.

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

Adapt names to the repo, but preserve the stable/dynamic split.

`CURRENT.md` is the top-level dynamic entry pointer. Keep it short:

```md
# Current

Current phase:
Current brief:
Progress file:
Decision file:
Blocked:
Next action:
```

When an existing repo convention does not use `CURRENT.md`, keep the same fields at the top of `progress/progress.md`.

## Stable Layer

The stable layer contains the content that should change rarely after design settles:

- goals and non-goals
- component responsibilities
- module boundaries
- public API shape
- pipeline order and input guarantees
- state and lifecycle model
- phase plan
- fixture index and acceptance semantics
- edit boundary policy for planned phases

Stable docs are the canonical source of truth. They read like settled decisions.

Stable docs are changed through explicit spec revision. A phase that needs a canonical change records the decision first, then updates the stable docs only when that spec-revision work is in scope.

## Phase Brief Layer

`spec-root/briefs/` contains execution-facing briefs. A brief is stable for the phase it describes, but it is intentionally narrow.

Each brief should be independently feedable to an implementation agent and list the supporting docs needed for that phase.

During implementation, a phase brief is read-only unless the current task explicitly includes revising that brief. When a brief is wrong or incomplete, record the gap in `progress/decisions.md` before changing behavior.

## Dynamic Layer

`spec-root/progress/` contains execution-time records:

- phase starts and finishes
- milestone status
- blockers that affect handoff
- downstream entry condition changes
- mainline adjustments
- decisions for spec gaps
- fixture errata

Dynamic records are concise append-style operational history for state points and spec-gap decisions.

The latest progress state should let a new agent identify the current phase, blocker status, and next brief from repo-local docs.

Dynamic records preserve audit history. Append new entries for new decisions or state points. Corrections are new entries that reference the earlier entry; existing unrelated content stays intact.

## Promotion Rule

When a dynamic decision changes canonical behavior:

1. Record the decision under `spec-root/progress/decisions.md`.
2. Mark that a canonical update is required.
3. Update the stable docs in a spec revision.
4. Regenerate or revise affected phase briefs.

Behavior-changing decisions are promoted through stable docs before they become canonical implementation guidance.

After promotion, stable docs contain the binding behavior directly. The decision ID may remain as audit context; implementation agents read the stable docs for the current contract.
