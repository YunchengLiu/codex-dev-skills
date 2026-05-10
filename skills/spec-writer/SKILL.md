---
name: spec-writer
description: Write and refine implementation specs for settled design goals so they become clear, unambiguous, and implementable. Use when the direction is already known and the remaining work is to define module boundaries, interfaces, behavior, errors, lifecycle, and acceptance criteria.
---

# Spec Writer

## Purpose
Turn settled design goals into a spec that an implementation agent can read and code directly.

## Use
Use this skill when the task is to draft or refine spec text for an already chosen direction. Use it to tighten boundaries, make behavior explicit, and check whether the spec still leaves implementation space open.

## Working rules
- Treat confirmed decisions as fixed unless the user explicitly reopens them.
- Describe behavior in positive form: what each component does, when it succeeds, and how failures are expressed.
- Make scope, public surface, inputs, outputs, state changes, errors, lifecycle, constraints, and acceptance criteria explicit whenever they affect implementation.
- Tie rationale to the task’s concrete constraints, not to generic best practice.
- If a needed implementation detail is missing, call it out instead of inventing intent.
- When writing exposes a gap, capture the gap and continue from that same constraint set.
- Read `references/spec-principles.md` for the full framework and the detailed writing principles.

## Self-check
Read the draft like an implementer and verify:
1. Do overview, detail, sketch, and plan files tell the same story?
2. Does every public capability have enough definition to implement and test it?
3. Would any wording reasonably lead an implementer toward a different mechanism?

For a self-check-only request on an existing draft, surface only issues that can cause implementation error. If there is no substantive blocker, output exactly `未发现实质问题`.
