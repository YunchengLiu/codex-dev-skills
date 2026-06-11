# Self-check

## Purpose

Use this reference before finalizing a spec, revising a draft, or performing a self-check review. The self-check should follow the same structured thinking path the spec is supposed to teach.

Report issues that can cause implementation error, scope expansion, fixture drift, noisy handoff, or divergent outputs across capable agents. Do not report cosmetic preferences as blockers.

## Self-check Thinking Frame

Review in this order:

1. **Entry.** Can a fresh agent find the current phase, current brief, blocker state, next action, and review path from repo-local docs?
2. **Repo evidence.** Does the spec derive from observed modules, tests, public surfaces, fixtures, repo instructions, and conventions?
3. **Behavior target.** Is the observable behavior or acceptance signal named before components and helpers?
4. **Implementation spine.** Does the phase plan follow the task-shaped spine before private internals?
5. **Gates.** Did the design pass simplification, spine order, review-sized phase scope, edit boundary policy, mutability, and material decision handling?
6. **Contracts.** Are public surfaces, responsibilities, input guarantees, outputs, invariants, failure behavior, acceptance, and implementation latitude clear?
7. **Briefs.** Can the current brief be executed as one local, review-sized slice?
8. **Records.** Are progress and decisions sparse handoff records rather than history dumps?
9. **Acceptance.** Would two capable agents infer the same expected behavior from fixtures or tables?
10. **Output.** Are findings concrete, risk-based, and tied to the file or section that should change?

## Entry Check

- Is there a current pointer naming current phase, current brief, progress file, decision file, blocker state, next action, and mainline return?
- Does the top-level stable entry include a collaboration model for interactive spec-driven development?
- Does the collaboration model state fresh-agent entry, pre-coding summary, approval expectations, current-phase-only execution, verification, and review handoff?
- Can a short prompt such as "read the spec and plan the next step" route an implementation agent to the right files?

## Repo Evidence Check

- Does the spec start from repo evidence: modules, tests, public APIs, fixtures, existing specs, and repo instructions?
- Does it avoid inventing repo conventions for build, exports, tests, formatting, naming, or directory layout?
- Are repo-required collateral edits described as principles from observed conventions rather than guessed manifests?
- If repo evidence conflicts with the requested shape, does the spec state the conflict and choose the smallest compatible path?

## Behavior and Spine Check

- Is the behavior target or acceptance signal stated before component names?
- Is the task-shaped implementation spine named, such as user flow, API call chain, pipeline/data path, migration path, lifecycle transition, CLI command flow, or compiler pass?
- Does the phase plan derive from the observable behavior and spine?
- Does the first usable phase establish the owning public entry point, consumer, assembler, coordinator, lifecycle root, or minimal executable spine before private helper work?
- Are helper-first phases treated as blockers unless the caller contract already exists and is stable, or the task is an isolated repair under a frozen public surface?
- Are bounded facades or stubs used only to keep the current spine executable, with present behavior, absent behavior, verification, and fill-in phase stated?
- Can review-time correction tasks be inserted without renumbering or losing the mainline return point?

## Gate Check

### Design Simplification

- Did the spec simplify ownership, boundaries, phase order, and contract shape before creating local tasks?
- Does every component, facade, phase, or helper have a behavior or acceptance signal that justifies it?
- Are abstractions avoided when they exist only to make a local micro-task convenient?
- Does the design avoid unusual glue, broad fallback behavior, or adapters that indicate a misplaced boundary?

### Review-sized Phase

- Does each phase have one focused review responsibility?
- Can the phase reasonably land as one coherent commit unless repo practice requires otherwise?
- Does each phase have its own acceptance, verification, and handoff condition?
- Is the phase free of unrelated helper extraction, cleanup, or future-phase work?

### Edit Boundary Policy

- Does the spec state primary targets, tests/fixtures, repo-required collateral policy, frozen scope, escalation rule, and reporting rule?
- Does the edit boundary focus implementation without becoming a brittle exhaustive behavior list?
- Does it escalate scope-broadening, contract-changing, ownership-moving, or repo-convention-unclear work?

### Mutability

- Are stable docs, phase briefs, and frozen fixtures treated as read-only unless spec revision is in scope?
- When spec correction is in scope, does the corrected canonical text stand on its own?
- Are dynamic records append-oriented and preserved outside the current responsibility?

### Material Decision

- Are decisions written only for material choices that affect future implementation judgment?
- Are wrong or unclear canonical specs corrected directly when revision is in scope?
- Are minor wording, naming, local cleanup, and transient discussion omitted from decisions and progress?

## Contract Check

- Does each component contract state role, spine or pipeline position, input source, upstream guarantees, local checks, output, and failure behavior?
- Are important internal invariants stated positively and guarded with repo-standard assertions where appropriate?
- Does the contract state generality boundary and implementation depth?
- Does failure behavior default to detect, report, and stop unless a richer failure-handling contract exists?
- If failure behavior is implementation-visible, is the error shape specified by contract or inherited from repo convention?
- Are public capabilities concrete enough to implement and test?
- Does the spec preserve private helper names, helper decomposition, exact control flow, and line-level edits as implementation latitude when contract-neutral?
- When pseudocode appears, does it communicate algorithm intent rather than concrete code structure?
- Are rationale and alternatives kept out of execution-facing contracts unless needed to prevent ambiguity?

## Brief Check

- Can the current phase brief be read with finite attention and executed as a self-contained slice?
- Does it state current phase goal, review responsibility, spine/mainline position, primary targets, frozen scope, acceptance, verification, and handoff?
- Does it tell the agent what to summarize before coding and whether approval is required?
- Does the first implementation action start from the stated owner, consumer, assembler, coordinator, lifecycle root, or minimal executable spine?
- If it starts with a helper, does it name the stable caller contract or isolated repair surface that makes this valid?
- Does it include only current-phase component details and local rationale?
- Does it preserve implementation latitude for contract-neutral private mechanics?
- Does it include a final minimal-entity check?
- Does it use boundary reporting for defined boundary conditions?

## Acceptance Check

- Are natural-language rules backed by fixture references or `input -> expected` tables when interpretation matters?
- Are fixture files marked frozen?
- Is there a fixture errata path through `progress/decisions.md`?
- Does the fixture errata rule distinguish partial contradictions from sole or canonical acceptance contradictions?
- Would two capable agents infer the same expected behavior from the acceptance section?

## Dynamic Record Check

- Does `progress/` preserve current phase, blocker state, current brief, and next action?
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
