# Self-check

## Purpose

Use this reference before finalizing a spec, revising a draft, or performing a self-check review. Review the settled design and execution risks rather than template completeness.

Report issues that can cause implementation error, scope expansion, fixture drift, noisy handoff, or divergent outputs across capable agents. Do not report cosmetic preferences as blockers. Public documentation that obscures intended use, depends on undisclosed spec context, or addresses the wrong audience is a substantive API-quality issue rather than a cosmetic preference.

## Self-check Thinking Frame

Review in this order:

1. **Entry.** Can a fresh agent find the current phase, current brief, blocker state, next action, and review path from repo-local docs when the task requires phased handoff?
2. **Repo evidence.** Were applicable repo instructions read, and does the spec derive from observed modules, tests, public surfaces, fixtures, and conventions?
3. **Behavior target.** Is the observable behavior or acceptance signal named before components and helpers?
4. **Implementation spine.** Does the phase plan follow the task-shaped spine before private internals?
5. **Gates.** Did the design pass simplification, spine order, review-sized phase scope, edit boundary policy, mutability, and material decision handling?
6. **Design requirements.** Are public surfaces, responsibilities, input guarantees, outputs, invariants, failure behavior, acceptance, and implementation latitude clear?
7. **Briefs.** Can the current brief be executed as one local, review-sized slice?
8. **Records.** Are progress and decisions sparse handoff records rather than history dumps?
9. **Production translation.** Can implementation be re-derived in repo-native code and caller-facing documentation without copying spec terminology or illustrative structure?
10. **Acceptance.** Does the spec state a rule and input domain for which fixtures are representative evidence rather than the implementation boundary?
11. **Output.** Are findings concrete, risk-based, and tied to the file or section that should change?

## Entry Check

- When durable handoff requires a current pointer, does it name current phase, current brief, progress file, decision file, blocker state, next action, and mainline return?
- When interactive phased development needs a collaboration model, does the top-level entry state fresh-agent entry, pre-coding summary, approval expectations, current-phase-only execution, verification, and review handoff?
- Can a short prompt such as "read the spec and plan the next step" route an implementation agent to the right files?

## Repo Evidence Check

- Were all applicable repo instructions read before drafting or review?
- Does the spec start from repo evidence: modules, tests, public APIs, fixtures, existing specs, and repo instructions?
- Does it avoid inventing repo conventions for build, exports, tests, formatting, naming, or directory layout?
- Does it avoid copying repo instructions, standard workflows, ordinary conventions, and machine-specific absolute paths into the spec?
- Are repo-required collateral edits described as principles from observed conventions rather than guessed manifests?
- If repo evidence conflicts with the requested shape, does the spec state the conflict and choose the smallest compatible path?

## Behavior and Spine Check

- Is the behavior target or acceptance signal stated before component names?
- Is the task-shaped implementation spine named, such as user flow, API call chain, pipeline/data path, migration path, lifecycle transition, CLI command flow, or compiler pass?
- Does the phase plan derive from the observable behavior and spine?
- Does the first usable phase establish the owning public entry point, consumer, assembler, coordinator, lifecycle root, or minimal executable spine before private helper work?
- Are helper-first phases treated as blockers unless the caller surface already exists and is stable, or the task is an isolated repair under a frozen public surface?
- Are bounded facades or stubs used only to keep the current spine executable, with present behavior, absent behavior, verification, and fill-in phase stated?
- Can review-time correction tasks be inserted without renumbering or losing the mainline return point?

## Gate Check

### Design Simplification

- Did the spec simplify ownership, boundaries, phase order, and requirement shape before creating local tasks?
- Does every component, facade, phase, or helper have a behavior or acceptance signal that justifies it?
- Are abstractions avoided when they exist only to make a local micro-task convenient?
- Are behavior and state that share ownership, lifecycle, invariants, and reasons to change kept together without mixing responsibilities that require materially different boundaries?
- Does every separate production entity establish a meaningful behavioral, data, ownership, lifecycle, dependency, or integration boundary rather than merely mirroring a spec concept or moving a few fields or operations behind forwarding code?
- Does the design avoid unusual glue, broad fallback behavior, or adapters that indicate a misplaced boundary?
- Are abstraction depth, defensive behavior, performance work, and
  extensibility justified by current requirements, repo constraints, fixtures,
  observed failures, acceptance, or integration risk?
- Are data scale, caller count, concurrency, asynchronous behavior, recovery, compatibility, and lifecycle assumptions supported by the request or repo evidence?
- Does the design avoid synchronization, recovery paths, generalized state machines, caching, or large-scale optimization when the evidenced operating envelope does not require them?
- Are internal helpers kept as ordinary implementation details unless they have an established or deliberately required compatibility boundary?

### Review-sized Phase

- Does each phase have one focused review responsibility?
- Can the phase reasonably land as one coherent commit unless repo practice requires otherwise?
- Does each phase have its own acceptance, verification, and handoff condition?
- Is the phase free of unrelated helper extraction, cleanup, or future-phase work?

### Edit Boundary Policy

- Does the spec state primary targets, tests/fixtures, repo-required collateral policy, frozen scope, escalation rule, and reporting rule?
- Does the edit boundary focus implementation without becoming a brittle exhaustive behavior list?
- Does it escalate scope-broadening, requirement-changing, ownership-moving, or repo-convention-unclear work?

