# Output Modes

Match the output shape to the intended executor.

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

## LLM-facing brief

Prefer:

- Task goal
- Relevant context
- Explicit repository, path, or workspace context when it matters
- Scope and non-goals
- Constraints and operating rules
- Expected output
- Completion criteria

Assume the receiving LLM has no hidden context.
Do not assume the current working directory or chat workspace in this thread is the same as the later execution directory unless that is explicitly stated.

## Fresh-context prompt

When the user asks for a prompt for another LLM:

- Make it self-contained.
- Do not rely on this conversation.
- Keep it concise but sufficient.
- Include only the context and rules that materially affect execution.
- State path or workspace assumptions explicitly when they matter.
