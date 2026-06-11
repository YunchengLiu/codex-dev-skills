# Writing Principles

## Purpose

Use this reference when writing stable contracts, component contracts, acceptance text, failure behavior, generality boundaries, or deferred decisions.

Spec prose should guide structured implementation thinking. It should make the smallest correct path easy to choose and make speculative implementation depth feel out of place.

## Contract Thinking Frame

Write each contract in this order:

1. **Role.**
   - Ask: What does this component, command, file, or phase own?
   - Write: role and responsibility in one or two concrete statements.
2. **Position.**
   - Ask: Where does it sit in the implementation spine or pipeline?
   - Write: upstream source, upstream guarantees, local responsibility, downstream consumer.
3. **Public surface.**
   - Ask: What names, paths, commands, data formats, APIs, or fixtures must remain stable across agents?
   - Write: only the externally visible or repo-contractual surface.
4. **Behavior.**
   - Ask: What must happen for valid inputs, visible state, lifecycle, outputs, and side effects?
   - Write: direct obligations, not rationale-heavy commentary.
5. **Failure.**
   - Ask: What invalid condition is detected, what error shape is reported, and where does execution stop?
   - Write: minimal failure behavior unless a richer failure contract is explicitly required.
6. **Generality boundary.**
   - Ask: Is this repo-local, limited-domain, or general-purpose?
   - Write: input domain, current scale, required mechanism, and extension trigger.
7. **Acceptance.**
   - Ask: Which concrete cases will two agents interpret the same way?
   - Write: fixture references or `input -> expected` tables.
8. **Implementation latitude.**
   - Ask: What remains a private implementation choice inside the contract?
   - Write: allowed latitude so the spec does not over-own private code.

## Design Contract Boundary

The spec owns design decisions that must remain stable across implementation agents:

- observable behavior and acceptance
- public surfaces, commands, data formats, stable file paths, and externally visible names
- component responsibilities and ownership
- phase order, edit boundaries, verification, and handoff
- invariants, failure behavior, and input guarantees
- pseudocode-level algorithm intent when it prevents ambiguity

The spec does not own ordinary private implementation shape:

- private class, method, variable, or helper names
- helper decomposition
- local control flow that is contract-neutral
- line-level edit strategy
- repo-style decisions already governed by surrounding code
- abstractions that exist only to make a local micro-task convenient

When a concrete code shape seems necessary, first ask whether it is actually a public contract, an observed repo convention, or a design simplification issue. Only public or contract-relevant choices belong in the stable spec.

## Contract Language

Use strong, direct language:

- `must` for required behavior
- `owns` for responsibility
- `receives` for inputs
- `returns` or `emits` for outputs
- `fails with` for failure behavior
- `frozen` for content that remains unchanged during implementation

Use future phase briefs for future requirements. Keep the current phase brief focused on current requirements.

## Right Level of Specificity Gate

Before finalizing contract text, ask:

- Does it fix observable behavior, public surface, integration point, edit boundary, input guarantee, fixture, verification, and handoff?
- Does it avoid private helper names, helper decomposition, exact control flow, and line-level edits when those are contract-neutral?
- Does it specify repo conventions by reference to observed repo practice instead of copying or guessing them?
- Does any pseudocode communicate algorithm intent rather than forcing concrete code structure?
- Would two capable agents produce materially similar behavior while retaining local implementation freedom?

Pass when the spec is precise about behavior and restrained about private mechanics.

## Generality Boundary and Implementation Depth

Specify the intended depth before mechanism details:

```md
Generality boundary:
Input domain:
Current scale:
Required mechanism:
Extension trigger:
Boundary note:
```

Use these fields to anchor small or repo-local features:

- `Generality boundary`: the feature serves the current repo, workflow, and stated scenarios.
- `Input domain`: the inputs the component receives after upstream processing.
- `Current scale`: expected size, frequency, and complexity that matter for this phase.
- `Required mechanism`: the smallest named mechanism that satisfies the contract, such as table lookup, regex match, direct mapper, existing library call, or adapter.
- `Extension trigger`: the concrete future condition that would justify broadening.
- `Boundary note`: the scenario boundary that keeps this phase at the stated depth.

Broader mechanisms require an explicit current-phase requirement or an accepted decision that changes the contract.

## Minimal-entity Execution

Encode this discipline as brief structure and final review guidance:

- before coding: identify the binding contract, edit boundary policy, input guarantees, fixtures, and smallest sufficient mechanism
- during coding: add only entities required to satisfy the current contract
- after coding: verify public surface, abstraction depth, failure behavior, validation path, and phase capability against the brief

Do not repeat this as generic prose in every section. Use it where it changes implementation judgment.

## Component Contract Template

Use this shape for a component-level spec, or the repo's stronger established template:

```md
# <Component>

## Binding Requirements

- Role:
- Spine/pipeline position:
- Input source:
- Upstream guarantees:
- Local checks:
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

## Failure Behavior

## Acceptance
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

Richer failure handling belongs in a dedicated failure-handling contract. If failure behavior is implementation-visible and no repo convention supplies the error shape, the phase has a material spec gap.

## Fixture-first Acceptance

Use concrete cases for behavior that affects implementation:

```md
| Input | Expected |
| --- | --- |
| `{ "status": "paid" }` | `OrderState.Paid` |
| `{ "status": "refunded" }` | `OrderState.Refunded` |
```

Natural language may summarize the rule, but fixtures or tables anchor exact interpretation.

Mark fixture files as frozen in phase briefs. If a fixture conflicts with the canonical spec, record a fixture erratum in `spec-root/progress/decisions.md`; the fixture remains unchanged during implementation.

## Deferred Decisions

Use deferred decisions only for material unsettled points:

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

The current phase default is binding until the decision is made. A missing safe default blocks the phase.

Do not create deferred decisions for minor wording fixes, member/helper naming feedback, local cleanup, or review corrections that do not change behavior, public surface, acceptance, phase order, edit boundaries, input guarantees, failure behavior, or generality boundary.
