# Design Principles

## Prefer standard-library-first solutions

- Reach for `pathlib`, `json`, `csv`, `sqlite3`, `argparse`, `logging`, `dataclasses`, `enum`, `contextlib`, `collections`, and `itertools` before adding dependencies.
- Add external libraries when they clearly reduce real work or unlock required capability.
- Do not pull in packaging, linting, typing, or workflow tools by default. Add them when the task has grown enough to justify the overhead.

## Keep code readable

- Prefer small functions with explicit inputs and outputs.
- Keep data transformations visible instead of hiding them behind unnecessary abstractions.
- Avoid clever control flow or metaprogramming for ordinary Python tasks.

## Use Python features where they help

- Use `dataclass` for simple structured records.
- Use `pathlib` for filesystem work.
- Use `match` when it clarifies multi-shape dispatch and the version supports it.
- Use type hints where they help clarify boundaries, returned shapes, or non-obvious contracts.
- Use context managers to make resource lifetime explicit.

## Keep state honest

- Avoid hidden mutation through globals, broad module state, or notebook-only variables.
- Prefer passing explicit values over relying on ambient state.
- Make side effects, file writes, and cache usage visible from the call path.

## Let organization follow the task

- A simple script can stay simple.
- A small tool can use a few clear modules without becoming a framework.
- A reusable package should still keep its public surface narrow and understandable.
- If the code starts to accumulate dependencies and tool configuration, let `pyproject.toml` carry that load instead of scattering settings across the project.
