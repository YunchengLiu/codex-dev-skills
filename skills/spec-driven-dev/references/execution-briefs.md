# Execution Briefs

## Purpose

Use this reference when writing the current phase brief. A phase brief is an action guide for one implementation slice. It should be local enough to read before coding and structured enough that a fresh agent can execute the phase without chat history.

Do not restate the whole stable spec. Re-anchor only the facts needed to execute the current phase correctly.

## Implementation Discipline

Every implementation brief must convey these rules, either directly or through a repo-standard equivalent:

- Re-read and follow the applicable repo instructions and surrounding code before editing.
- Implement the settled requirements; re-derive production structure, naming, comments, and ordinary code choices from repo conventions and caller needs.
- Keep spec-only terminology, explanatory models, pseudocode, phase language, and illustrative implementation shape out of production code and comments unless they are part of the settled domain language.
- Treat fixtures and examples as representative acceptance evidence unless explicitly marked exhaustive; implement the stated rule over its declared input domain.
- Use the simplest repo-consistent implementation for the evidenced operating envelope; do not add hypothetical scale, concurrency, asynchronous coordination, recovery, compatibility, or extensibility machinery.

When repo evidence conflicts with settled behavior, a public requirement, or acceptance, report the material conflict instead of silently following either source. Differences in explanatory wording or illustrative structure are resolved in favor of repo-native implementation.

## Brief Thinking Frame

Write the brief in the order the implementation agent should think.

1. **Name the current goal.**
   - Ask: What single behavior surface, integration point, public requirement, fixture set, or cleanup boundary does this phase own?
   - Write: phase goal and review responsibility.
2. **Place the phase on the spine.**
   - Ask: Where is this phase in the behavior path, and what becomes executable after it?
   - Write: behavior target, task-shaped spine, owner/consumer/assembler, immediate upstream, immediate downstream, available prerequisites, present capability, and later work that is not required for current acceptance.
3. **Set the edit boundary policy.**
   - Ask: What are the primary anchors, tests/fixtures, repo-required collateral rules, frozen paths, and escalation conditions?
   - Write: primary targets, tests/fixtures, collateral policy, frozen scope, escalation rule, and reporting rule.
4. **Write the current requirements.**
   - Ask: What inputs, upstream guarantees, local responsibilities, outputs, invariants, and failure behavior are settled for this phase?
   - Write: the component or behavior requirements at design level.
5. **Bound implementation depth.**
   - Ask: What is the intended generality boundary and smallest repo-consistent mechanism?
   - Write: current input domain, mechanism depth, implementation latitude, and extension trigger.
6. **Anchor acceptance.**
   - Ask: What rule and input domain does the phase implement, and which fixture, table, command output, or check demonstrates it?
   - Write: the general acceptance rule followed by concrete `input -> expected` cases or fixture references; mark a case set exhaustive only when it defines a closed input set.
7. **Define execution protocol.**
   - Ask: What must the agent summarize before editing, when must it wait, and how does it verify?
   - Write: pre-coding summary fields, approval gate, verification commands, boundary reporting, and handoff.
8. **Run the phase gates.**
   - Ask: Is this phase review-sized, spine-ordered, non-helper-first, specified at design level, and sparse in records?
   - Write: a short minimal-entity check.

## Brief Template

Use this as an optional shape check. Omit irrelevant fields and repeated sections. A brief may be much shorter when the phase is clear without the full template.

```md
# Phase <N>: <Name>

## Required Work

- Goal:
- Review responsibility:
- Spine/mainline position:
- Primary targets:
- Tests/fixtures:
- Repo-required collateral policy:
- Frozen:
- Escalation rule:
- Input guarantees:
- Required behavior:
- Failure behavior:
- Facade/stub behavior:
- Acceptance:
- Verify:
- Handoff:
- Implementation discipline:
- Pre-coding summary:
- Approval gate:
- Read first:
- Read next:

## Current Spine Position

## Edit Boundary Policy

## Current Requirements

## Generality Boundary and Implementation Latitude

## Acceptance

## Verification

## Boundary Reporting

## Handoff
```

The `Required Work` section is the action table. Later sections add only the precision needed for this phase.

## Current Spine Position

State where the phase sits in the top-down implementation spine:

```md
Spine/mainline position:
- Behavior target:
- Task-shaped spine:
- Owner/consumer/assembler:
- Immediate upstream:
- Immediate downstream:
- Available prerequisites:
- Becomes executable:
- Later work not required for current acceptance:
```

The owner field adapts to the task: API handler, UI page or state owner, CLI command, migration coordinator, lifecycle root, pipeline assembler, compiler pass owner, or the repo's equivalent.

The first implementation action starts at the owner, consumer, assembler, coordinator, lifecycle root, or minimal executable spine for this phase. A private helper can be first only when the brief names the already-stable caller surface that consumes it, or when the task is an isolated repair under a frozen public surface.

Everything required for the phase acceptance must be available before implementation or land in the phase. Later work may extend or optimize a correct current capability. When the current mechanism is intentionally non-optimal, state its current guarantee, bounded limitation, and concrete extension trigger or next phase.

## Review Responsibility

Keep the phase review-sized:

```md
Review responsibility:
- one focused behavior, integration point, public requirement, fixture set, or cleanup boundary
- expected to land as one coherent commit unless repo practice requires otherwise
- no unrelated helper extraction, broad cleanup, or speculative abstraction
```

If a larger edit is indivisible, state the single responsibility that makes it indivisible.

## Edit Boundary Policy

