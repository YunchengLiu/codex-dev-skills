# Spec Architecture

## Binding Rules

- Start every non-trivial spec task with repo-aware architecture analysis.
- Decide the document layout before writing detailed spec text.
- Classify the task as refactor, incremental feature, or new development.
- Map the spec to concrete repo locations: modules, public APIs, tests, fixtures, and existing spec conventions.
- Separate stable contracts from dynamic execution records at the architecture level.
- Plan execution slices so each phase brief contains the current phase's necessary facts.
- Plan concrete execution boundaries before private implementation mechanics.
- Identify whether the feature is repo-local, limited-domain, or general-purpose before choosing document and implementation depth.

Treat a spec as non-trivial when it changes public behavior, crosses more than one file, adds or changes fixtures, changes pipeline boundaries, affects failure/state/lifecycle behavior, needs phase handoff, or will be implemented by a fresh agent. For a trivial single-slice spec, still inspect the target file and adjacent tests, then use a compact shape.

## Architecture Analysis Output

Produce a concise spec shape analysis before drafting. Use this form or the repo's stronger convention:

```md
## Spec Shape

Task type:
Repo landing points:
Existing conventions:
Stable spec root:
Stable docs:
Phase briefs:
Fixtures:
Progress records:
Current pointer:
Allowed edit strategy:
Frozen strategy:
Generality boundary:
Open spec gaps:
```

Keep this analysis short. Its job is to place the spec in the repo and assign unresolved details to a handling path.

Use the repo's established convention when it preserves fresh-agent entry, stable/dynamic separation, phase sliceability, and fixture acceptance. When the convention weakens those properties, adapt it minimally and state the adapted structure.

Every open spec gap must be assigned one handling path before drafting continues:

- `defer`: record a deferred decision with a current phase default and decision point
- `default`: write the binding default into the relevant contract or phase brief
- `block`: stop the spec or phase until the user resolves the gap

Each open gap receives a handling path. Use repo evidence for defaults; use `defer` or `block` when repo evidence is insufficient.

## Repo Landing Points

Identify the implementation surface before writing contracts:

- source files or packages likely to change
- tests and fixtures that define behavior
- public API or command surface
- upstream and downstream pipeline stages
- existing naming, error, lifecycle, and dependency patterns
- current spec or planning directories

If the repo evidence conflicts with the user's requested shape, state the conflict and choose the smallest compatible layout.

## Generality Classification

Classify implementation depth from repo evidence:

- `repo-local`: serves this repo's workflow and stated fixtures
- `limited-domain`: supports a defined input domain or DSL with bounded syntax and callers
- `general-purpose`: intentionally supports broad external use, extensibility, or unknown callers

Default to `repo-local` or `limited-domain`. Use `general-purpose` when the user or existing public API requires broad external behavior.

When a broader mechanism may be useful later, record the extension trigger and keep the current phase at its selected depth.

## Task Type

### Refactor

Refactor specs must define exact edit boundaries:

- files allowed to modify
- files allowed to create
- frozen files and public behavior
- migration or compatibility requirements
- verification commands proving unchanged behavior

### Incremental Feature

Incremental feature specs must define where new behavior attaches:

- owning module or component
- public surface change
- upstream input guarantees
- downstream output expectations
- fixture additions
- phase boundary between integration and cleanup

### New Development

New development specs define concrete anchors:

- planned file paths
- planned type/function/module names
- public interface shape
- fixture file paths
- verification commands
- first usable phase and later integration phases

These anchors turn broad intent into executable phase boundaries.

## Slice Planning

A phase is a valid slice when it has:

- a narrow goal
- allowed create/modify paths
- frozen paths
- local component contract
- input guarantees
- fixture or table acceptance
- verification command
- clear downstream handoff condition

A slice that depends on future contracts should be reorganized around the owning component or phase boundary.

A slice has excess implementation detail when private helper bodies, exact control flow, or mechanical edits are already prescribed while remaining contract-neutral.

A slice has excess generality when its mechanism serves inputs, callers, scale, or extensibility beyond the stated generality boundary.
