# Pre-Spec Design

## Purpose

Use this mode when the user wants to discuss or shape a development design before writing the spec. Inspect the repo, resolve only the choices that affect the result, recommend a right-sized plan, and ask for confirmation where it is actually needed.

Entering this mode does not by itself authorize spec edits or code edits. A recommendation is not a decision, and a question from the user is not an instruction to change files.

## Working Rules

1. Inspect applicable repo instructions, the active spec or brief, relevant entry points, existing facilities, callers, tests, public surfaces, and conventions before asking questions the repo can answer.
2. Establish behavior before mechanism. Identify the requested result, its acceptance, and the owning path before proposing classes, helpers, files, or a migration sequence. Existing code is evidence and a possible facility, not a default work breakdown.
3. Use ordinary engineering judgment for private structure, naming, helper decomposition, routine library choices, and other choices already settled by the repo or common practice.
4. Ask only when the answer changes behavior, architecture, data meaning, ownership or lifetime, public compatibility, acceptance, work order, operating requirements, or product policy.
5. When an important choice remains, recommend one option and explain its practical effect before asking the user to decide. Choose the simplest useful planning depth; ask only when alternatives materially change the result or boundary.
6. Use ideas from mature systems as evidence about tradeoffs. Adopt their structure or machinery only when it solves a current need and fits this repo.
7. Do not invent scale, concurrency, recovery, compatibility, extensibility, or operational requirements. A broad future need is context for avoiding an obvious dead end, not a current demand for a complete future architecture.
8. Make material sources and choices visible when they matter. Do not silently turn an inference, historical design, or external analogy into settled design, and resolve a concrete conflict before relying on it.
9. Follow `spec-architecture.md` for planning depth and commit packaging; base the split on behavior and dependencies rather than source files or a target count.

## Method

### 1. Establish the whole

From the repo and the request, determine:

- the result the user wants and how it will be recognized;
- the existing facilities and real integration points;
- how one run moves from entry or input to result;
- important changes in data or state, identity, ownership, and lifetime;
- the code or component responsible for the operation;
- public behavior, failure rules, evidence-based compatibility obligations, and acceptance that must be stable.

Identify whether the task is new development, an incremental feature, a refactor, or a migration. Design new development from the target system and its real entry points. Before adding transition or compatibility work, identify the actual released surface, downstream user, persisted data, repo policy, or explicit commitment that requires it. Follow the compatibility guidance in `spec-architecture.md`.

Explain only the existing code and domain background needed to understand the design. Cite the rest.

### 2. Recommend the plan

Use the minimum plan shape in `SKILL.md` and the detailed criteria in `spec-architecture.md`. For a current phase, list the reasonably knowable steps, their order, and normal commit boundaries; a current step must have a result that can be checked without relying on unfinished future behavior. Defer private details that depend on later design. Use a task grouping only when one phase list is too large to manage.

### 3. Resolve important choices

For each unsettled point:

1. Follow repo evidence when it answers the question.
2. Apply useful principles from established practice, adjusted to this repo and task.
3. Prefer the simplest local design that meets the current requirements.
4. If reasonable choices change the result or an important boundary, recommend one option and explain the tradeoff.
5. Ask the user when product, domain, or personal policy is required.
6. Leave private implementation choices to the implementer.

A deferred important choice needs a safe current default and confirmation before the spec or code relies on it. If no safe current choice exists, the affected work is blocked.

### 4. Stop when the next step is clear

Stop expanding the design when the goal, whole flow, responsibilities, important contracts, acceptance, and the next ordered step are clear enough to implement and verify. Before implementation, make that step's result, dependencies, acceptance, and any split commit order clear. Lower-level private design that has not been reached is expected future work, not a defect to report.

## Report and Confirm

Use the reporting guidance in `spec-architecture.md`: establish the overall result and repo-based understanding, then show the breakdown, ordered steps, and reasons. Mention split commits when applicable. If a task grouping is needed, state only its local goal and ordered steps.

For the whole task, also explain one run from entry or input to result, important contracts, acceptance, and verification. For a task grouping or current step, state only its local goal and needed detail. Do not repeat the parent or create empty headings for a small task.

End with the key assumptions or defaults chosen by the agent, remaining material questions, and the reasons the execution steps are ordered that way. Ask for confirmation before authoring when the user requested discussion or assessment. A direct request to write or revise a spec authorizes that work after important choices are settled.

## Final Check

Before requesting confirmation, ask whether the repo was inspected, the whole precedes the parts, the ordered steps follow real dependencies, any task grouping is needed, future details remain future details, and every agent-made choice that could affect the result is visible.
