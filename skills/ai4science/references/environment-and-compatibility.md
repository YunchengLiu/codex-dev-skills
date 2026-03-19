# Environment and Compatibility

## Confirm the active stack first

- Check Python version, framework version, accelerator stack, and target execution environment before recommending features or commands.
- Inspect existing environment and dependency manifests first rather than guessing from a shell or interpreter alone.
- Identify whether the work is meant for local debugging, remote servers, or both.

## Dependency changes need explicit approval

- Do not silently create environments, install dependencies, or switch dependency ownership.
- Follow the project's existing dependency mechanism when possible.
- If compatibility is uncertain, inspect first and ask the user before proposing changes as ready.

## Portability matters early

- Avoid hard-coding local paths, devices, and shell-only assumptions.
- Keep run entry points and arguments understandable enough to move from local debugging to server execution without hand-editing core code.
- Prefer changes that reduce environment drift between local and remote workflows.

## Version and framework caution

- If the effective version or compatibility matrix cannot be confirmed, stay with broadly supported patterns or ask the user before relying on newer behavior.
- Verify framework-specific compatibility and runtime assumptions against official documentation when they matter.
