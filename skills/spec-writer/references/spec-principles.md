# Spec Writing and Self-check Principles

This file guides project-level spec writing, revision, and self-checking in the spec directory. It defines the dimensions a usable spec should cover and how to judge them. The structure should follow the task, not the other way around.

## Table of Contents

- [Purpose](#purpose)
- [Core Dimensions](#core-dimensions)
- [Common Structures](#common-structures)
- [Component-Level Content](#component-level-content)
- [Expression Rules](#expression-rules)
- [Design Intent vs Implementation Contract](#design-intent-vs-implementation-contract)
- [Self-check Lens](#self-check-lens)
- [Implementation Phasing](#implementation-phasing)
- [Freeze Criteria](#freeze-criteria)

## Purpose

A spec’s final output is a clear design and implementation brief. Once a decision is written into the spec, treat it as settled unless the task explicitly reopens it. Specs may include goals, preferences, and tradeoffs to explain why a choice was made and where the boundary lies.

## Core Dimensions

A spec should let an implementation agent understand, implement, and verify the work consistently. For each component, scan these eight dimensions and decide how deeply each one needs to be specified for this task. If a dimension is handled lightly or deferred, record that choice and where it is handled instead.

1. Goal and applicable scenario: why this exists and what real scenario it serves.
2. Scope and boundaries: what the current task covers and what remains outside it.
3. Chosen approach: explicit choices about objects, interfaces, modules, flows, or migration strategy.
4. Behavior contract: inputs, outputs, state changes, failure modes, visibility, lifecycle.
5. Errors and diagnostics: error categories, return shapes, exception shapes, diagnostic context.
6. Performance and engineering constraints: hot paths, resource cost, dependencies, build, compatibility.
7. Implementation cadence: independently verifiable steps, phase boundaries, allowed local refactors and helper tools.
8. Acceptance criteria: tests, checks, validation commands, benchmarks, or migration checks.

These dimensions may live in one file or several files. The format should serve the task.

## Common Structures

Complex modules or cross-component work often fit a top-down structure:

1. An overview file fixes goals, scope, core scenarios, design tradeoffs, responsibilities, and implementation cadence.
2. Component files fix a single object, component, or backend’s responsibilities, interfaces, behavior, errors, and boundaries.
3. An implementation plan breaks settled decisions into independently verifiable phases.
4. An API sketch provides a baseline public shape; the behavior contract in the body takes precedence over sketch details.
5. An implementation principles file keeps the development process narrow and prevents unnecessary cross-phase changes.

The overview explains the "why" and the high-level partitioning. Concrete interfaces, methods, error codes, path algorithms, lifecycle rules, and performance boundaries belong in the owning component file.

## Component-Level Content

A component section can cover these items as needed:

1. Role: what problem the object or component solves.
2. Component overview: responsibilities, design goals, core contract, ownership boundaries, performance focus, acceptance focus.
3. Object model or composition: stable concepts, fields, states, or handles.
4. Capability list: public methods, inputs and outputs, successful behavior.
5. Behavior contract: key algorithms, state changes, visibility, lifecycle, ordering, coverage, commit rules.
6. Errors and diagnostics: failure modes, error codes, exception or expected shapes, diagnostic sources.
7. Performance boundaries: what high-frequency paths should avoid and what low-frequency boundaries may optimize for clarity.
8. Relationships to other components: keep the necessary linkage, point to the owning file, and avoid repeating long contract text.

Any decision that affects implementation must have a clear owner. Headings and order should follow the task.

## Expression Rules

Prefer positive behavior descriptions:

- Write what an interface does, when it succeeds, and how failure is expressed.
- Write what an object owns, where its lifecycle is rooted, and which fields matter for decisions.
- Write what a phase accepts and which tests demonstrate the behavior.

When a competing direction needs to be ruled out, describe the chosen behavior precisely so the other direction no longer fits. Keep explicit exclusions short and attached to the positive statement that makes them unnecessary. When the meaning is already clear, let contract clarity take priority over stylistic variation.

## Design Intent vs Implementation Contract

Design intent explains tradeoffs. Anchor rationale to the task’s concrete constraints instead of generic industry practice. The implementation contract must be specific enough for an implementation agent to code and test directly:

- public objects and methods
- input normalization
- visible success behavior
- failure categories and error codes
- lifecycle and dangling boundaries
- concurrency, performance, cache, or materialization boundaries
- phase acceptance and test points

Only capabilities already in the spec count as current development requirements.

## Self-check Lens

Before finishing a draft, read it like an implementer and verify:

1. Do overview, detail, sketch, and phase plan tell the same story?
2. Does every public capability have enough definition to implement and test it?
3. Would any wording reasonably lead an implementer toward a different mechanism?

If the answer is yes to all three, the spec is ready.

## Implementation Phasing

Each phase should be independently buildable, testable, and verifiable. Helper tools and local refactors belong in a phase only when they serve that phase’s goal.

## Freeze Criteria

When the spec has clear goals and scope, clear responsibilities and public capabilities, consistent behavior, errors, lifecycle, and phase boundaries, and the remaining comments are wording preferences or optional extensions, move to implementation or an independent gate check. After that point, keep changes limited to issues that affect correctness.
