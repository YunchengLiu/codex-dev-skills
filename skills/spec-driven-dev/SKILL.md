---
name: spec-driven-dev
description: >
  Discuss, write, refine, review, and implement repo-aware development specs.
  Use after a rough requirement or plan exists to resolve material design
  choices before writing, to produce a minimal rigorous spec, or to implement
  a supplied spec in gated copilot or explicitly authorized autonomous mode.
---

# Spec-Driven Development

## Purpose

Carry development from pre-spec design convergence through a minimal rigorous spec to repo-native implementation and verification.

Enter at the mode supported by the user's current inputs. Do not force every task through every mode.

## Modes

Select one mode from the request and current artifacts:

1. **Pre-Spec Design.** Use when the user has supplied a rough requirement or plan and wants the design resolved before a spec is written. Inspect relevant repo context, reason from established practice, ask only material questions, and finish with a top-down design outline plus the basis for agent-made choices. Wait for user confirmation before authoring the spec unless the user explicitly requested a combined flow.
2. **Spec Authoring.** Use when the design is sufficiently settled and the user asks to write, revise, organize, or review a spec. Produce the smallest rigorous repo-aware spec needed for correct execution.
3. **Implementation.** Use when the user supplies a spec path or an identifiable repo-local spec and asks to implement, start, continue, or complete it. Select gated copilot execution by default; use autonomous iteration only after explicit user authorization.

If `planning-clarification` is available and the request is still too vague to begin spec-focused design, it may be used first. The absence of that skill does not block this workflow: clarify only the minimum missing goal, scope, or deliverable before entering Pre-Spec Design.

## Hard Rules

These rules are mandatory in every applicable mode. Detailed procedures live in the references.

1. **Repository instructions are a hard gate.** Before drafting a non-trivial spec, read the applicable repo instructions and inspect the target modules, adjacent code, tests, public surfaces, fixtures, and conventions. Record only repo constraints that materially affect this work. Implementation agents must repeat this check before editing.
2. **Design questions must be material.** Resolve ordinary engineering choices from repo evidence and established practice. Ask the user only when the answer changes behavior, architecture, data meaning, lifecycle, public compatibility, acceptance, phase boundaries, or product/domain policy.
3. **Agent-made design choices must be disclosed before authoring.** Pre-Spec Design must end with a top-down outline that states the proposed design, material assumptions, important agent-selected defaults, alternatives that required judgment, and the evidence or practice supporting those choices. Do not silently convert an assumption or recommendation into settled design.
4. **Minimum sufficient design.** Apply Occam's razor to architecture and prose. Design for the operating envelope supported by the request and repo evidence. Add scale, concurrency, asynchronous coordination, recovery, compatibility, extensibility, caching, or state machinery only when current behavior, callers, lifecycle, data volume, failure handling, or integration risk requires it.
5. **Responsibility boundaries determine structure.** Keep behavior and state together when they share ownership, lifecycle, invariants, and reasons to change. Introduce a separate production entity only when it establishes a meaningful behavioral, data, ownership, lifecycle, dependency, or integration boundary. Spec concepts and separately described responsibilities do not map one-to-one to types, interfaces, or files; use the smallest set of entities that preserves clear responsibilities and dependencies.
6. **Semantic authority, repo-native implementation.** The spec binds settled architecture, behavior, explicit public requirements, constraints, and acceptance semantics. Production structure, naming, comments, and ordinary implementation choices must be re-derived from those requirements, applicable repo instructions, surrounding code, and caller perspective. Spec wording and explanatory structure are not production-code authority.
7. **Design requirements, not prewritten production code.** Describe responsibilities, flows, state transitions, public requirements, invariants, and algorithm intent at the minimum depth needed for unambiguous implementation. Production-shaped code is permitted only to quote an existing declaration or an explicitly settled exact public requirement, and only in the necessary fragment.
8. **Spec vocabulary must not leak into production.** Explanatory models and authoring terms such as `contract`, `binding`, `spine`, `phase`, and `gate` do not become production types, identifiers, public API concepts, or source comments unless they are established domain concepts. Leaking spec-only terminology, pseudocode, or illustrative structure into production code or comments is prohibited.
9. **Acceptance evidence is representative by default.** State the rule and its input domain. Fixtures, examples, and tables are lower-bound evidence unless explicitly marked exhaustive. Implementation and verification must cover the stated behavior beyond the listed cases without broadening the declared domain.
10. **Do not duplicate repository knowledge.** Repo instructions, standard workflows, ordinary conventions, and machine-specific absolute paths remain in their authoritative source. Include only task-specific deviations, design-relevant constraints, repo-relative landing points when useful, and verification requirements that are not already obvious from the repo.
11. **Phase order follows executable behavior.** Each phase has one review-sized responsibility, acceptance, verification, and handoff. Helper-first phases are valid only when an established caller surface already makes that work independently meaningful.
12. **Execution strategy is explicit.** Gated copilot is the default. Autonomous iteration requires explicit user authorization and one confirmed top-level execution outline before code changes begin.
13. **Review corrections preserve the mainline.** Classify review feedback as a phase-local correction, a durable design change, or temporary inserted work. Apply the correction while preserving the main goal, next planned phase, and mainline return point.
14. **Stable records remain neutral and sparse.** Canonical specs state current requirements directly. `CURRENT.md`, progress, and decisions record only durable handoff state or material design changes; never transcript history, review chatter, private naming, wording polish, rejected minor alternatives, or temporary investigation detail.
15. **File structure follows task scale.** Use one document for a compact spec or a few closely related phases. Add separate briefs, pointers, progress, or decision files only when independent execution or durable handoff requires them.

## Reference Routing

Load only the reference files needed for the current task:

- `references/pre-spec-design.md`: required for Pre-Spec Design; defines evidence gathering, best-practice reasoning, high-value questions, disclosure, and the confirmation outline.
- `references/spec-architecture.md`: use before drafting or reorganizing a spec; frames repo evidence, decomposition, phase order, and spec layout.
- `references/writing-principles.md`: use when writing stable requirements, component designs, acceptance text, failure behavior, generality boundaries, or deferred decisions.
- `references/file-organization.md`: use when deciding whether the task needs one spec, phase briefs, or a durable handoff layout, and when defining mutability.
- `references/implementation.md`: required for Implementation; defines spec discovery, gated copilot execution, autonomous iteration, review correction, commits, and completion.
- `references/execution-briefs.md`: use when authoring an independently executable phase brief.
- `references/progress-and-decisions.md`: use when defining or updating `spec-root/progress/` records.
- `references/self-check.md`: use before finalizing a spec, revising a draft, or performing a self-check review.

## Self-check

For a self-check review request on an existing draft, surface issues that can cause implementation error, scope expansion, fixture drift, or divergent outputs across capable agents. For Chinese self-check-only requests with no requested format, output exactly `未发现实质问题` when the draft has no substantive blocker.
