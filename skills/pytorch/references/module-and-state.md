# Module and State

## Prefer native module patterns

- Use ordinary `nn.Module` structure unless a heavier abstraction is clearly justified.
- Keep parameterized submodules, buffers, and reusable blocks explicit enough to inspect and debug.
- Avoid inventing custom framework layers for simple composition.
- For common module, save, and load patterns, prefer PyTorch's official documentation, `pytorch/examples`, and other mature, reliable implementations before introducing local conventions.

## Keep save and load behavior explicit

- Prefer `state_dict`-based save and load flows unless there is a concrete reason to do something else.
- Make it clear which parts of the run state are saved: model, optimizer, scaler, scheduler, step or epoch counters, or other relevant state.
- Keep resume behavior understandable instead of hiding it behind too much machinery.

## Avoid fragile state assumptions

- Be careful with device-specific loads, module-name drift, and hidden coupling between checkpoint format and code layout.
- Tighten state rules as the project begins to depend on stable resume behavior, but do not overbuild checkpoint systems for trivial prototypes.
