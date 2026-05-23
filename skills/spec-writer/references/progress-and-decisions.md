# Progress and Decisions

## Binding Rules

- Dynamic records live under `spec-root/progress/`.
- `progress.md` records state points.
- `decisions.md` records spec gaps before code changes.
- Implementation agents write decisions when they encounter a spec gap.
- Coordinators or review agents write progress when they can judge status and handoff impact.
- When no coordinator or review agent exists, the implementation agent records minimal progress entries for phase start, phase finish, blocker introduced, and blocker cleared when those entries affect fresh-agent handoff.
- Fixture errata go through decisions. Implementation agents record the contradiction, keep frozen fixtures unchanged, and apply the fixture skip/block rule below.
- Entries must be concise. A decision is one to three lines when possible; a progress entry is one to two lines when possible. Use long form when compact form lacks audit clarity.
- Decisions are durable records for behavior-affecting gaps. Boundary reports are transient execution signals for boundary events.
- Progress must preserve fresh-agent entry. Later agents should be able to read the latest progress state and identify the current phase, blocker status, and next brief.
- Dynamic records are append-oriented. Preserve existing entries, corrections, and unrelated content outside the current responsibility.

## Current Pointer

Use `spec-root/CURRENT.md` for a new spec set. Keep these fields current:

```md
Current phase:
Current brief:
Progress file:
Decision file:
Blocked:
Next action:
```

For an existing spec set without `CURRENT.md`, keep the same fields in a latest-state block at the top of `progress.md`.

## `progress.md`

Record status points that help later agents align quickly:

- phase start
- phase finish
- milestone reached
- blocker introduced
- blocker cleared
- downstream entry condition changed
- verification status changed
- mainline adjustment that changes output shape, milestone position, or phase boundary

Use the listed status points as the progress surface. A correction that changes final output shape, milestone position, or downstream entry condition is a mainline adjustment.

Progress entries are append-style. A stale or wrong entry is corrected by appending a later status point; existing entries remain available for handoff audit.

Recommended format:

```md
- <date> | <phase> | <status point> | impact: <handoff impact> | next: <brief or condition>
```

Example:

```md
- 2026-05-23 | phase-01 status-map | milestone reached: status fixtures pass | impact: fulfillment phase may consume order state v1 | next: phase-02-fulfillment.md
```

## `decisions.md`

Record a decision when the spec has a gap for a detail needed before code can be written.

Required fields:

- phase
- source
- question
- decision
- reason
- canonical update flag

Preferred compact format:

```md
- DEC-0001 | phase=<phase> | source=<source> | question=<question> | decision=<decision> | reason=<reason> | canonical_update=<yes|no>
```

Use the expanded form when clarity requires it:

```md
## DEC-0001
Phase:
Source:
Question:
Decision:
Reason:
Canonical update required:
```

Use `Source` to identify the trigger:

- repo evidence
- fixture erratum
- missing component contract
- verification constraint
- phase brief ambiguity
- upstream guarantee mismatch
- generality boundary mismatch

The decision is written before implementation follows it. If the decision expands scope or changes canonical behavior, mark `Canonical update required: yes` and keep the implementation to the smallest safe step.

Decision precedence:

- Write a decision first when the gap affects behavior, public surface, fixture interpretation, edit boundaries, input guarantees, failure behavior, canonical meaning, or the brief's generality boundary.
- Use a boundary report for execution signals that preserve behavior, such as unavailable verification tooling or a skipped optional check.
- Ordinary private implementation choices remain inside the brief's contract, edit boundary, fixtures, and verification.
- A gap requiring resolution beyond the current phase boundary is blocked.

Decision entries are append-style. A superseded decision is followed by a new decision that references it; unrelated earlier decisions remain intact.

## Fixture Errata

Fixture contradictions are decisions:

```md
- DEC-0002 | phase=phase-01 status-map | source=fixture erratum | question=`order_status_cases.json` maps `paid` to `Pending`, canonical spec maps it to `Paid` | decision=skip affected fixture until spec or fixture revision | reason=frozen fixtures remain unchanged during implementation | canonical_update=yes
```

Fixture skip/block rule:

- Partial contradiction: record a decision and skip only the affected fixture when remaining fixtures still provide valid acceptance coverage.
- Sole or canonical acceptance contradiction: block the phase until the spec or fixture is revised.

## Responsibility Split

Implementation agent:

- appends decisions for spec gaps before coding through them
- appends fixture errata when frozen fixtures conflict with stable docs
- writes boundary reports when phase boundaries are crossed

Coordinator or review agent:

- writes progress entries for phase start, finish, milestone, blocker, or handoff changes
- promotes accepted decisions into stable docs through explicit spec revision
- revises affected phase briefs after stable docs change
