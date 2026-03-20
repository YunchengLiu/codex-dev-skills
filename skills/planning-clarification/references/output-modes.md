# Output Modes

Match the output shape to the intended executor and the user's interest in implementation detail.

## Human-facing brief

Prefer:

- Goal
- Scope
- Non-goals
- Constraints
- Unknowns or assumptions
- Recommended path
- Deliverables
- Completion criteria

Keep it easy to scan and decision-oriented.
When the user is mainly result-oriented, keep implementation detail secondary.

## LLM-facing brief

Prefer:

- Task goal
- Relevant context
- Explicit repository, path, or workspace context when it matters
- Scope and non-goals
- Constraints and operating rules
- Execution boundaries, including which local actions are allowed by default and which actions require explicit approval
- Expected output
- Completion criteria

Assume the receiving LLM has no hidden context.
Do not assume the current working directory or chat workspace in this thread is the same as the later execution directory unless that is explicitly stated.

## Result-oriented execution brief

When the user mainly wants the final result rather than the implementation detail, prefer:

- Goal
- Required inputs or local artifacts
- Explicit workspace or path scope when it matters
- Acceptance criteria
- Deliverables
- Stop-and-ask conditions
- Execution boundaries, especially any prohibition on global installs, system changes, unrelated file access, or high-risk external actions

Keep implementation detail brief unless it is necessary to complete the task safely.

## Fresh-context prompt

When the user asks for a prompt for another LLM:

- Make it self-contained.
- Do not rely on this conversation.
- Keep it concise but sufficient.
- Include only the context and rules that materially affect execution.
- Include execution boundaries explicitly when the later agent may act on the local machine or local files.
- State path or workspace assumptions explicitly when they matter.
