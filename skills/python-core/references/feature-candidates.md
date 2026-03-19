# Feature Candidates

Use this file as a reminder list, not as a complete Python reference.

## Language features worth considering

- `f`-strings for readable formatting.
- Assignment expressions when they simplify a local flow instead of obscuring it.
- `match` for structured dispatch when it is clearer than long `if` or `elif` chains.
- `|` unions and modern type syntax when the target version and tooling support them.
- `ExceptionGroup` and `except*` only when concurrent or batched error handling really needs them.

## Standard-library features worth considering

- `pathlib` for path handling.
- `dataclasses` for lightweight structured data.
- `enum` for named discrete modes or states.
- `contextlib` for scoped resource management.
- `argparse` for small and moderate CLI needs.
- `logging` for repeated tools or scripts that need diagnosable output.
- `functools`, `itertools`, and `collections` when they reduce local boilerplate without hiding intent.

## Use with restraint

- Heavy type machinery that makes ordinary code harder to read.
- Decorator and descriptor patterns when plain functions or small classes would be clearer.
- Asynchronous structure when the task is fundamentally synchronous.
- Framework-style plugin systems in scripts or tools that do not need them.

## When uncertain

- Verify target Python version support before recommending newer syntax.
- Verify that the active environment model can support the proposed dependency or tool flow.
- Verify library-specific behavior against official documentation when typing, platform behavior, or semantics are unclear.
- If the Python version is unknown, prefer broadly supported constructs over version-edge syntax.
- Prefer the Python docs and relevant tool or packaging docs over memory when syntax, typing, or packaging behavior is version-sensitive.
- Prefer a simpler pattern if the newer feature does not clearly improve readability or maintainability.
