# Task Selection

Use subagents selectively. The default is still a direct main-agent pass.

## Good fits

- Independent code review of a non-trivial change
- Design or architecture critique where alternative interpretations matter
- Debugging hypotheses that benefit from separate reasoning passes
- High-risk command review or migration-risk confirmation
- Comparing algorithmic approaches or tradeoffs
- Research planning or execution-briefing that benefits from an independent challenge pass

## Weak fits

- Small local edits with obvious acceptance criteria
- Simple command execution or rote file manipulation
- Strongly sequential tasks where the next step depends on the exact previous result
- Tasks blocked on missing repository context or missing user requirements
- Situations where the main agent already has enough confidence and an extra pass is unlikely to add new information

## Choosing a pattern

- No subagent:
  Use for routine tasks, tightly coupled execution, or low-risk work.
- One bounded subagent:
  Use for a single independent check, a focused side analysis, or a clearly separable support task.
- Two independent subagents:
  Use for high-value review, design tradeoff critique, ambiguous debugging hypotheses, or other cases where comparing independent perspectives is worth the cost.

## Fresh vs reused context

- Prefer fresh context for independent review, design critique, or contradiction checking.
- Reuse an existing subagent only when its accumulated context is directly helpful and does not bias the outcome.
- If independence matters more than continuity, start fresh.
