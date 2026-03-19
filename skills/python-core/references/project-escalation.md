# Project Escalation

Scale the structure with the task instead of front-loading full project machinery.

## Keep it light when

- The script is local, short-lived, or exploratory.
- The user mainly wants something runnable now.
- Reuse is limited to a small amount of obvious helper extraction.
- Packaging, installation, distribution, or reuse by other projects is not part of the current need.

## Add structure when

- Logic is being copied between scripts or notebooks.
- The code now has multiple entry points or multiple consumers.
- Inputs, outputs, configuration, and side effects need to be easier to reason about.
- The user expects the code to be rerun, shared, or maintained over time.
- Dependencies, tool configuration, or project metadata are now substantial enough that `pyproject.toml` would clarify the project better than scattered ad hoc files.

## Typical escalation path

1. Start with a clean script.
2. Extract stable logic into local helper functions.
3. Split repeated logic into one or more small modules.
4. Add `pyproject.toml` once project metadata, dependencies, or tool configuration need a stable home.
5. Add a package layout, tests, configuration, or CLI boundaries only when the current shape starts to fight the task.

Do not skip directly from a simple script to a full project template unless the user already has that level of requirement.
Do not use that escalation as a reason to switch packaging or dependency tools unless the user actually wants to change them.
