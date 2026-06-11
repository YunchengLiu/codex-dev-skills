---
name: spec-writer
description: >
  Write and refine repo-aware implementation specs as sliceable, strongly
  structured document sets: stable canonical contracts, phase execution briefs,
  fixture-driven acceptance, and progress/decision records for implementation
  agents.
---

# Spec Writer

## Purpose

Turn settled design goals into a repo-aware spec document set that implementation agents can execute with low ambiguity, low scope expansion, and consistent judgment.

Write specs as structured thinking artifacts. The reading path should teach the next agent how to think: start from repo evidence, derive behavior and the implementation spine, pass the gates, then write only the current executable contract.

## Core Invariants

Treat these as the non-negotiable reasoning layer. Detailed templates and examples live in the references.

1. **Repo evidence first.** Start non-trivial specs from modules, tests, public surfaces, fixtures, repo instructions, conventions, and pipeline or lifecycle boundaries.
2. **Fresh-agent entry first-class.** A new agent must find the current phase, current brief, blocker state, next action, and review path from repo-local docs.
3. **Top-down decomposition.** Move from observable behavior and acceptance to the task-shaped implementation spine before specifying components, internals, or helpers.
4. **Design simplification before phase planning.** Use ownership, boundaries, phase order, and contract shape to remove unnecessary complexity before creating local tasks.
5. **Design contracts, not private implementation.** Specify public surfaces, behavior, data formats, invariants, acceptance, edit boundaries, and algorithm intent when needed. Leave private class names, helper decomposition, line-level edits, and repo-style choices to implementation context.
6. **Evidence-bounded complexity.** Abstraction depth, defensive behavior, performance work, and extensibility must be justified by current requirements, repo contracts, fixtures, observed failures, acceptance, or integration risk.
7. **Spine-ordered phases.** Each phase has one review-sized responsibility, acceptance, verification, and handoff. Helper-first phases are invalid unless the caller contract already exists and is stable.
8. **Edit boundary as policy.** State primary anchors, relevant tests and fixtures, repo-required collateral principles from observed conventions, frozen scope, and escalation rules.
9. **Bounded facades only for executability.** Use stubs or facades only to keep the current spine executable; state present behavior, absent behavior, and the later fill-in phase.
10. **Correct canonical specs directly.** When spec revision is in scope, fix wrong or unclear canonical text. Record decisions only for material durable choices not already captured by the corrected spec.
11. **Sparse handoff records.** Progress and decisions serve future execution judgment, not transcript history.

## Structured Thinking Loop

Use this loop for non-trivial specs. The written spec should expose the same sequence so another agent can follow the reasoning without chat history.

1. **Orient in the repo.** Classify the task and locate concrete landing points: code, tests, fixtures, public surfaces, existing specs, and repo conventions.
2. **Define the collaboration surface.** State fresh-agent entry, pre-coding summary, approval expectations, current-phase-only execution, verification, and review handoff.
3. **Name the behavior target.** Define the observable behavior, output, state transition, or acceptance signal before naming components.
4. **Choose the implementation spine.** Identify the user flow, API call chain, pipeline path, lifecycle transition, CLI command flow, compiler pass, migration route, or repo-local equivalent that owns the behavior.
5. **Run the gates.** Check design simplification, evidence-bounded complexity, spine order, review-sized phase scope, edit boundary policy, mutability, and material decision handling before writing tasks.
6. **Write design contracts.** Define responsibilities, public surfaces, input guarantees, outputs, invariants, failure behavior, fixtures, verification, and implementation latitude.
7. **Plan phases in spine order.** Slice around executable behavior or integration responsibility. Each phase gets its own acceptance, verification, and handoff.
8. **Write only the current brief at implementation depth.** Localize it to the current goal, spine position, primary anchors, collateral policy, acceptance, verification, and handoff.
9. **Set the pointer and records.** Expose `CURRENT.md` or the repo equivalent. Use progress for handoff state and decisions for material durable choices.
10. **Self-check through the same gates.** Reject specs that are helper-first, over-specific about private code, vague about acceptance, noisy in records, dependent on low-value history, or driven by abstraction, defensive behavior, performance work, or extensibility that lacks current evidence.

## Reference Routing

Load only the reference files needed for the current task:

- `references/spec-architecture.md`: use before drafting or reorganizing a spec; frames repo evidence, decomposition, gates, phase order, and spec layout.
- `references/writing-principles.md`: use when writing stable contracts, component contracts, acceptance text, failure behavior, generality boundaries, or deferred decisions.
- `references/file-organization.md`: use when creating or revising the `spec-root/` layout, stable/dynamic split, current pointer, and mutability model.
- `references/execution-briefs.md`: use when writing the current phase brief for implementation agents.
- `references/progress-and-decisions.md`: use when defining or updating `spec-root/progress/` records.
- `references/self-check.md`: use before finalizing a spec, revising a draft, or performing a self-check review.

## Self-check

For a self-check review request on an existing draft, surface issues that can cause implementation error, scope expansion, fixture drift, or divergent outputs across capable agents. For Chinese self-check-only requests with no requested format, output exactly `未发现实质问题` when the draft has no substantive blocker.
