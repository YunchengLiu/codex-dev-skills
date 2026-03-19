# Reproducibility and Artifacts

## Make reruns practical

- Keep run parameters, seeds, input assumptions, and important outputs visible enough to rerun the experiment.
- Logging and metrics should help explain what happened without obscuring the main logic.
- Prefer simple, readable output rules over premature output infrastructure.
- Increase provenance with the stage:
  - early work: keep essential params, seeds, and key outputs visible
  - repeated experiments: also track the data source, important split or preprocessing assumptions, and the effective run configuration
  - mature comparisons: capture dataset identity or version, preprocessing or split definitions, code revision, and important runtime context alongside outputs

## Early-stage checkpoints and artifacts

- In early phases, saved state is often mainly for backup, recovery, and quick inspection.
- A single output directory plus a few clearly named files can be enough.
- Do not overdesign directory trees, schemas, or save formats before the workflow needs them.

## Tighten gradually

- As the experiment becomes more repeatable, clarify naming, saved metadata, and resume behavior.
- As comparisons become more systematic, make artifacts easier to line up across runs.
- Only push for stronger compatibility guarantees once the workflow is mature enough that format stability matters.

## Keep portability in mind

- Avoid output rules that only work on one machine or one directory layout.
- Keep local and remote run outputs organized enough that movement between them stays manageable.