Use explicit anchors and collateral rules:

```md
Primary targets:
- `src/orders/status_mapper.ts`

Tests/fixtures:
- `tests/orders/status_mapper.test.ts`

Repo-required collateral policy:
- allow minimal mechanical integration edits required by observed repo conventions, such as build/test registration or exports when the repo already uses that pattern

Frozen:
- `src/orders/payment_state.ts`
- `tests/fixtures/order_status_cases.json`

Escalation rule:
- stop or report a boundary when the needed edit broadens the phase, changes required behavior or fixture meaning, restructures unrelated systems, moves ownership across components, or is not clearly required by repo convention

Reporting:
- report any collateral edit in the implementation summary
```

For new development, primary targets may be planned paths. Repo-required collateral is allowed only when directly caused by the phase, required by observed repo conventions, minimal, mechanical, and behavior-neutral.

## Current Requirements

Write behavior as concrete obligations:

```md
The status mapper receives normalized payment status strings from the payment adapter. It returns the internal order state required by downstream fulfillment code.
```

State the requirement dimensions that affect implementation:

- role and responsibility
- input source and upstream guarantees
- local checks and internal invariants
- success output or visible side effect
- failure behavior and stopping point
- state or lifecycle changes
- public surface, command, file, or data format when visible

Keep private helper names, helper decomposition, and line-level edit strategy out of the brief unless they are public or repo-conventional.

The brief's terminology and design model guide understanding; they are not names or comments to copy into production. Public API and source documentation must be written for their actual repo audience and remain understandable without the spec.

## Facade and Stub Boundaries

Use a facade or stub only when the current acceptance is limited to proving the owning or integration path and does not require the deferred semantic capability. A stub must not stand in for behavior needed to make the phase's claimed domain result correct:

```md
Facade/stub behavior:
- path and public surface:
- behavior present now:
- behavior intentionally absent:
- verification that still applies:
- fill-in phase:
```

Keep the facade or stub inside the owning boundary. Do not create broad extension points unless the stable spec requires them.

## Generality Boundary and Implementation Latitude

State implementation depth in positive terms:

```md
Generality boundary:
- repo-local or limited-domain behavior for <scenario>
- inputs come from <upstream source>
- scale is <current expected size/frequency>

Implementation depth:
- use the smallest repo-consistent mechanism that satisfies fixtures and verification
- broaden only when <explicit extension trigger> occurs

Implementation latitude:
- private helper names and local function decomposition
- internal control flow that preserves the required behavior
- small repo-consistent refactors inside the edit boundary policy
```

State scale, concurrency, lifecycle, compatibility, and recovery assumptions only when supported by the request or repo. Do not turn internal helpers into independent compatibility surfaces or add synchronization, asynchronous flows, recovery paths, state machines, caching, or large-scale optimization without an evidenced need.

This preserves freedom inside the stated requirements, edit boundary, fixtures, and verification.

## Acceptance

State the behavior rule and declared input domain before the examples. Treat cases as representative unless explicitly marked exhaustive.

Use fixture/table acceptance for behavior that affects implementation:

```md
| Input | Expected |
| --- | --- |
| `paid` | `OrderState.Paid` |
| `refunded` | `OrderState.Refunded` |
```

Concrete cases anchor interpretation but do not replace the rule. Implementation and verification cover relevant normal, boundary, and failure cases implied by the rule and repo context. Mark frozen fixture files in the edit boundary policy.

## Pre-Coding Summary

For interactive spec-driven development, state what the implementation agent must summarize before editing:

```md
Pre-coding summary:
- current phase goal
- spine/mainline position
- edit boundary policy
- frozen paths
- acceptance and verification
- first implementation action
- expected review surface
- approval gate
```

This makes execution explicit without prescribing private code structure.

## Boundary Reporting

Boundary reports are one-line, grep-able execution signals for defined boundary conditions:

```text
SPEC_BOUNDARY: phase=<phase>; path=<path>; reason=<reason>; action=<continue|skip|blocked>
```

Report when:

- implementation requires work beyond the edit boundary policy
- repo-required collateral expands beyond minimal mechanical integration
- a frozen fixture contradicts the canonical spec
- repo evidence contradicts a stated input guarantee
- verification is unavailable for a repo-specific reason
- a material spec gap needs a decision before code can be written

Use actions precisely:

- `continue`: the boundary condition preserves behavior and the brief already defines a safe path
- `skip`: a frozen fixture or optional verification path is skipped and recorded
- `blocked`: behavior, public surface, fixture interpretation, edit boundary, input guarantee, failure behavior, or generality boundary needs resolution

If the issue is wrong or unclear spec text and spec correction is in scope, correct the canonical spec or brief directly. Record a decision only for a material durable choice.

## Handoff

End the brief with the handoff condition:

```md
Handoff:
- complete when:
- verification required:
- next brief:
- mainline return:
- blocker state:
```

A fresh agent should be able to read the current pointer, this brief, latest progress state, and code, then know the next action.

## Minimal-entity Check

Use this as the final phase self-check:

```md
Minimal-entity check:
- current requirements are satisfied at the stated mechanism depth
- implementation starts from the stated spine position
- current acceptance does not depend on future-phase behavior
- later work only extends or optimizes a correct current capability
- production code and comments are repo-native and do not transcribe spec-only models or wording
- public surface, abstraction depth, failure behavior, validation path, and phase capability match the brief
- the stated behavior and input domain are implemented; fixtures remain concrete acceptance evidence rather than the implementation boundary
```
