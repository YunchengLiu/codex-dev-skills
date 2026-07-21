# codex-skills

Personal Codex skills shaped around my own day-to-day workflow.

Most of them are meant to stay reusable across projects, but they are still personal: they reflect the kinds of tasks I do often, the defaults I prefer, and the ways I want Codex to stay focused.

## Scope

This repository mainly covers:

- language and build-system guidance
- planning and work-tracking helpers
- spec-focused design, authoring, and implementation guidance
- AI experiment and PyTorch implementation guidance
- note-taking and personal knowledge capture

## Existing Skills
- `planning-clarification`: For talking through vague ideas and turning them into a clearer execution direction.
- `use-subagents`: For deciding when subagents add value and dispatching concise, conclusion-neutral independent work.
- `personal-markdown-note-writer`: For turning discussion results and scattered notes into long-lived Chinese personal notes.
- `plan-progress-tracker`: For maintaining the smallest useful on-disk plan and handoff state across sessions or agents.
- `spec-driven-dev`: For converging pre-spec design, writing minimal rigorous specs, and implementing them through gated or authorized autonomous workflows.
- `modern-cpp`: For modern C++ feature choices and incremental migration tradeoffs.
- `modern-cmake`: For modern CMake structure, migration, and build-system decisions.
- `ai4science`: For landing and iterating on AI4Science experiment code without overengineering it.
- `pytorch`: For single-machine PyTorch implementation details with a bias toward native, readable, reliable patterns.

## Repo Layout

```text
skills/
  <skill-name>/
    SKILL.md
    agents/
    references/
    scripts/
    assets/
```

Each skill keeps its own instructions and any related resources inside its own folder.

## How To Use

1. Clone this repository on the machine where you use Codex.
2. Copy or sync the skill folders you want into `$CODEX_HOME/skills`.
3. Use the skills by name in prompts when needed. Some skills may also be eligible for implicit selection when their descriptions match the task, while more policy-oriented skills may intentionally require explicit `$skill-name` invocation.

Current example:

```text
skills/modern-cpp/
```

That folder can be synced into:

```text
$CODEX_HOME/skills/modern-cpp/
```
