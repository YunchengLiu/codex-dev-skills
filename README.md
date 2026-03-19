# codex-dev-skills

Reusable Codex skills for development workflows.

This repository is intended to serve two goals:

- Keep a curated set of cross-project skills under version control.
- Make it easy to install the same skill set on multiple machines.

## Scope

The repository is for general-purpose development skills, such as:

- Modern C++
- CMake
- Build and test workflows
- Language-specific engineering guidance

Repository-specific rules should stay in the target project instead of this repository.

## Layout

The repository will grow around a simple structure:

```text
skills/
  <skill-name>/
```

Each skill is expected to contain its own `SKILL.md` and any related references, scripts, or assets.
