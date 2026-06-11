# Progress and Decisions

## Purpose

Use this reference when defining or updating `spec-root/progress/`. Progress and decisions are sparse handoff records. They help a future agent know current state and material durable choices; they are not conversation logs.

## Record Thinking Frame

Before writing any progress or decision entry, ask these questions in order:

1. **Is canonical text wrong or unclear?**
   - If spec revision is in scope and no new durable choice is needed, correct the stable doc or brief directly.
2. **Does the change affect handoff state?**
   - If it changes current phase, blocker state, verification state, downstream entry, milestone, mainline return, or next action, append progress.
3. **Does the change introduce or select a durable constraint?**
   - If it affects behavior, public surface, fixture interpretation, edit boundary, input guarantee, failure behavior, canonical meaning, generality boundary, phase order, or mainline return, append a decision before implementation follows it.
4. **Is it only local implementation detail or review chatter?**
   - Do not record private naming, helper decomposition, local cleanup, wording polish, transient discussion, or small review corrections that do not change future implementation judgment.
5. **Is the phase blocked?**
   - If a material choice has no safe current-phase default, mark the phase blocked in the current pointer and progress state.

## Current Pointer

Use `spec-root/CURRENT.md` for a new spec set. Keep these fields current:

```md
Current phase:
Current brief:
Progress file:
Decision file:
Blocked:
Next action:
Mainline return:
```

For an existing spec set without `CURRENT.md`, keep the same fields in a latest-state block at the top of `progress.md`.

## `progress.md`

Progress records state points that affect fresh-agent handoff.

Record:

- phase start or finish when it changes handoff
- milestone reached
- blocker introduced or cleared
- downstream entry condition changed
- verification status changed
- mainline adjustment that changes output shape, milestone position, or phase boundary
- review-time insertion started or finished, with the mainline return point

Do not record:

- ordinary wording or heading fixes
- private member/helper naming feedback
- local cleanup choices
- transient review discussion
- temporary work that starts and finishes without changing blocker state, verification state, phase boundary, or mainline return

Recommended compact format:

```md
- <date> | <phase> | <status point> | impact: <handoff impact> | next: <brief or condition>
```

Example:

```md
- 2026-05-23 | phase-01 status-map | milestone reached: status fixtures pass | impact: fulfillment phase may consume order state v1 | next: phase-02-fulfillment.md
```

Progress entries are append-style. Correct stale entries by appending a later status point; preserve existing unrelated content.

## `decisions.md`

Write a decision when implementation needs a material choice before code can proceed and that choice affects future implementation judgment.

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

Use expanded form when clarity requires it:

```md
## DEC-0001

Phase:
Source:
Question:
Decision:
Reason:
Canonical update required:
```

Use `Source` to identify the material trigger:

- repo evidence
- fixture erratum
- missing component contract
- verification constraint
- phase brief ambiguity
- upstream guarantee mismatch
- generality boundary mismatch
- mainline return mismatch

Decision precedence:

- Write the decision before implementation follows it.
- Mark `canonical_update=yes` when the decision changes stable behavior or should be promoted into stable docs.
- Do not write a decision for a spec correction that simply makes canonical text match the intended current contract. Correct the canonical doc instead.
- Use boundary reports for execution signals that preserve behavior, such as unavailable optional verification tooling.
- Ordinary private implementation choices remain inside the brief's contract, edit boundary, fixtures, and verification.

A gap requiring resolution beyond the current phase boundary blocks the phase.

Decision entries are append-style. A superseded decision is followed by a new decision that references it; unrelated earlier decisions remain intact.

## Fixture Errata

Fixture contradictions are material decisions:

```md
- DEC-0002 | phase=phase-01 status-map | source=fixture erratum | question=`order_status_cases.json` maps `paid` to `Pending`, canonical spec maps it to `Paid` | decision=skip affected fixture until spec or fixture revision | reason=frozen fixtures remain unchanged during implementation | canonical_update=yes
```

Fixture skip/block rule:

- Partial contradiction: record a decision and skip only the affected fixture when remaining fixtures still provide valid acceptance coverage.
- Sole or canonical acceptance contradiction: block the phase until the spec or fixture is revised.

## Spec Correction vs Decision

Use this gate:

```text
Can the corrected canonical spec stand alone for the next agent?
```

If yes, correct the stable doc or brief directly and do not add a decision. If no, record the durable choice or blocked state that future agents must know.

Examples that should not become decisions:

- rewording a brief so the current contract is clearer
- renaming a private helper or member in review feedback
- moving a section to match the template
- deleting noisy history
- correcting a typo or ambiguous sentence without changing behavior

Examples that should become decisions:

- selecting an error shape not supplied by repo convention
- changing fixture interpretation
- expanding or narrowing a public surface
- changing phase order or mainline return
- changing input guarantees, failure behavior, edit boundary, or generality boundary

## Responsibility Split

Implementation agent:

- appends decisions for material spec gaps before coding through them
- appends fixture errata when frozen fixtures conflict with stable docs
- writes boundary reports when phase boundaries are crossed
- writes minimal progress only when no coordinator exists and handoff state changes

Coordinator or review agent:

- writes progress entries for phase start, finish, milestone, blocker, verification, or handoff changes
- promotes accepted decisions into stable docs through explicit spec revision
- revises affected phase briefs after stable docs change

## Sparse Record Check

Before finishing, ask:

- Can a fresh agent identify current phase, blocker state, current brief, and next action?
- Are decisions limited to material durable choices?
- Are ordinary corrections reflected directly in canonical text?
- Are progress entries limited to handoff-relevant state?
- Can future execution proceed without reading chat history?
