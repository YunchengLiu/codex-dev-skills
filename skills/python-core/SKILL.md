---
name: python-core
description: Use pragmatic Python across projects. Use when Codex needs to clarify whether Python code should stay a script, become a small module, or grow into a maintainable tool; decide whether Python language or standard-library features fit the active version and environment; or keep notebook-backed and script-heavy work clear without overdesigning lightweight tasks.
---

# Python Core

## Overview

Use this skill as the general baseline for Python work. Favor clear organization, simple data flow, and standard-library-first solutions, then add more structure only when the task actually needs it.

## Workflow

### 1. Establish the Python environment first

- Check which Python interpreter and environment model the task is using: system Python, `venv`, `uv`, `conda`, `mamba`, or an existing project-managed environment.
- Confirm the target Python version before recommending version-specific syntax, typing features, tooling, or dependencies.
- Inspect the existing project manifests and dependency files before recommending dependency commands or workflow changes, for example `pyproject.toml`, `requirements*.txt`, lockfiles, or other established environment metadata.
- If the current environment is unclear and it affects the recommendation, inspect first. If it is still unclear, ask the user before assuming how the project should be run or managed.
- If the project does not yet have an environment and the task needs one, confirm whether the user wants it created now and which tool should own it.
- Do not silently create environments, switch interpreters, or install dependencies.
- If the task needs dependency changes, get user approval first and keep the dependency path consistent with the active environment model.
- In `conda` or `mamba` environments, confirm whether dependency management should stay there before reaching for `pip`. Avoid casual mixed management unless the user explicitly wants it.

Read [references/environment-management.md](references/environment-management.md) when environment handling, dependency installation, or version targeting matters.

### 2. Establish the task profile first

- Check whether the task is a one-off script, a small local tool, a notebook-backed analysis, a reusable module, or a longer-lived application.
- Confirm present-day needs before recommending structure: reuse, tests, packaging, CLI entry points, configuration, logging, data files, or distribution.
- If the code is already part of an existing project, align naming, layout, and organization with the established project unless the user asked for a broader refactor.
- Do not force package structure or framework-style layering onto lightweight tasks that only need to run once or stay local.

Read [references/task-profiles.md](references/task-profiles.md) when the task shape or maintenance horizon is unclear.

### 3. Prefer simple structure with clear extension points

- Start with the lightest structure that meets the current need.
- Keep the code easy to grow: separate core logic from ad hoc entry-point code, keep data flow explicit, and avoid hidden global state.
- Add modules, packages, CLI parsing, configuration files, reusable helpers, or `pyproject.toml` when they reduce repetition or clarify boundaries, not as default ceremony.
- Avoid both extremes: do not leave evolving code as an unstructured blob, and do not scaffold full project machinery without a real need.

Read [references/project-escalation.md](references/project-escalation.md) for when to keep a script lightweight and when to scale it up.

### 4. Use Python's built-in capabilities well

- Prefer standard-library facilities and clear language features before reaching for custom helpers or extra dependencies.
- Use `pathlib`, `dataclasses`, `enum`, `contextlib`, `logging`, `argparse`, `typing`, and other built-in tools when they make intent clearer.
- Prefer clear functions, explicit data structures, and readable control flow over clever indirection.
- Use newer Python language features when they improve clarity and the target version supports them, but keep clean code first. Do not chase the newest syntax when it adds complexity without enough payoff.

Read [references/design-principles.md](references/design-principles.md) for the default style and organization rules.

### 5. Keep notebooks and data workflows honest

- Use notebooks for exploration, inspection, and presentation, not as the only home for stable core logic.
- When code starts to stabilize, move core computation, loading, transformation, or plotting helpers into `.py` modules and let notebooks stay thin.
- Keep input paths, output paths, generated artifacts, and cache locations explicit instead of scattering them across cells or helper scripts.
- Prefer repeatable script or module entry points once an analysis or workflow needs to be rerun reliably.

Read [references/notebooks-and-data.md](references/notebooks-and-data.md) when the task mixes notebooks, scripts, data processing, or visualization.

### 6. Pull in feature guidance only when needed

- Read [references/feature-candidates.md](references/feature-candidates.md) when deciding whether a Python language or standard-library feature is worth adopting.
- If the effective Python version cannot be confirmed, stay with broadly supported constructs or ask the user before using newer syntax.
- If version support, library behavior, typing semantics, or platform behavior are uncertain, verify against official Python documentation or the relevant library documentation before presenting a recommendation as ready.

### 7. Recognize when this skill stops being the main one

- Use `python-core` as the baseline for general Python structure, environment discipline, and language or standard-library choices.
- If framework behavior, scientific stack behavior, notebook kernel setup, or domain-library semantics become the main problem, say that the task has moved beyond `python-core` alone.
- In those cases, recommend bringing in a more specific skill if one is available, or inspect available skills and other authoritative guidance before proceeding as if this skill were sufficient on its own.

Do not turn this skill into a Python language manual. Read only the reference files needed for the current task.

## Response Expectations

When recommending or applying a Python change:

- State the active or intended Python environment model and target version when they matter.
- State the task profile and current maintenance needs.
- Explain why the suggested structure or feature is worth adopting now.
- Identify the main version, environment, dependency, readability, or maintenance risks.
- Say whether the recommendation should be applied now, deferred, or left as a future cleanup.
- Flag any environment creation, dependency installation, or environment-manager change that needs explicit user approval.
- Say when the task has crossed into framework- or domain-specific territory that needs more than `python-core`.
- Prefer small, clear changes unless the user explicitly asks for a broader redesign.
