# codex-dev-skills

My personal Codex skills for day-to-day development tasks.

These skills are intended to stay cross-project and reusable. They are built and iterated with Codex, with help from the `skill-creator` skill when scaffolding and refining new skills.

## Scope

This repository is for general development targets, for example:

- C++/Python/etc: modern language features and best practices
- CMake/etc: build system best practices
- Some best-practice for engineering guidance

## Existing Skills
- `modern-cpp`: A practical reminder layer for modern C++ work. It should nudge Codex toward better-fit language or library features when they are worth it, but still stay grounded in project constraints, toolchain reality, and stable interface boundaries.
- `modern-cmake`: A practical reminder layer for modern CMake work. It should keep new and existing build systems target-based and demand-driven, without turning simple projects into overdesigned package scaffolding.
- `python-core`: A lightweight foundation for general Python work. It should keep scripts, small tools, and notebook-backed code clear and appropriately structured, while staying honest about Python versions, environments, dependency flow, and where a more specific skill is needed.

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
3. Use the skills by name in prompts when needed, or let Codex pick them when their descriptions match the task.

Current example:

```text
skills/modern-cpp/
```

That folder can be synced into:

```text
$CODEX_HOME/skills/modern-cpp/
```
