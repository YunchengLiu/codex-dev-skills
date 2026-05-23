---
name: spec-writer
description: Write and refine repo-aware implementation specs as sliceable, strongly structured document sets: stable canonical contracts, phase execution briefs, fixture-driven acceptance, and progress/decision records for implementation agents.
---

# Spec Writer

## Purpose

Turn settled design goals into a repo-aware spec document set that implementation agents can execute with low ambiguity and low scope expansion.

The skill must first decide how the spec should be organized, then write execution-facing documents as contracts. A good output should let capable implementation agents with finite attention produce materially similar implementations from the same phase brief during routine execution.

## Hard Rules

- For non-trivial specs, start with repo-aware spec architecture analysis and locate the repo landing points before drafting.
- Treat a spec as non-trivial when it changes public behavior, crosses more than one file, adds or changes fixtures, changes pipeline boundaries, affects failure/state/lifecycle behavior, needs phase handoff, or will be implemented by a fresh agent.
- Execution-facing specs are binding contracts with chosen behavior stated directly.
- Each document uses a top-down structure: first list the binding requirements, then explain details in scoped sections.
- Use contract-level specificity: fix behavior, boundaries, fixtures, and verification while preserving private implementation latitude for contract-neutral mechanics.
- Prefer positive structural constraints over negative warnings. Use allowed paths, frozen paths, input guarantees, fixtures, and explicit public surfaces.
- Phase briefs are sliceable current-phase contracts with local rationale and directly relevant component details.
- Stable spec documents, phase briefs, and frozen fixtures are read-only during implementation unless the current phase explicitly authorizes a spec revision. Dynamic records are append-oriented and preserve entries outside the current responsibility.
- Specs must expose a current-phase pointer. A fresh agent should be able to identify the current phase, current brief, blocker state, and next action from repo-local docs.
- Specs must define the intended generality boundary. A repo-local, limited-input feature should be specified as such, so implementation agents keep the mechanism at the required depth.
- Target capability-level execution with agent-runtime-neutral guidance.
- Specs must support fresh-agent entry. A short prompt should be enough for a new implementation agent to find the current phase, read the right brief, form the next execution plan, and start from repo-local docs.
- Specs should encode minimal-entity execution: identify the required contract and smallest sufficient mechanism before coding, then verify no extra capability, abstraction, or failure behavior was added.
- Every component contract must state pipeline position, input source, upstream guarantees, local responsibilities, output shape, and failure behavior when they affect implementation.
- Important internal invariants should be stated positively. When repo conventions support assertions, use assertions for invariant violations rather than widening external validation or failure handling.
- Default failure behavior is minimal: detect, report, stop. A dedicated failure-handling contract defines any behavior beyond the specified error shape and stopping point.
- Acceptance should be fixture-first. Use concrete `input -> expected` cases or tables for behavior that affects implementation.
- Frozen fixtures remain unchanged during implementation. Partial fixture contradictions are recorded under `spec-root/progress/decisions.md` and skipped only when remaining acceptance coverage is valid; a contradiction in the sole or canonical acceptance signal blocks the phase.
- Use lightweight, grep-able boundary reports for defined boundary conditions.

## Workflow

1. Inspect the repo before writing non-trivial specs. Locate existing modules, tests, public surfaces, naming patterns, spec conventions, and pipeline boundaries.
2. Plan the spec shape. Decide the `spec-root/`, stable files, phase briefs, fixture files, and `spec-root/progress/` records before drafting content.
3. Write stable canonical docs under `spec-root/` for goals, component contracts, public interfaces, pipeline guarantees, phase plan, and fixture semantics.
4. Write phase execution briefs as current-phase action references. Each brief carries the local facts needed for that phase.
5. Put dynamic execution records under `spec-root/progress/`. Decisions capture spec gaps before code changes; progress captures status points and milestone effects.
6. Run the self-check before finishing. Reject wording that leaves broad interpretation space or invites implementation beyond the current phase.

## Reference Routing

Load the reference files needed for the task:

- `references/spec-architecture.md`: use before drafting or reorganizing a spec; covers repo-aware spec shape analysis.
- `references/writing-principles.md`: use when writing component contracts, behavior contracts, acceptance text, or deferred decisions.
- `references/file-organization.md`: use when creating or revising the `spec-root/` layout and stable/dynamic split.
- `references/execution-briefs.md`: use when writing phase briefs for implementation agents.
- `references/progress-and-decisions.md`: use when defining or updating `spec-root/progress/`.
- `references/self-check.md`: use before finalizing a spec, revising a draft, or performing a self-check review.

## Self-check

For a self-check review request on an existing draft, surface issues that can cause implementation error, scope expansion, fixture drift, or divergent outputs across capable agents. When the draft has no substantive blocker, output exactly `未发现实质问题`.
