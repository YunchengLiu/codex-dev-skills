# Dispatch Patterns

Delegation prompts should reduce guessing and preserve independence.

## Required elements

- Task goal
- Task type
- Scope
- Non-goals
- Relevant context or artifacts
- Operating boundaries
- Expected output
- Completion criteria

## Minimal template

```text
Goal:
Task type:
Scope:
Non-goals:
Relevant context:
Operating boundaries:
Expected output:
Completion criteria:
```

## Neutrality rules

- Do not tell a review subagent what conclusion to reach.
- Avoid loaded wording such as "confirm that this is correct" unless the task is specifically a verification against a known standard.
- Prefer "assess", "review", "analyze", "challenge", or "identify issues" over "approve".
- Pass raw artifacts when possible instead of summarizing them with your own interpretation first.

## Output shaping

Use a minimal common structure when results need comparison. Keep it short and task-shaped.

Suggested shared fields:

- Conclusion
- Evidence or reasoning
- Risks or uncertainties
- Recommended next step

Add task-specific fields only when helpful:

- Review: findings, severity, affected areas
- Design critique: tradeoffs, rejected assumptions
- Verification: checks performed, pass or fail conditions
- Command review: potential impact, rollback or protection concerns
