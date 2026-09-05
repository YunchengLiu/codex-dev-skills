---
name: task-handoff
description: >
  Keep compact current task state for continuation across conversations,
  pauses, context compaction, or agent handoff. Use during long or changing
  tasks when key decisions, progress, and the next action would be costly
  to reconstruct.
---

# Task Handoff

Maintain one concise handoff note so a task can continue across conversations.
Optimize for accurate, fast resumption: retain effective decisions and state,
with brief reasons only where they affect the next action.

Create or reuse a note when work spans several turns or execution cycles,
requirements change materially, or a pause, compaction, or handoff is likely.
Short local work needs one only when useful state would otherwise be lost.

## Find Or Create

If the handoff path is known, read it directly. Otherwise, inspect task
directories and notes in the user or project's designated location, defaulting
to `.agent-context/handoff/` in the workspace. Narrow candidates by name, then
read their goals and scopes to confirm they describe the same task. A shared
module or the latest modification time alone does not establish task identity.

Reuse the same file when the task continues, even if its wording, agent,
conversation, or phase changes. Preserve a matching record's existing location
unless the user requests a move. If no existing note matches, name a task
directory after the stable objective and use `session.md` for its handoff:
`.agent-context/handoff/<task>/session.md` by default. Resolve genuine ambiguity
with the user before reusing or creating a note.

Default to one handoff note per task; agents continuing it share the note and
coordinate writes. Use separate tracks when the user explicitly requests them.
Discover files directly without maintaining a separate registry or index.

## Task Working Files

Keep task-specific probe scripts, experiments, temporary inputs, and their
outputs together in the task directory, with subdirectories as needed. For an
existing standalone note, use an adjacent directory named after the task.
Project builds and maintained deliverables keep their configured or agreed
locations. Keep `session.md` concise: record useful conclusions and references
to the supporting files. Create only the files needed for the work.

## Record

Record only applicable fields:

- task, goal, scope, and effective constraints;
- key decisions and their still-relevant reasons;
- current progress and actual validation results;
- blockers, unresolved choices, and the concrete next action;
- essential file or document references.

Use short bullets and recognizable paths or identifiers. Omit empty fields,
discussion corrections, transcripts, raw output, and completed micro-steps.
Link to maintained source documents instead of duplicating their content.
Prefer repo-relative paths and stable URLs. Use a machine-specific absolute
path only when needed to locate the work unambiguously or when the path is
itself part of an external requirement.

## Update And Resume

Update after a material decision, scope change, validation result, or before
a pause or handoff. Replace stale conclusions instead of appending history.

On resumption, read the handoff note and verify time-sensitive facts against
current user instructions, repository state, and referenced artifacts. Correct
the note when those facts differ. A fresh agent should be able to identify the
current result, remaining work, and one next action without replaying the chat.
