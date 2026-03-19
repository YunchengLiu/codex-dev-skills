# Task Profiles

Start by placing the task in the lightest honest bucket.

## One-off script

- Good fit for a single file or a very small helper module.
- Focus on readable inputs, outputs, paths, and failure messages.
- Do not add package scaffolding, plugin layers, or heavy configuration unless the user already needs them.
- Usually no need for `pyproject.toml` unless the script is already turning into a maintained local tool.

## Small local tool

- Good fit for a clear entry point plus a few helper modules.
- Add lightweight CLI parsing, logging, or config only when they improve repeated use.
- Keep the structure obvious enough that the tool can grow later without a rewrite.
- Consider `pyproject.toml` once dependencies, tool configuration, or repeatable invocation start to matter.

## Notebook-backed analysis

- Use notebooks for exploration, inspection, and presentation.
- Move stable data loading, transforms, plotting utilities, and core algorithms into `.py` files once they start to repeat.
- Keep runtime assumptions explicit: paths, seeds, output locations, and environment-sensitive settings.

## Reusable module or library

- Favor clearer boundaries, stable function signatures, and lightweight tests.
- Add package structure, basic typing, and small internal organization once reuse is real rather than speculative.
- Prefer a small public surface over many weakly justified helpers.
- A `pyproject.toml` file is usually a good fit once the code has project-level metadata, dependencies, or tool configuration to keep in one place.

## Maintained application or tool

- Add more structure only where it pays off: package layout, CLI or UI boundaries, configuration, logging, tests, and dependency discipline.
- Keep modules responsibility-driven rather than template-driven.
- Align with existing project layout before introducing a new local style.
- Prefer `pyproject.toml` when the project has clear dependency, tooling, or packaging needs.
