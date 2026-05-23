# Execution Briefs

## Binding Rules

- A phase brief is an action reference for one implementation slice.
- Include the current phase's goal, edit boundaries, local contract, fixtures, and verification commands.
- Include current-phase component contracts, local rationale, and directly relevant component boundaries.
- Make the brief usable as a fresh-agent entry point from a short repo-local prompt.
- Use file-level allowlists and frozen declarations.
- Preserve implementation latitude for private mechanics inside the contract.
- State the generality boundary and intended implementation depth.
- Include minimal-entity execution guidance as final review structure.
- Include internal invariants when they affect implementation correctness; prefer repo-standard assertions for those invariants.
- State input guarantees and minimal failure behavior.
- State out-of-contract input behavior when upstream guarantees affect implementation depth.
- Use fixture/table acceptance for behavior that affects implementation.
- Use lightweight boundary reports for defined boundary conditions.

## Brief Template

Use the template as a shape check, not as a requirement to keep empty headings. Keep the brief short enough to read before coding. Omit irrelevant conditional fields when omission does not create ambiguity.

```md
# Phase <N>: <Name>

## Binding Requirements

- Goal:
- Allowed to create:
- Allowed to modify:
- Frozen:
- Input guarantees:
- Required behavior:
- Failure behavior:
- Fixtures:
- Verify:
- Handoff:
- Read first:
- Read next:

## Conditional Requirements

- Out-of-contract input behavior:
- Internal invariants:
- Generality boundary:
- Implementation depth:
- Implementation latitude:
- Boundary reporting:

## Local Context

## Fresh-agent Entry

## Edit Boundary

## Component Contract

## Internal Invariants

## Generality Boundary

## Implementation Latitude

## Minimal-entity Check

## Acceptance Fixtures

## Verification

## Boundary Reporting
```

The `Binding Requirements` section is the phase's action table. Conditional requirements are included when they affect implementation depth, failure behavior, handoff, or fresh-agent entry.

## Fresh-agent Entry

A brief must work when a new agent is started in the repo with a short prompt such as "read the spec and plan the next step." The brief provides its own entry context.

State:

- the current phase name
- the first files to read
- the next brief or progress file to read after handoff
- deferred files for later phases or verification fallback
- the first implementation action
- the handoff condition for the next agent

Keep this section operational. It routes attention with phase facts.

## Internal Invariants

Use this section for important internal conditions:

```md
Internal invariants:
- <condition> holds after <stage>; assert if violated according to repo convention
```

These assertions defend the phase contract and preserve the stated external input handling and failure behavior.

## Generality Boundary

State the current implementation depth in positive terms:

```md
Generality boundary:
- repo-local or limited-domain behavior for <scenario>
- inputs come from <upstream source>
- scale is <current expected size/frequency>

Implementation depth:
- use the smallest repo-consistent mechanism that satisfies fixtures and verification
- broaden when <explicit extension trigger> occurs
```

State the mechanism depth required now and the trigger that would justify broadening it.

## Implementation Latitude

State what the implementation agent may decide locally as contract-bounded latitude:

```md
Implementation latitude:
- private helper names and local function decomposition
- internal control flow that preserves token order and error shape
- small repo-consistent refactors inside allowed files
```

This section preserves freedom inside the already stated contract, edit boundary, fixtures, and verification.

## Minimal-entity Check

Use a short final review pass:

```md
Minimal-entity check:
- current contract satisfied with the stated mechanism depth
- public surface, abstraction depth, failure behavior, validation path, and phase capability match the brief
- fixtures and verification remain the acceptance authority
```

This check guides implementation and final review as a final pass after local edits are complete.

## Edit Boundary

Use explicit paths:

```md
Allowed to create:
- `src/orders/status_mapper.ts`
- `tests/orders/status_mapper.test.ts`

Allowed to modify:
- `src/orders/index.ts`

Frozen:
- `src/orders/payment_state.ts`
- `tests/fixtures/order_status_cases.json`
```

For new development, use planned paths for files that will be created.

## Local Context

Keep local context narrow:

- current component role
- immediate upstream source
- immediate downstream consumer
- existing repo conventions needed to implement this phase

Reference other components by name and boundary. Include a full component contract when the current phase implements that component.

## Required Behavior

Write behavior as concrete obligations:

```md
The status mapper receives normalized payment status strings from the payment adapter. It returns the internal order state required by downstream fulfillment code.
```

Then anchor interpretation with fixtures:

```md
| Input | Expected |
| --- | --- |
| `paid` | `OrderState.Paid` |
| `refunded` | `OrderState.Refunded` |
```

## Boundary Reporting

Boundary reports are one-line, grep-able execution signals for defined boundary conditions.

Decisions are durable records. Boundary reports are transient signals. If a gap affects behavior, public surface, fixture interpretation, edit boundaries, or input guarantees, append a decision before implementing through it.

Emit boundary reports in the implementation summary or final response for the phase. Copy the substance into `progress/decisions.md` when the boundary affects behavior, public surface, fixture interpretation, edit boundaries, input guarantees, failure behavior, canonical meaning, or generality boundary. Verification-tool unavailability or another local execution signal stays in the summary unless it changes handoff state.

Use this format:

```text
SPEC_BOUNDARY: phase=<phase>; path=<path>; reason=<reason>; action=<continue|skip|blocked>
```

Report when:

- implementation requires a file beyond the allowed edit set
- a frozen fixture contradicts the canonical spec
- a spec gap needs a decision before code can be written
- repo evidence contradicts a stated input guarantee
- verification is unavailable for a repo-specific reason

Use actions precisely:

- `continue`: the boundary condition preserves behavior and the brief already defines a safe path
- `skip`: a frozen fixture or optional verification path is skipped and recorded
- `blocked`: behavior, public surface, fixture interpretation, edit boundary, or input guarantee requires resolution inside the current brief

Use `action=blocked` for an unresolved decision required before code can be written.
