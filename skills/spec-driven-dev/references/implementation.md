# Spec Implementation

## Purpose

Use this mode when the user supplies a spec path or an identifiable repo-local spec and asks to implement, start, continue, or complete it. Implement the current actionable scope in the repo; do not respond with another plan unless the user requested planning only.

## Hard Rules

1. **Read the authoritative inputs before editing.** Read applicable repo instructions, the supplied spec, directly referenced current briefs or records, and the relevant code and tests.
2. **Implement semantics in repo-native form.** Preserve settled behavior, public requirements, constraints, and acceptance. Re-derive production structure, naming, comments, and ordinary mechanics from repo conventions and caller needs.
3. **Re-derive production entity boundaries.** Keep behavior and state together when they share ownership, lifecycle, invariants, and reasons to change. Split them only for a meaningful behavioral, data, ownership, lifecycle, dependency, or integration boundary. Do not translate each spec concept or responsibility into a type, interface, helper, or file; use the smallest repo-consistent structure that keeps responsibilities and dependencies clear.
4. **Use the evidenced operating envelope.** Do not add hypothetical scale, concurrency, asynchronous coordination, recovery, compatibility, extensibility, caching, or generalized state machinery.
5. **Fixtures are not the implementation boundary.** Implement the stated rule over its declared domain and verify relevant normal, boundary, and failure cases.
6. **Gated copilot is the default.** Do not begin phase edits until the user approves the phase summary. Do not commit, update durable progress, or advance to the next phase until the user accepts the reviewed phase. After acceptance, create one focused local commit unless the user or repo explicitly excludes commits.
7. **Autonomous iteration requires explicit authorization.** Before editing, present one top-level execution outline and obtain confirmation. After confirmation, execute, verify, self-check, create one local commit for each verified phase result, update necessary progress, and advance without routine approval stops. Use a different commit policy only when the user or repo explicitly requires it.
8. **Material conflicts stop execution.** Stop when safe progress requires changing settled behavior, public compatibility, acceptance, scope, or an unresolved product/domain rule. Resolve explanatory wording or illustrative differences through repo-native implementation without escalation.
9. **Review corrections preserve the mainline.** Apply corrections without losing the main goal, next planned phase, or return point after inserted work.
10. **Stable records remain neutral.** Update canonical specs only when spec revision is in scope or an accepted durable design change requires promotion. Record final state and durable choices, never review dialogue or transient implementation history.

## Locate the Actionable Scope

Use this order:

1. Follow an explicit current phase or current brief.
2. For a compact one-slice spec, execute the whole stated slice.
3. For a phased spec without a pointer, inspect the repo and verification state to identify the first unfinished executable phase.
4. If several materially different scopes remain plausible, ask one focused question before editing.

Do not infer authorization for future phases in gated copilot mode. In autonomous mode, the confirmed top-level outline authorizes the planned phases within the stated boundaries.

## Reconcile Spec and Repo

Before editing, distinguish:

- **Settled requirements:** behavior, public APIs or formats, constraints, input guarantees, failure semantics, compatibility, and acceptance.
- **Repo-governed implementation:** private types, helpers, file-local structure, ordinary control flow, naming, comments, and routine tests.
- **Explanatory material:** rationale, models, pseudocode, examples, phase vocabulary, and suggested private shapes.

Implement settled requirements. Use repo evidence for repo-governed implementation. Use explanatory material to understand intent, never as production text or a code skeleton.

Re-evaluate the production entity boundaries against the surrounding code. A spec may separate responsibilities to explain the design without requiring separate types or files. Conversely, do not combine responsibilities whose ownership, lifecycle, invariants, or dependency direction require a real boundary merely to minimize the entity count.

Repo instructions and standard workflows remain authoritative at their original location. Do not copy them into the spec or progress records. Do not persist machine-specific absolute paths unless they are an actual external requirement.

## Gated Copilot Execution

Use this strategy unless the user explicitly authorizes autonomous iteration.

### Before each phase

Report concisely:

- phase goal and mainline position
- design and repo evidence supporting the approach
- expected edit surface and frozen boundaries
- acceptance and verification
- first implementation action
- material risks or conflicts, if any

Wait for user approval before modifying code.

### Implement and review

1. Implement only the approved phase.
2. Run focused verification.
3. Perform a self-check against the spec, repo rules, operating envelope, and production-language boundaries.
4. Report changes, verification, boundary conditions, and remaining risks.
5. Wait for user review.
6. Apply review corrections and repeat verification as needed.

After the user accepts the phase:

1. update canonical spec text only for an accepted durable design change;
2. update progress or decisions only when the spec uses durable handoff records and state materially changed;
3. create one focused local commit for the accepted phase without staging unrelated user changes, unless the user or repo explicitly excludes commits;
4. identify the next phase and wait before beginning it.

## Autonomous Iteration

Use only after explicit user authorization.

### Confirmation before execution

Present one top-level outline containing:

- overall goal and current repo state
- ordered phases and mainline
- operating envelope and key settled assumptions
- acceptance and verification for each phase
- commit and progress-update behavior
- conditions that will stop autonomous execution

Wait for user confirmation. This is the single routine approval gate for the confirmed scope.

### Phase loop

For each phase:

1. re-read the current brief and relevant repo context;
2. implement the review-sized responsibility;
3. run focused verification;
4. self-check behavior, scope, repo fit, and unnecessary complexity;
5. correct discovered issues;
6. update only necessary durable records;
7. create one focused local commit for the completed phase without staging unrelated user changes;
8. advance to the next phase while preserving the mainline.

Stop and ask the user when:

- settled behavior, public compatibility, or acceptance must change;
- required work materially exceeds the confirmed scope;
- a product or specialized domain choice lacks a safe answer;
- repo evidence invalidates a central design assumption;
- user changes cannot be safely coordinated;
- verification demonstrates that the confirmed design is not viable.

Do not stop for ordinary private implementation choices, repo-consistent naming, local test additions, or corrections that preserve settled behavior.

Autonomous authorization does not authorize push, pull request creation, release, deployment, publication, or other external effects unless the user separately authorizes them.

## Review Correction and Mainline Return

Classify review feedback:

1. **Phase-local correction:** implementation, naming, comments, tests, or local complexity changes that preserve the design. Correct locally; do not create a decision record.
2. **Durable design change:** behavior, public surface, data meaning, input guarantee, failure semantics, acceptance, phase order, or operating envelope changes. Confirm the change, update canonical text, and revise affected future briefs.
3. **Inserted work:** a bounded correction outside the current phase that leaves the mainline intact. Record only the current inserted task and the mainline return point when durable handoff requires it.

After any correction, restate internally:

- overall goal
- current phase or inserted task
- next mainline phase
- remaining acceptance

Do not transform individual review comments into permanent decisions or extra phases unless they change future execution judgment.

## Completion

Completion requires:

- the selected scope is implemented;
- focused verification passes or remaining verification is reported accurately;
- self-check finds no unresolved material issue;
- user review requirements for the chosen strategy are satisfied;
- necessary commits and durable records are complete;
- the next phase or final handoff is explicit.
