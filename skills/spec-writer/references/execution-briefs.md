# Execution Briefs

## Purpose

Use this reference when writing the current phase brief. A phase brief is an action contract for one implementation slice. It should be local enough to read before coding and structured enough that a fresh agent can think through the phase without chat history.

Do not restate the whole stable spec. Re-anchor only the facts needed to execute the current phase correctly.

## Brief Thinking Frame

Write the brief in the order the implementation agent should think.

1. **Name the current goal.**
   - Ask: What single behavior surface, integration point, contract, fixture set, or cleanup boundary does this phase own?
   - Write: phase goal and review responsibility.
2. **Place the phase on the spine.**
   - Ask: Where is this phase in the behavior path, and what becomes executable after it?
   - Write: behavior target, task-shaped spine, owner/consumer/assembler, immediate upstream, immediate downstream, present capability, and later fill-in.
3. **Set the edit boundary policy.**
   - Ask: What are the primary anchors, tests/fixtures, repo-required collateral rules, frozen paths, and escalation conditions?
   - Write: primary targets, tests/fixtures, collateral policy, frozen scope, escalation rule, and reporting rule.
4. **Write the current contract.**
   - Ask: What inputs, upstream guarantees, local responsibilities, outputs, invariants, and failure behavior are binding for this phase?
   - Write: component or behavior contract at design-contract level.
5. **Bound implementation depth.**
   - Ask: What is the intended generality boundary and smallest repo-consistent mechanism?
   - Write: current input domain, mechanism depth, implementation latitude, and extension trigger.
6. **Anchor acceptance.**
   - Ask: Which fixture, table, command output, or check proves the phase behavior?
   - Write: concrete `input -> expected` cases or fixture references.
7. **Define execution protocol.**
   - Ask: What must the agent summarize before editing, when must it wait, and how does it verify?
   - Write: pre-coding summary fields, approval gate, verification commands, boundary reporting, and handoff.
8. **Run the phase gates.**
   - Ask: Is this phase review-sized, spine-ordered, non-helper-first, contract-level, and sparse in records?
   - Write: a short minimal-entity check.

## Brief Template

Use this as a shape check. Omit irrelevant conditional fields when omission does not create ambiguity.

```md
# Phase <N>: <Name>

## Binding Requirements

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
- Pre-coding summary:
- Approval gate:
- Read first:
- Read next:

## Current Spine Position

## Edit Boundary Policy

## Current Contract

## Generality Boundary and Implementation Latitude

## Acceptance

## Verification

## Boundary Reporting

## Handoff
```

The `Binding Requirements` section is the action table. Later sections add only the precision needed for this phase.

## Current Spine Position

State where the phase sits in the top-down implementation spine:

```md
Spine/mainline position:
- Behavior target:
- Task-shaped spine:
- Owner/consumer/assembler:
- Immediate upstream:
- Immediate downstream:
- Becomes executable:
- Later fill-in:
- Dependency role: locate missing repo evidence, prove the main path, stabilize
  a contract, unblock integration, or preserve behavior during migration:
```

The owner field adapts to the task: API handler, UI page or state owner, CLI command, migration coordinator, lifecycle root, pipeline assembler, compiler pass owner, or the repo's equivalent.

The first implementation action starts at the owner, consumer, assembler, coordinator, lifecycle root, or minimal executable spine for this phase. A private helper can be first only when the brief names the already-stable caller contract that consumes it, or when the task is an isolated repair under a frozen public surface.

## Review Responsibility

Keep the phase review-sized:

```md
Review responsibility:
- one focused behavior, integration point, contract, fixture set, or cleanup boundary
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
- stop or report a boundary when the needed edit broadens the phase, changes contract or fixture meaning, restructures unrelated systems, moves ownership across components, or is not clearly required by repo convention

Reporting:
- report any collateral edit in the implementation summary
```

For new development, primary targets may be planned paths. Repo-required collateral is allowed only when directly caused by the phase, required by observed repo conventions, minimal, mechanical, and behavior-neutral.

## Current Contract

Write behavior as concrete obligations:

```md
The status mapper receives normalized payment status strings from the payment adapter. It returns the internal order state required by downstream fulfillment code.
```

State the contract dimensions that affect implementation:

- role and responsibility
- input source and upstream guarantees
- local checks and internal invariants
- success output or visible side effect
- failure behavior and stopping point
- state or lifecycle changes
- public surface, command, file, or data format when visible

Keep private helper names, helper decomposition, and line-level edit strategy out of the contract unless they are public or repo-conventional.

## Facade and Stub Boundaries

Use a facade or stub only when it keeps the current spine executable while a real dependency waits for a later phase:

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
- internal control flow that preserves the contract
- small repo-consistent refactors inside the edit boundary policy
```

This preserves freedom inside the stated contract, edit boundary, fixtures, and verification.

## Acceptance

Use fixture/table acceptance for behavior that affects implementation:

```md
| Input | Expected |
| --- | --- |
| `paid` | `OrderState.Paid` |
| `refunded` | `OrderState.Refunded` |
```

Natural language may summarize the rule, but concrete cases anchor interpretation. Mark frozen fixture files in the edit boundary policy.

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
- current contract is satisfied at the stated mechanism depth
- implementation starts from the stated spine position
- no future-phase behavior was pulled forward
- public surface, abstraction depth, failure behavior, validation path, and phase capability match the brief
- fixtures and verification remain the acceptance authority
```
