---
name: ai4science
description: >
  Guide stage-aware Python AI and AI4Science experiment work: clarify the
  experiment stage, evaluation protocol, representation design, module
  boundaries, logging, artifacts, and framework reuse while keeping the current
  implementation minimal, explicit, and repo-context driven.
---

# AI4Science

## Purpose

Use this skill to land and iterate on Python-based AI and AI4Science experiment
code while keeping small experiments clean, explicit, and easy to evolve. The
skill keeps the current repo and current scientific question in charge: inspect
the local context, identify the smallest useful model of the problem, then add
only the structure that carries clear meaning for the current question.

## Core Rules

- Use the current experiment stage as the primary design input.
- Inspect relevant repo code, data flow, and existing conventions before
  proposing structure, fields, artifacts, or dependency changes.
- Keep the first working design low entropy: use the fewest modules, dimensions,
  configuration entries, and artifacts that make the current workflow clear and
  rerunnable.
- Model the common structure of the problem before naming fields. Treat a
  low-information flag as a signal to search for a better shared representation.
- Add core dimensions when they express stable, meaningful properties or
  relations of the problem. Keep values derived when they are cheaper and
  clearer to compute at the use site.
- Split clear workflow stages by responsibility when they have distinct inputs,
  outputs, tests, or replacement points. Keep the runner thin.
- Keep logging, checkpoints, metrics, and artifacts low entropy: record values
  that are needed to understand, compare, rerun, or debug the current workflow.
  Add richer provenance only when the experiment stage requires it.
- Keep a short single file only when the repo is exploratory, the flow is small,
  and local functions are enough to keep IO, processing, modeling, and reporting
  understandable.
- Confirm metric, split, and leakage assumptions before changing train/eval
  logic.
- Keep holdout test data for final reporting, not model selection or iterative
  feature tuning.
- Ask before installing packages, creating environments, changing dependency
  ownership, or relying on compatibility-sensitive framework behavior.

## Required Workflow

1. Establish the stage: early setup, local debugging, active iteration, mature
   comparison, or repeatable workflow.
2. Inspect the relevant local context: entry points, data paths, transforms,
   model/evaluation code, outputs, and dependency files.
3. Run the representation checkpoint when the task involves feature extraction,
   classification, preprocessing, schema design, or new fields.
4. Identify natural stages and choose the smallest clear decomposition. Prefer
   stage-owned functions or modules over a large catch-all file when boundaries
   are already visible.
5. Confirm scientific-integrity basics before train/eval changes: primary
   metric, validation protocol, split ownership, and leakage risks.
6. Reuse mature framework-native infrastructure before inventing local
   experiment machinery.
7. Add logging, checkpoints, and artifacts only to the depth needed for the
   current stage.
8. Report the chosen stage and remaining open assumptions before or alongside
   implementation. Include representation and decomposition only when they
   affect the current task.

## Decision Checkpoints

Pause and present a compact design note before coding when:

- the user asks for feature extraction, classification, analysis variables, or a
  new data schema but has not stated the modeling assumptions;
- the implementation would add several dimensions, flags, configuration keys,
  log fields, artifact files, checkpoint entries, metrics, or
  artifact types;
- a sample has unusual properties that could become fixture-only fields;
- a clear workflow can be decomposed into IO, processing, model/inference, and
  reporting stages, but the repo does not already show the preferred boundary;
- the metric, split, or leakage assumptions would change the implementation.

Use this compact form:

```text
Observed entities:
Natural relations:
Downstream decision/report:
Minimal representation:
Derived fields:
Recommended smallest design:
Open question:
```

## Reference Routing

- `references/stage-principles.md`: read when the experiment stage controls how
  much structure to add.
- `references/representation-and-decomposition.md`: read before adding feature
  fields, schemas, stage modules, or pipeline structure.
- `references/environment-and-compatibility.md`: read when runtime, dependency,
  or portability choices matter.
- `references/ecosystem-and-reuse.md`: read before building local framework
  machinery.
- `references/structure-principles.md`: read when balancing clear decomposition
  against needless architecture.
- `references/reproducibility-and-artifacts.md`: read when outputs,
  checkpoints, logs, or reruns are part of the task.
- `references/boundaries.md`: read when the task may be PyTorch mechanics,
  scientific validity, or another specialized domain instead of experiment
  workflow.

## Self-check

Before finalizing a recommendation or patch, verify:

- the chosen structure matches the current experiment stage;
- every new field, dimension, log entry, artifact, checkpoint entry, or metric
  has a current purpose for understanding, comparing, rerunning, or debugging;
- low-information flags have been replaced by a common representation or kept
  outside the core model with a stated reason;
- IO, preprocessing, modeling/classification, and reporting boundaries are clear;
- metric, split, and leakage assumptions are stated or explicitly blocked;
- the design leaves repo-specific implementation details to the current code
  context instead of imposing a generic framework.

## Response Expectations

State the inferred experiment stage and why the chosen level of structure is
sufficient now. Include minimal representation or decomposition only when the
task involves fields, features, preprocessing, classification, or pipeline
boundaries. Flag dependency/environment changes for approval. When modeling
assumptions are missing, ask a small number of concrete questions or present the
smallest design with explicit `TBD` points instead of inventing fields.
