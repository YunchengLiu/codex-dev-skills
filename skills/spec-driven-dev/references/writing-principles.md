# Writing Principles

## Purpose

Use this reference when writing stable requirements, component designs, acceptance text, failure behavior, generality boundaries, or deferred decisions.

Spec prose should state the settled design clearly enough for repo-native implementation. Apply Occam's razor: use the shortest rigorous explanation that preserves the decisions needed for correct implementation, and stop when additional wording no longer changes implementation or verification judgment. Do not introduce labels, categories, distinctions, or definitions that do not change behavior, design choice, or validation.

## Design Authority and Production Translation

The spec is authoritative for settled architecture, design intent, observable behavior, explicit public APIs and formats, constraints, and acceptance semantics. Its prose, explanatory models, examples, pseudocode, section labels, and suggested private structure are not production artifacts.

Implementation agents re-derive production code and documentation from the settled requirements, applicable repo instructions, surrounding code, and caller needs. Keep spec-only terminology and models out of production types, identifiers, public APIs, and source comments unless they are established or explicitly settled domain concepts. Authoring terms such as `contract`, `binding`, `spine`, `phase`, and `gate` must not become production vocabulary merely because the spec uses them.

Public API documentation must stand on its own for a caller who has not read the spec. State what the caller can do and the observable semantics needed for correct use. Explain copy, ownership, lifetime, concurrency, or failure properties only when their caller-visible meaning is not evident from the declaration and repo conventions.

## Design Requirement Thinking Frame

Consider each applicable design area in this order:

1. **Role.**
   - Ask: What does this component, command, file, or phase own?
   - Write: role and responsibility in one or two concrete statements.
2. **Position.**
   - Ask: Where does it sit in the implementation spine or pipeline?
   - Write: upstream source, upstream guarantees, local responsibility, downstream consumer.
3. **Public surface.**
   - Ask: What names, paths, commands, data formats, APIs, or fixtures must remain stable across agents?
   - Write: only the externally visible or repo-required surface.
4. **Behavior.**
   - Ask: What must happen for valid inputs, visible state, lifecycle, outputs, and side effects?
   - Write: direct obligations, not rationale-heavy commentary.
5. **Failure.**
   - Ask: What invalid condition is detected, what error shape is reported, and where does execution stop?
   - Write: minimal failure behavior unless richer failure semantics are explicitly required.
6. **Generality boundary.**
   - Ask: Is this repo-local, limited-domain, or general-purpose?
   - Write: input domain, current scale, required mechanism, and extension trigger.
7. **Acceptance.**
   - Ask: Which concrete cases will two agents interpret the same way?
   - Write: fixture references or `input -> expected` tables.
8. **Implementation latitude.**
   - Ask: What remains a private implementation choice inside the settled requirements?
   - Write: allowed latitude so the spec does not over-own private code.

Use this frame as a reasoning checklist, not a required document structure. Write only the dimensions that materially constrain the current design.

## Design and Implementation Boundary

The spec owns design decisions that must remain stable across implementation agents:

- observable behavior and acceptance
- public surfaces, commands, data formats, stable file paths, and externally visible names
- component responsibilities and ownership
- phase order, edit boundaries, verification, and handoff
- invariants, failure behavior, and input guarantees
- algorithm intent when it prevents ambiguity

Repo instructions, standard build or review workflows, ordinary style rules, and environment-specific absolute paths are implementation context rather than spec content. Reference an authoritative repo-relative source only when the task needs the reader to locate it. Restate a repo rule only when the spec defines a task-specific exception or the rule materially changes this design.

The spec does not own ordinary private implementation shape:

- private class, method, variable, or helper names
- helper decomposition
- local control flow that does not change required behavior
- line-level edit strategy
- repo-style decisions already governed by surrounding code
- abstractions that exist only to make a local micro-task convenient

When a concrete code shape seems necessary, first ask whether it is an explicitly settled public requirement, an observed repo convention, or a design simplification issue. Only public or otherwise design-relevant choices belong in the stable spec.

Use production-shaped code only to quote a relevant existing declaration or an explicitly settled exact public requirement. Identify the source or reason and include only the necessary fragment. Express other design content through responsibilities, flows, state transitions, data shapes, formulas, and language-neutral algorithm steps. Do not use complete class declarations, private members, helper layouts, or implementation bodies to make a broad requirement appear settled.

An explanatory model may use terms such as tree, node, leaf, range, stage, or spine when they improve design understanding. Mark the model as explanatory when those terms are not part of the established domain language. The implementation must preserve the modeled behavior, not the model's vocabulary or illustrative structure.

## Responsibility and Entity Boundaries

Treat separately described responsibilities as design analysis, not a required mapping to production entities. Derive types, interfaces, and files from settled requirements, repo conventions, and actual ownership and dependency boundaries.

Keep behavior and state together when they share ownership, lifecycle, invariants, and reasons to change. Separate them when doing so establishes an independently meaningful behavioral, data, ownership, lifecycle, dependency, or integration boundary. Evaluate the total structure: a new entity must improve responsibility clarity, dependency direction, correctness, or independent use enough to justify its naming, construction, wiring, and navigation cost.

