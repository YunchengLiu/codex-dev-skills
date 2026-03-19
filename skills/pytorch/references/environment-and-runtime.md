# Environment and Runtime

## Confirm the stack first

- Check Python version, PyTorch version, accelerator backend, device availability, and relevant driver context before recommending runtime-sensitive changes.
- Inspect existing environment and dependency manifests before recommending installs or upgrades.
- Prefer concrete runtime evidence over memory when compatibility is uncertain.

## Environment changes need explicit approval

- Do not silently create environments or install or upgrade packages.
- Do not assume the current runtime stack is correct just because imports succeed.
- If the work depends on runtime compatibility, verify first and ask the user when changes are needed.

## Prefer concrete diagnostics

- For environment debugging, prefer collecting real PyTorch runtime information before offering fixes.
- Use official runtime and environment reporting tools when available.
- Verify compatibility-sensitive advice against official PyTorch documentation when needed.
