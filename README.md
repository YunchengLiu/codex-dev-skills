# codex-dev-skills

My personal Codex skills for day-to-day development tasks.

These skills are intended to stay cross-project and reusable. They are built and iterated with Codex, with help from the `skill-creator` skill when scaffolding and refining new skills.

## Scope

This repository is for general development workflows, for example:

- Modern C++
- CMake
- Build and test workflows
- Language-specific engineering guidance

Repository-specific conventions should stay with the target repository instead of this one.

## Layout

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
3. Use the skills by name in prompts when needed, or let Codex pick them when their descriptions match the task.

Current example:

```text
skills/modern-cpp/
```

That folder can be synced into:

```text
$CODEX_HOME/skills/modern-cpp/
```

## Workflow

- Add or refine skills here.
- Keep them under version control.
- Reuse the same repository across machines.
- Publish the repository to GitHub when the skills are ready to share.