### Mutability

- Are stable docs, phase briefs, and frozen fixtures treated as read-only unless spec revision is in scope?
- When spec correction is in scope, does the corrected canonical text stand on its own?
- Are dynamic records append-oriented and preserved outside the current responsibility?

### Material Decision

- Are decisions written only for material choices that affect future implementation judgment?
- Are wrong or unclear canonical specs corrected directly when revision is in scope?
- Are minor wording, naming, local cleanup, and transient discussion omitted from decisions and progress?
- Are review sequences, rejected minor alternatives, and temporary investigations absent from canonical specs and durable records?

## Design Requirement Check

- Does each independently specified component state its role, spine or pipeline position, input source, upstream guarantees, local checks, output, and failure behavior?
- Are important internal invariants stated positively and guarded with repo-standard assertions where appropriate?
- Does the design state its generality boundary and implementation depth when those affect implementation judgment?
- Does failure behavior default to detect, report, and stop unless richer failure handling is required?
- If failure behavior is implementation-visible, is the error shape explicitly specified or inherited from repo convention?
- Are public capabilities concrete enough to implement and test?
- Does the spec preserve private helper names, helper decomposition, exact control flow, and line-level edits as implementation latitude when they do not change required behavior?
- Does the spec avoid implying a one-to-one mapping from logical responsibilities to production types, interfaces, or files?
- Does any production-shaped code quote an existing declaration or an explicitly settled exact public requirement, with only the necessary fragment?
- Does any algorithm sketch communicate intent without supplying complete classes, private members, helper layouts, or implementation bodies?
- Are explanatory design concepts clearly distinguished from established domain concepts?
- Can implementation names, structure, and source comments be re-derived from repo conventions without copying spec wording?
- If public API documentation is in scope, will it be understandable to callers who have not read the spec and use caller-facing rather than architecture-classification language?
- Are rationale and alternatives kept out of execution-facing requirements unless needed to prevent ambiguity?
- Does each paragraph or section change implementation, verification, review, or handoff judgment? If not, should it be removed?
- Does the spec avoid labels, categories, and semantic distinctions that do not affect behavior, design choice, or validation?
- Does the spec use direct domain language instead of propagating authoring terms such as contract, binding, spine, phase, or gate into proposed production vocabulary?

## Brief Check

- Can the current phase brief be read with finite attention and executed as a self-contained slice?
- Does it state current phase goal, review responsibility, spine/mainline position, primary targets, frozen scope, acceptance, verification, and handoff?
- Does it tell the agent what to summarize before coding and whether approval is required?
- Does the first implementation action start from the stated owner, consumer, assembler, coordinator, lifecycle root, or minimal executable spine?
- If it starts with a helper, does it name the stable caller surface or isolated repair surface that makes this valid?
- Does it include only current-phase component details and local rationale?
- Does it preserve implementation latitude for private mechanics that do not change required behavior?
- Does it require the implementation agent to re-read repo instructions and surrounding code before editing?
- Does it require repo-native production code and comments rather than transcription of spec-only terminology, models, pseudocode, or phase language?
- Does it require the simplest repo-consistent implementation for the evidenced operating envelope?
- Does it include a final minimal-entity check?
- Does it use boundary reporting for defined boundary conditions?

## Acceptance Check

- Is the general behavior and declared input domain stated before fixture references or `input -> expected` tables?
- Are fixtures and examples treated as representative lower-bound evidence unless explicitly marked exhaustive?
- Would an implementation that special-cases only the listed fixtures still fail the stated requirements?
- Does verification include relevant normal, boundary, and failure cases implied by the rule and repo context without broadening the declared domain?
- Are fixture files marked frozen?
- Is there a fixture errata path through `progress/decisions.md`?
- Does the fixture errata rule distinguish partial contradictions from sole or canonical acceptance contradictions?
- Would two capable agents infer the same expected behavior from the acceptance section?

## Production Translation Check

- Does the spec bind semantics rather than its wording or illustrative structure?
- Are spec-only models and terms prevented from automatically becoming production types, identifiers, public API concepts, or source comments?
- Does the execution brief direct the agent to design public surfaces and documentation from the perspective of repo users who do not know the spec internals?
- Are copy semantics, ownership, lifetime, concurrency, and failure details documented only when their caller-visible meaning needs explanation?
- Would two capable agents be able to produce the same behavior through different reasonable private implementations that both fit the repo?
- Are proposed identifiers and public comments free of spec-authoring vocabulary unless that vocabulary is an established domain concept?

## Dynamic Record Check

- When durable handoff uses `progress/`, does it preserve current phase, blocker state, current brief, and next action?
- Are progress entries limited to handoff-relevant state points?
- Are decisions written before implementation choices that fill material spec gaps?
- Do decisions include phase, source, question, decision, reason, and canonical update flag?
- Are canonical updates promoted explicitly through stable docs when required?
- Can future execution proceed without reconstructing chat history?

## Output Standard

If any check fails, state the concrete risk and the file or section that should change.

For Chinese self-check-only requests with no requested format, output exactly this when the draft has no substantive blocker:

```text
未发现实质问题
```
