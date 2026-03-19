# Structure Principles

## Keep the main path readable

- Make it easy to find data loading, model creation, training, evaluation, inference, logging, and output handling.
- Keep the control flow understandable after metrics, logging, and checkpoint support are added.
- Prefer direct code paths over clever indirection for ordinary experiment logic.

## Allow simple centralized configuration early

- A dedicated Python file with low-frequency, mostly read-only globals can be acceptable in early phases if it keeps the experiment easy to adjust.
- Do not introduce serialization layers, complex config systems, or argument surfaces before the task really needs them.
- Keep the structure organized enough that the current configuration style can later be consolidated without a rewrite.

## Add structure only when it pays off

- Add clearer module boundaries once logic starts repeating or the main file becomes hard to follow.
- Add argument parsing when local and remote execution or repeated reruns need a more stable interface.
- Add stronger organization when the current shape starts to slow down iteration or make mistakes likely.
- Notebook-based exploration can be acceptable early, but once logic is rerun or shared repeatedly, move stable parts into scripts or modules and let notebooks stay thin.

## Simplest is best

- Prefer the simplest structure that keeps the experiment understandable, portable, and recoverable.
- Do not confuse roughness with failure if the current form is clear and easy to evolve.
