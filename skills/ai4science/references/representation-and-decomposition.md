# Representation and Decomposition

## Core Rule

Model the shared structure of the problem first, then express ordinary cases and
edge cases through the same meaningful dimensions when the semantics stay clear.
Split a workflow along real responsibility boundaries, and keep the orchestration
layer thin.

## Representation Method

Use this sequence before adding fields, schemas, or feature tables:

1. Name the entities that actually appear in the current problem.
2. Name the relations, measurements, or latent factors that explain the user's
   question.
3. Choose the smallest representation that can express ordinary cases and edge
   cases with the same concepts.
4. Treat low-information flags as modeling pressure: look for a relation,
   measurement, ordering, grouping, or boundary semantics that explains the case
   more generally.
5. Mark values as derived when they can be computed cheaply from existing data.
6. Promote a derived value into stored state when repeated use, cost,
   auditability, or downstream API shape makes storage clearer.
7. Keep fixture-specific quirks inside tests or fixture metadata unless they
   express a stable domain concept.

A core field or dimension must pass these checks:

- it has stable meaning beyond one sample or fixture;
- it represents a property, relation, measurement, or factor that helps explain
  the current problem;
- it is clearer as stored state than as a derived value at the use site.

Valuable dimensions can be numerous when they carry real meaning. The failure
mode to catch is not "too many fields" by count; it is fields that encode sample
quirks, duplicate other dimensions, or record labels without explanatory value.

## Common Structure Before Flags

Prefer one relation model with defined boundary semantics over low-information
flags. A flag such as `is_single`, `is_first`, or `has_special_case` usually
means the representation has not yet captured the underlying relation.

Example pattern:

- For adjacent-line spacing, model each line with left-neighbor and
  right-neighbor spacing when those are the meaningful relations.
- Represent a missing neighbor with the repo-appropriate boundary value
  (`None`, `null`, `boundary`, `inf`, or another explicit local convention).
- Add a flag such as `is_single_line` only after checking that no clearer
  relation, boundary value, grouping, or derived predicate represents the same
  idea. When a flag remains, state the domain concept it represents.

This example is a pattern, not a fixed schema. Choose the boundary value from
the current code, math, serialization format, and tests.

## Decomposition Method

Use a stage boundary when a step has its own input/output contract, test value,
or replacement path. Common AI/AI4Science pipelines often separate:

- IO and dataset discovery;
- deterministic preprocessing or feature extraction;
- model inference, classification, or scoring;
- evaluation, reporting, and artifact writing.

Use a thin runner to connect these stages. Keep a single file when the workflow
is short, exploratory, and still readable with local functions.

## Discussion Trigger

Before coding, pause for a compact design note when the user has described the
task only as "extract features", "classify", "analyze influence", or similar
phrasing and the representation is not obvious from the repo.

Use:

```text
Observed entities:
Natural relations:
Downstream decision/report:
Minimal representation:
Derived fields:
Recommended smallest design:
Open question:
```
