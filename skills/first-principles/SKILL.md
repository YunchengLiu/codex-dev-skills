---
name: first-principles
description: >
  Reason from required outcomes, facts, and constraints, then test the need for
  each part through ablation. Use for analysis, planning, design, problem
  solving, and review. Apply a brief check to straightforward work and a deeper
  comparison to consequential decisions.
---

# First Principles

Start with what the result must accomplish. Derive the approach from current
facts and constraints; use established practice to inform that reasoning.

## When To Apply It

Use this method when framing a problem, choosing a design, explaining a failure,
or reviewing a proposed solution. Apply a brief check to straightforward work
and a deeper comparison where the decision has material consequences.

## Establish The Problem

1. State the required outcome and the observable evidence of success.
2. Identify the relevant facts, constraints, scope, and established invariants.
   Separate confirmed facts from assumptions that still need evidence.
3. Trace the current process: what it already provides, where the necessary
   information is available, who uses the result, and what remains missing.
4. Read each part in context: its enclosing scope, adjacent explanation, and
   relationship to the whole determine what it means.

## Derive And Compare

Start with the simplest approach that delivers the complete outcome. Assign
each responsibility where the information needed to fulfill it is available,
and let subsequent steps use the established result.

For a consequential choice, compare credible alternatives on the same
requirements. Consult relevant evidence and mature approaches; explain the
principle that makes an approach fit this problem. Resolve assumptions that
could change the choice with a focused question, inspection, or experiment.

Keep the detail needed for someone to understand the result and its reasons.
Completeness includes the connections, affected users, and evidence required
for the result to work.

## Ablation

After each design, implementation, execution, or validation stage, compare the
result with one that removes an addition or replaces it with a simpler alternative:

1. Which requirement, invariant, useful information, or distinct acceptance
   signal would be lost?
2. Could an existing step or smaller representation provide the same result?
3. Does the retained part solve the stated problem at the required scope?

Remove a part when the simpler version preserves the required result. Retain
rules, explanations, examples, and checks whose removal would weaken a
requirement or create a likely misunderstanding. Brevity follows clarity.

For mechanical rules, compare each changed line with the simpler version,
then check every retained line against the applicable checklist.

Use a controlled experiment when reasoning alone cannot distinguish the
alternatives: hold other relevant conditions fixed, change one factor, and
compare the same acceptance signal. Distinguish measured results from reasoned
expectations. Finish when the required result and sufficient evidence are
established.
