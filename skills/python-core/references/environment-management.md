# Environment Management

Treat the Python environment as a first-order project constraint.

## Confirm the environment model first

- Check which interpreter the project expects and which environment model is already in use.
- Check which dependency and environment files already exist before recommending commands, for example `pyproject.toml`, `requirements*.txt`, lockfiles, or other established project metadata.
- Prefer the project's existing environment model over introducing a new one.
- If the interpreter, virtual environment, or package manager is unclear and it affects the work, inspect first and ask the user if the answer is still ambiguous.
- If no environment exists yet and the task needs one, confirm whether it should be created now and whether `venv`, `uv`, `conda`, or another tool should own it.

## Keep dependency management consistent

- In `conda` or `mamba` environments, confirm whether dependency installation should stay in that ecosystem before falling back to `pip`.
- In non-conda environments, `pip` or `uv pip` is usually the natural path unless the project says otherwise.
- Avoid casual mixed management because it makes environments harder to reason about and reproduce.
- Identify dependency ownership before recommending commands. Do not guess from the interpreter alone.

## Do not mutate environments silently

- Do not create a new virtual environment without user approval.
- Do not install, upgrade, or remove dependencies in the background.
- Do not switch the task onto a different interpreter or environment manager without making that choice explicit.
- Do not introduce or rewrite `pyproject.toml`, lockfiles, or environment manifests as a side effect of an unrelated change.

If the task needs those changes, explain why and get user approval first.

## Match recommendations to version reality

- Verify the target Python version before recommending syntax or typing features that are version-sensitive.
- Treat environment constraints as stronger than general Python feature advice.
- If a dependency or toolchain recommendation depends on version compatibility, check the relevant project or package documentation before presenting it as ready.
- If the effective Python version cannot be confirmed, prefer broadly supported syntax and ask before using version-edge language features.

## Use `pyproject.toml` when the project is large enough

- A one-off script usually does not need `pyproject.toml`.
- A small local tool may still be fine without it if the dependency story is simple and local.
- Once the code becomes a maintained tool, reusable module, or multi-file project with tests or tool configuration, `pyproject.toml` becomes a strong candidate.
- Use it to centralize project metadata, dependencies, and tool configuration when that reduces drift and makes the project easier to maintain.