Entity size and caller count are evidence, not rules. A small single-caller entity is justified when it protects a real boundary; a separately named concept is not justified when it only moves a few fields or operations behind forwarding code. Use the smallest set of entities that preserves clear responsibilities and dependencies.

## Requirement Language

Use mandatory language only for settled constraints supported by the request, repo evidence, or an explicit decision. Do not strengthen an inference or illustrative choice merely by writing it as a requirement. For settled requirements, use strong, direct language:

- `must` for required behavior
- `owns` for responsibility
- `receives` for inputs
- `returns` or `emits` for outputs
- `fails with` for failure behavior
- `frozen` for content that remains unchanged during implementation

Use future phase briefs for future requirements. Keep the current phase brief focused on current requirements.

## Right Level of Specificity Gate

Before finalizing requirement text, ask:

- Does it fix observable behavior, public surface, integration point, edit boundary, input guarantee, fixture, verification, and handoff?
- Does it avoid private helper names, helper decomposition, exact control flow, and line-level edits when those do not change required behavior?
- Does it specify repo conventions by reference to observed repo practice instead of copying or guessing them?
- Does it avoid duplicating repo instructions, standard workflows, ordinary conventions, and machine-specific absolute paths?
- Does any algorithm sketch communicate intent without presenting a copyable production structure?
- Does it distinguish settled domain concepts from explanatory design terminology?
- Can production code and public documentation be written in repo-native, caller-facing language without copying the spec's wording?
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
- `Required mechanism`: the smallest named mechanism that satisfies the requirements, such as table lookup, regex match, direct mapper, existing library call, or adapter.
- `Extension trigger`: the concrete future condition that would justify broadening.
- `Boundary note`: the scenario boundary that keeps this phase at the stated depth.

Base these fields on request or repo evidence. Do not invent future scale, callers, concurrency, asynchronous behavior, recovery requirements, compatibility obligations, or extensibility goals. Internal helpers do not acquire compatibility requirements unless they already have independent consumers or the requested design deliberately establishes such a boundary.

Broader mechanisms require an explicit current-phase requirement or an accepted decision that changes the design requirements.

## Minimal-entity Execution

Encode this discipline as brief structure and final review guidance:

- before coding: identify the settled requirements, edit boundary policy, input guarantees, fixtures, and smallest sufficient mechanism
- during coding: add only entities required to satisfy the current requirements
- after coding: verify public surface, abstraction depth, failure behavior, validation path, and phase capability against the brief

Do not repeat this as generic prose in every section. Use it where it changes implementation judgment.

## Optional Component Design Shape

Use this optional shape only when a component has enough independent responsibility to need its own design section. Omit unused fields and repeated sections. Small helpers and local implementation pieces do not need component documents.

```md
# <Component>

## Required Design

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

The first section must be enough for an implementation agent to understand the required design. Later sections add precision within the same scope.

## Internal Invariants and Assertions

Include internal invariants only when they are required to preserve correctness across implementation choices. Keep external behavior defined by the failure requirements:

```md
Internal invariants:
- after <stage>, <condition> holds because <upstream guarantee or local step>
- assert <condition> at <internal boundary> if the repo uses assertions for invariant violations
```

Assertion guidance:

- assertions defend impossible internal states under the stated requirements
- invalid inputs covered by the requirements use the specified failure behavior
- assertions preserve the stated mechanism depth and diagnostic shape

Do not prescribe an assertion merely to make the spec appear complete. Mention an assertion point only when the repo uses assertions for that class of invariant and the location materially affects correctness or diagnostics. Keep this section short.

## Pipeline Position and Input Guarantees

For pipeline stages, state exactly what has already happened upstream:

```md
Input source:
Upstream guarantees:
Local checks:
Out-of-scope input behavior:
```

Use upstream guarantees to prevent defensive implementation inflation. If input is already decoded, normalized, authenticated, parsed, or range-checked, say so.

## Failure Behavior

Default failure behavior:

```md
Detect the invalid condition, report the specified error shape, and stop the current operation.
```

Richer failure handling belongs in a dedicated failure-handling design. If failure behavior is implementation-visible and no repo convention supplies the error shape, the phase has a material spec gap.

## Rule-and-Fixture Acceptance

State the general behavior and its declared input domain before listing cases. Fixtures, examples, and tables are representative lower-bound evidence unless the spec explicitly marks the set as exhaustive. `frozen` means the artifact is unchanged during implementation; it does not mean the listed cases define the entire behavior.

Use concrete cases for behavior that affects implementation:

```md
| Input | Expected |
| --- | --- |
| `{ "status": "paid" }` | `OrderState.Paid` |
| `{ "status": "refunded" }` | `OrderState.Refunded` |
```

Fixtures or tables anchor exact examples, but implementation and verification must also cover relevant normal, boundary, and failure cases implied by the stated rule and repo context. Do not broaden the declared domain or implement only enough behavior to pass the listed cases.

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

The current phase default applies until the decision is made. A missing safe default blocks the phase.

Do not create deferred decisions for minor wording fixes, member/helper naming feedback, local cleanup, or review corrections that do not change behavior, public surface, acceptance, phase order, edit boundaries, input guarantees, failure behavior, or generality boundary.
