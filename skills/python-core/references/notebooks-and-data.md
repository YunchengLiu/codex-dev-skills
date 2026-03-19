# Notebooks and Data

## Use notebooks for the right job

- Notebooks are good for exploration, visualization, and narrative presentation.
- They are a weak place to hide the only copy of stable logic, data loading rules, or export behavior.

## Move stable logic out gradually

- Extract repeated cell logic into `.py` modules once it starts to stabilize.
- Keep the notebook focused on orchestration, inspection, and presentation.
- Prefer rerunnable helpers over copy-pasted cells across multiple notebooks.

## Make data flow explicit

- Keep input paths, output paths, cache paths, and artifact paths easy to locate.
- Do not scatter path literals and ad hoc directory creation across many cells or helper files.
- Keep generated figures, tables, exports, and intermediate files organized enough to rerun the workflow.

## Prefer repeatable execution when needed

- If an analysis is rerun often, add a script or module entry point instead of relying on manual notebook state.
- If results depend on seeds, sampling, environment settings, or version-sensitive behavior, make those assumptions visible.
- If notebook execution depends on a specific kernel or interpreter, confirm that it matches the intended environment before recommending reruns or extraction work.
