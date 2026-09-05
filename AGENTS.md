# Skill Maintenance

Write reusable personal skills around the tasks they help an agent perform.
Keep their instructions neutral across agent runtimes and put runtime metadata
in its designated adapter files.

## Editing

- Establish when the skill should apply, what it should help the agent do, and
  what result would demonstrate useful guidance.
- Explain the workflow top-down with direct language. Preserve the meaning,
  force, defaults, exceptions, and useful examples of sound existing rules.
- State the required behavior, conditions, and result positively. Reserve
  negative wording for concrete prohibitions and essential boundaries.
  Discussion corrections and temporary task notes must not enter reusable
  instructions; express their lasting implications as current requirements.
- Use fluent, idiomatic language in both instructions and the collaboration
  they guide. Establish the facts and structure first, then polish the wording
  while preserving every requirement and mechanical rule.
- Keep each skill sufficient for its own task. Allow useful overlap;
  link substantial shared material where it actually serves the reader.
- After a change, compare with the earlier or simpler form. Keep additions that
  improve decisions or prevent a likely misunderstanding; remove repetition
  that adds neither. Clarity and rule strength take priority over length.

## Verification

Run the skill validator and check references and runtime metadata. For changes
to guidance or discovery, try realistic requests and assess the resulting
decisions. Use independent review when it adds useful coverage.
