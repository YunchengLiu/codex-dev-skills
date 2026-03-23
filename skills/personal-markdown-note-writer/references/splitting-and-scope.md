# Splitting and Scope Rules

## When to split

Split the material into distinct sections by default when it mixes distinct intents. Only split into multiple files if the user explicitly asks. Typical patterns:

- “Teach the concept” + “reverse engineer a specific repo/app”
- “Fundamental theory” + “UI/call chain tracking”
- “Algorithm explanation” + “engineering checklist”
- “Tool usage” + “deep theory”

If in doubt, optimize for:

- Each note answers one main question.
- Each note can be read independently.

Default output behavior:

- Keep a single output file by default: split as multiple top-level sections in one Markdown file.
- Only split into multiple files if the user explicitly asks for multiple outputs.

## Suggested split outcomes

Common outcomes that work well:

- One top-level section for the core concept (`learning-note`)
- One top-level section for the reproduction steps (`tool-note`)
- One separate top-level section (optional) for code call chains / system-specific details

## Scope discipline

- Keep the note focused on what you want to remember and reuse.
- Move long raw excerpts into:
  - an `Appendix` section, or
  - a separate “reference dump” note only when the user explicitly wants multiple output files.
- Prefer stating the main conclusion, then keep only the minimum supporting detail.
