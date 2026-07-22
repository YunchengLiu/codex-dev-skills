# Pre-Spec Design

## Purpose

Use this mode after the user has supplied a rough requirement, direction, or plan and before a development spec is written. Resolve the design choices that materially affect implementation, then present a top-down design outline for user confirmation.

This is not general ideation and not a questionnaire. The agent owns repo inspection, technical analysis, and ordinary engineering judgment.

## Hard Rules

1. **Inspect before asking.** Read applicable repo instructions and the relevant code, tests, public surfaces, existing specs, and conventions before asking questions that repo evidence may answer.
2. **Own ordinary engineering choices.** Apply established practice when it fits the repo and evidenced operating envelope. Do not ask the user to decide private structure, local naming, helper decomposition, routine library use, or ordinary error-handling mechanics.
3. **Ask only material questions.** A question must change behavior, architecture, data meaning, lifecycle, public compatibility, acceptance, phase boundaries, operating constraints, or product/domain policy.
4. **Recommend before requesting a choice.** When multiple reasonable designs remain, state the recommended option first, explain the practical basis and tradeoff, and ask the user to choose only when the distinction is material.
5. **Do not invent requirements.** Do not introduce hypothetical scale, concurrency, asynchronous behavior, recovery, compatibility, extensibility, security posture, or operational machinery without request or repo evidence.
6. **Disclose agent-made decisions.** The final outline must identify material defaults and design choices selected by the agent and state their basis. A reasonable choice must not become settled design silently.
7. **Require design confirmation.** Present the final design outline and wait for user confirmation before authoring the spec unless the user explicitly authorized a combined design-and-authoring flow.

## Design Convergence Loop

### 1. Establish the design context

Determine only the applicable items:

- target behavior and user-visible outcome
- current callers or users
- owning execution path and integration boundary
- existing public surfaces and compatibility obligations
- data meaning, state, ownership, and lifecycle
- actual execution model and operating envelope
- failure behavior that callers can observe
- acceptance signal and representative cases
- likely review-sized phase boundaries

Separate user-confirmed facts, repo evidence, agent inferences, and unresolved decisions.

### 2. Resolve each design point through the proper source

Use this order:

1. **Repo evidence settles it:** follow the repo and report the material constraint in the final outline when it affects design.
2. **Established practice clearly fits:** select or recommend the smallest fitting approach and record the basis for confirmation.
3. **Several reasonable options materially differ:** present two or three concise options, recommend one, and explain the behavior, cost, or boundary affected by the choice.
4. **Product, domain, or personal policy is required:** ask the user for the intended rule or preference without substituting a generic technical default.
5. **The choice is private and repo-governed:** leave it to implementation and keep it out of the spec discussion.

Use authoritative technical sources when a recommendation depends on current standards, version-sensitive APIs, or externally defined behavior. Do not invoke generic "best practice" without relating it to the repo and operating envelope.

### 3. Ask high-value questions

Ask one to three related questions at a time. Questions must be short, answerable, and accompanied by enough context for the user to understand the consequence.

Good question targets include:

- competing interpretations of observable behavior
- ownership or lifecycle choices that change API use
- real concurrency or execution-model choices
- failure semantics visible to callers
- compatibility or migration policy
- domain-specific data meaning
- acceptance distinctions that determine correctness
- scope boundaries that materially change the design

Do not ask about information available in the repo, speculative future use, ordinary implementation detail, or distinctions that do not change design or validation.

### 4. Stop at sufficient certainty

Stop asking when the target behavior, main execution path, responsibilities, operating envelope, material state or lifecycle, failure semantics, acceptance, and phase shape are clear enough to write a rigorous spec. Remaining repo-native implementation choices do not justify further discussion.

## Required Confirmation Outline

End Pre-Spec Design with a concise top-down outline using only applicable sections:

```md
## Proposed Design

### Goal and Non-Goals

### Main Behavior and Execution Path

### Responsibilities and Boundaries

### Data, State, and Lifecycle

### Failure and Compatibility Behavior

### Operating Envelope

### Acceptance Approach

### Phase Outline

### Agent-Selected Decisions and Basis

### Remaining Material Questions
```

For every material agent-selected decision, state:

- the selected approach
- the request, repo evidence, or established practice supporting it
- the meaningful alternative when one existed
- why the selected approach is the smallest sufficient fit

Keep the outline independent of the discussion transcript. Report settled design and the basis for judgment, not the sequence of questions that produced it.

Derive the phase outline from the whole design in dependency order. Establish a functionally correct path before optional optimization, and do not make one phase depend on later work for its own acceptance.

## Transition

After confirmation:

- enter Spec Authoring when the user asked for a spec;
- enter Implementation only when an existing confirmed spec is available and the user authorized implementation;
- remain in Pre-Spec Design when the user materially changes the proposed design.

## Self-Check

Before requesting confirmation, verify:

- repo-answerable questions were resolved through inspection rather than delegated to the user;
- every question asked changed a material design or acceptance decision;
- recommendations are tied to the actual repo, operating envelope, and relevant established practice;
- no hypothetical scale, concurrency, recovery, compatibility, or extensibility requirement entered the design;
- every material agent-selected default is visible in the outline with its basis;
- the outline is top-down, concise, and independent of the discussion transcript;
- remaining implementation freedom can safely be resolved from repo conventions after confirmation.
