# Writing Principles

## Binding Rules

- Write execution-facing spec text as a binding contract.
- Use a top-down structure in every document: binding requirements first, scoped detail after.
- State the chosen behavior directly. Include purpose when it prevents implementation ambiguity.
- Be specific at the contract level and restrained at the implementation level.
- Put the executable path in component contracts and phase briefs; keep rationale brief and local to the binding choice.
- Use positive constraints: allowed files, frozen files, public surface, input guarantees, fixtures, and verification commands.
- State the intended generality boundary and implementation depth for local or limited-domain features.
- State pipeline position and upstream guarantees for each component or function when they affect implementation depth.
- Encode minimal-entity execution as brief structure and final review guidance.
- State important internal invariants positively; prefer repo-standard assertions for invariant violations when assertions are part of the local coding style.
- Write for capable implementation agents with finite attention; make constraints concrete enough that attention stays on coding rather than inferring architecture.
- Target a capability level rather than runtime-specific assumptions.
- Use minimal failure behavior by default: detect, report, stop.
- Put unsettled points in a deferred decision block with a current default and decision point.

## Contract Language

Use strong, binding language:

- `must` for required behavior
- `owns` for responsibility
- `receives` for inputs
- `returns` or `emits` for outputs
- `fails with` for failure behavior
- `frozen` for content that remains unchanged during implementation

Use deferred decision blocks for unsettled points. Use future phase briefs for future requirements. The current phase brief contains current requirements.

## Generality Boundary and Implementation Depth

Specify the intended depth of the implementation before mechanism details:

```md
Generality boundary:
Input domain:
Current scale:
Required mechanism:
Extension trigger:
Boundary note:
```

Use these fields to anchor small or repo-local features:

- `Generality boundary`: the feature serves the current repo, current workflow, and stated scenarios.
- `Input domain`: the inputs the component actually receives after upstream processing.
- `Current scale`: expected size, frequency, and complexity that matter for this phase.
- `Required mechanism`: the smallest named mechanism that satisfies the contract, such as table lookup, regex match, direct mapper, existing library call, or adapter.
- `Extension trigger`: the concrete future condition that would justify a broader mechanism.
- `Boundary note`: the scenario boundary that keeps the current phase at the stated mechanism depth.

The implementation target is the smallest repo-consistent mechanism that satisfies the stated contract, fixtures, and verification. Broader mechanisms require an explicit current-phase requirement or an accepted decision that changes the contract.

This section should be short. It prevents generic-system completion while preserving local implementation latitude.

## Minimal-entity Execution

Execution-facing text should make the smallest valid path easy to choose:

- before coding: identify the binding contract, allowed files, input guarantees, fixtures, and smallest sufficient mechanism
- during coding: add entities required to satisfy the current contract
- after coding: verify the public surface, abstraction depth, failure behavior, validation path, and phase capability match the brief

Encode this discipline as brief structure and final self-check rather than repeated meta-work.

## Right Level of Specificity

Specify the required contract and the implementation freedom that remains inside it.

The spec must fix:

- observable behavior
- public surface and integration points
- file-level edit boundaries
- pipeline position and input guarantees
- state, lifecycle, and failure contracts when visible
- fixture/table acceptance
- verification commands
- phase handoff condition

The spec may fix internal approach when it affects correctness, interoperability, performance, migration safety, or a public contract. In those cases, state the required property or selected mechanism and why it is binding.

Implementation latitude covers private helper names, local decomposition, and internal control flow when multiple local implementations satisfy the contract.

Leave ordinary private helper names, internal control flow, and local decomposition to the implementation agent, constrained by repo conventions, allowed files, fixtures, and verification.

Execution-facing specs should define contracts, not line-by-line patches. When a private implementation detail is contract-neutral, leave it as implementation latitude.

When a detail is discovered during implementation or after running checks, handle it through a deferred decision, a phase decision, or a blocker depending on whether the phase has a safe default.

## Component Contract Template

Use this shape for a component-level spec, or the repo's established stronger template:

```md
# <Component>

## Binding Requirements

- Role:
- Pipeline position:
- Input source:
- Upstream guarantees:
- Internal invariants:
- Generality boundary:
- Public surface:
- Success output:
- Failure behavior:
- State changes:
- Lifecycle:
- Constraints:
- Acceptance:

## Role

## Public Surface

## Input Guarantees

## Required Behavior

## State and Lifecycle

## Constraints

## Failure Behavior

## Acceptance Fixtures
```

The first section must be enough for an implementation agent to understand the contract. Later sections add precision within the same scope.

## Internal Invariants and Assertions

Use internal invariants to express important internal assumptions while keeping external behavior defined by the failure contract:

```md
Internal invariants:
- after <stage>, <condition> holds because <upstream guarantee or local step>
- assert <condition> at <internal boundary> if the repo uses assertions for invariant violations
```

Assertion guidance:

- assertions defend impossible internal states under the stated contract
- contract-defined invalid inputs use the specified failure behavior
- assertions preserve the stated mechanism depth and diagnostic shape

Keep this section short. It should make internal assumptions executable while keeping the external behavior contract stable.

## Contract Dimensions

Specify these dimensions when they affect implementation:

- scope and boundaries
- public objects, methods, commands, or files
- inputs and normalization state
- outputs and visible side effects
- state changes and persistence
- lifecycle, ownership, and cleanup boundaries
- error shape and failure stopping point
- performance, dependency, compatibility, or migration constraints
- acceptance fixtures and verification commands

When a dimension is handled outside the current phase, cite the owning phase or document.

## Pipeline Position and Input Guarantees

For pipeline stages, state exactly what has already happened upstream:

```md
Input source:
Upstream guarantees:
Local checks:
Out-of-contract input behavior:
```

Use upstream guarantees to prevent defensive implementation inflation. If input is already decoded, normalized, authenticated, parsed, or range-checked, say so.

## Failure Behavior

Default failure behavior:

```md
Detect the invalid condition, report the specified error shape, and stop the current operation.
```

Richer failure handling belongs in a dedicated failure-handling contract. A contract with an error shape and stopping point keeps failure behavior at that depth.

If failure behavior is implementation-visible and no repo convention supplies the error shape, the phase has a spec gap. Record a decision before implementation follows a chosen shape.

## Fixture-first Acceptance

Use concrete cases for behavior that affects implementation:

```md
| Input | Expected |
| --- | --- |
| `{ "status": "paid" }` | `OrderState.Paid` |
| `{ "status": "refunded" }` | `OrderState.Refunded` |
```

Natural language may summarize the rule, but fixtures or tables anchor the exact interpretation.

Mark fixture files as frozen in phase briefs. If a fixture conflicts with the canonical spec, record a fixture erratum in `spec-root/progress/decisions.md`; the fixture remains unchanged during implementation.

## Deferred Decisions

Unsettled points must be isolated and bounded:

```md
## Deferred Decision: <short name>

Phase:
Trigger:
Question:
Current phase default:
Allowed options:
Decision owner:
Decision point:
```

The current phase default is binding until the decision is made. A missing safe default makes the phase blocked.
