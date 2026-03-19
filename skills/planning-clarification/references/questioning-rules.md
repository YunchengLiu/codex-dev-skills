# Questioning Rules

Ask less, but ask better.

## Good question targets

- Intended deliverable
- Execution owner: human or LLM
- Execution context when it changes the plan or prompt shape
- Whether there is a real repository, file set, or workspace to inspect now
- Scope boundaries and non-goals
- Constraints that change the plan
- Missing local facts the user is best positioned to supply

## Good question style

- Keep questions short and easy to answer.
- Prefer one to three questions at a time.
- Ask about decisions, not essays.
- Use the current understanding summary to show what is already understood.
- Let the agent own obvious inspection and triage choices instead of bouncing them back to the user.

## Avoid

- Asking the user to restate the whole task
- Turning clarification into a template or form
- Asking about details that do not affect the plan
- Reconfirming obvious facts from the current request
- Repeatedly asking whether to inspect local context when the agent can determine that itself
- Asking speculative future-state questions unless they materially change the current scope
