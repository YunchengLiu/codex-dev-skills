# Output Modes

Shape the brief for its executor. Ask who will use it or how much implementation
detail they need only when this is unclear and changes the result. These are
useful forms, not required templates.

## Human Brief

Lead with the requested outcome and recommended path. Include the scope,
constraints, decisive tradeoff, deliverable, and completion signal. Explain
enough reasoning for the user to judge the recommendation; keep implementation
detail secondary when they mainly want the result.

For example, a plan to organize local reports can name the source folder, the
classification rule, a preview of the proposed moves, and the condition for
applying them. It needs no project scaffolding or maintenance roadmap unless
the request actually calls for those.

## Agent Execution Brief

Assume the executor has no hidden conversation context. Carry the goal,
necessary evidence, settled choices, relevant inputs or workspace, affected
surfaces, ordered work, and acceptance signal. For development or refactoring,
include the behavior target, owning execution path, and integration boundary
that make the implementation order understandable.

For result-oriented work, concrete inputs, deliverables, acceptance, and
operating limits may be sufficient. Do not prescribe internal steps that the
executor can choose without changing the result.

State the authorized scope and any concrete stop conditions. Without broader
authorization, keep execution within the supplied workspace or artifacts;
global tool installs, system environment changes, unrelated locations, and
high-risk external actions require explicit authorization. Carry existing
authorization forward instead of inserting a new approval round.

## Fresh-Context Prompt

A prompt for a new session is self-contained and neutral. State the goal,
current verified state, requested work, settled constraints, deliverables, and
relevant execution limits. Express effective requirements directly, in natural
language suited to the executor, and retain only implementation details that
are settled or necessary to locate the work.

Ask the receiving agent to inspect the current project or supplied artifacts
and verify project-dependent facts. This confirmation is evidence gathering;
it does not reopen agreed decisions or require user approval that the task did
not otherwise need.

Use "current repo" or "current workspace" when the next session will start from
the target project. Include a concrete path when requested, when multiple
projects are involved, or when needed to avoid ambiguity. Never invent a path
or assume the present working directory will be the later execution directory.

Keep discussion history and superseded corrections out. State each still-active
constraint as a current requirement. Include design conclusions only when they
are verified and implementation choices only when they are settled requirements.
