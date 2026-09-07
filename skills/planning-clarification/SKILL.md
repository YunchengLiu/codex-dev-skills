---
name: planning-clarification
description: >
  Clarify unsettled requests, probe assumptions and design choices, and converge
  on evidence-backed execution briefs or fresh-context prompts. Use when goals,
  constraints, or material decisions need working through before execution.
---

# Planning Clarification

Turn an unsettled request into the smallest complete plan that another person
or agent can execute. Work from the desired result and available evidence,
actively test assumptions, and resolve the decisions that determine the route.
Express the settled requirements and reasoning directly, in clear, idiomatic
language suited to the reader. Keep interview history out of the result.

Use the depth the task needs. A clear local request may need only a short brief;
a difficult design may need several rounds of investigation and questioning.
Preserve the user's choices, project instructions, and authorization already
given when shaping the next work.

## Ground The Problem

Identify the target project from the request. Read the supplied material and
the smallest relevant set of local artifacts before asking questions they can
answer. Inspect incrementally: current behavior, callers, tests, manifests,
notes, or data only where they inform this task. Handle ordinary lookup and
triage directly.

Reason from first principles within the given frame:

- Establish the requested outcome, who needs it, and the observable signal that
  would show success. Separate this need from a suggested implementation unless
  the user has already chosen that implementation.
- Identify the stated domain, scale, constraints, and commitments. Distinguish
  confirmed facts, evidence-based inferences, working assumptions, and unknowns;
  do not invent requirements to fill gaps.
- For development or refactoring, locate the owning execution path and its
  integration boundary. Establish what the current path provides, where its
  guarantees are established, who consumes them, and what is actually missing
  before decomposing implementation work. If an owner or behavior is unknown,
  locating or deciding it is the next step.

A settled design is an input. Reopen a settled point only when concrete evidence
shows a conflict with the requested behavior or current project, and keep the
challenge confined to that conflict.

## Investigate The Design Route

If a missing requirement determines which approaches are relevant, resolve that
decision before researching branches it may rule out.

For non-local, non-obvious, or algorithmically difficult work, deliberately try
a credible alternative representation, decomposition, or execution route. A
state machine, ownership model, dataflow representation, geometric operation,
or table of rules may simplify the problem; these are examples, not a menu to
work through.

For development, use an alternative only when it matches the required semantics
and reduces total implementation, testing, and maintenance complexity compared
with the direct design. If it does not fit, state the mismatch and return to
the simplest direct approach.

For each material representation, abstraction, or algorithm choice, classify
the domain and actively study relevant mature implementations and primary
sources before settling the route. Inspect the concrete algorithm as well as
the surrounding design. For example, compiler work may benefit from LLVM's
implementation and tests; runtime work from CPython or Lua; geometry from CGAL.
Extract the invariant, ownership rule, algorithmic idea, or tradeoff and explain
why it fits, needs adaptation, or fails to fit this task's semantics and scale.
Prefer an established approach that directly covers the requirement over a
parallel local model. Do not import an architecture because it is prominent or
turn an obvious local change into a research exercise.

Also verify external facts when the plan depends on current capabilities,
version-sensitive behavior, standards, regulations, or precise sourced claims.
Prefer official documentation, project code and tests, standards, and primary
papers. Distinguish source findings from your synthesis. If sources conflict,
are unavailable, or browsing is forbidden, state the affected uncertainty and
what could resolve it instead of presenting an unverified answer as settled.

## Probe The Decisions

When clarification is still needed, briefly summarize the current understanding
before asking questions so the user can correct the frame.

Actively identify assumptions whose failure
would change the outcome, scope, acceptance, ownership, dependencies, or another
costly decision. Test them against the evidence and a concrete case: what
requires this constraint, what happens at the relevant boundary, or whether the
proposed mechanism solves the stated problem. Raise practical contradictions
directly; avoid hypothetical future requirements and exhaustive risk surveys.

Follow decision dependencies. Settle an upstream choice before asking about
details that depend on it, then trace the answer into the affected parts of the
plan. Ask one coherent decision at a time, or a few independent questions that
can be answered together. Continue through consequential branches until the
shared model is clear.

For each question, explain briefly why the answer changes the plan and give a
reasoned recommendation when the evidence supports one. Compare only credible
options with materially different consequences; say when the available facts
do not support a preference. Present an informed tradeoff for the user to
choose; handle investigation and local mechanical choices yourself.

For example, "move exports into the background" may leave unclear whether an
export must survive application exit. Inspect the existing export path first.
If that guarantee is still undecided and changes ownership or persistence,
settle it before asking about job storage or retry policy. Recommend an answer
from the actual workflow and explain its consequence; do not assume durability
merely because the request uses the word "background".

After an answer, update the working plan, revisit only dependent decisions, and
inspect any new evidence it calls for. Carry settled facts and relevant process
choices forward. When the user mainly wants a result, concentrate on missing inputs,
acceptance, and boundaries that affect delivery.

## Remove Unnecessary Structure

As material choices arise, after a design change, and before finalizing, compare
the proposal with the existing path and the simplest complete alternative.
Carry forward supported decisions; revisit only what new facts or an unresolved
concern could change. Keep routine comparisons brief. For each added phase,
abstraction, fallback, dependency, document, or validation step, ask what current
requirement, invariant, execution ambiguity, or distinct acceptance evidence
would be lost if it were removed. Use the smaller form when it provides the
same result; remove additions with no such justification.

Check that simplification preserves the complete requested behavior and real
integration points. Keep guarantees, supported inputs, hardening, and execution
authority within the agreed scope. Retain the explanation, examples, and model
an executor needs to understand and carry out the plan.

## Converge On The Brief

Stop questioning when the material decisions are settled and remaining details
do not change the agreed route. Produce a compact brief in top-down order:
outcome and scope; recommended approach and decisive evidence; affected work
and its dependencies; deliverable and acceptance. Carry the owning path,
established guarantees, and remaining responsibilities needed to guide local
implementation into that brief. Include assumptions, limits,
or unresolved choices only where they still matter. Do not emit empty sections
or a transcript of rejected proposals.

For a material design choice, include any relevant alternative considered, the mature
implementations or primary sources consulted, and the extracted idea with why
it is reused, adapted, limited, or rejected. Omit this design evidence only when
no material design choice remains.

If a critical choice remains unresolved after inspection and research, ask the
user and identify what depends on the answer. A provisional brief may describe
independent work and explicit assumptions, but must not disguise a blocked
decision as an executable instruction.

When shaping a human brief, an agent execution brief, or a prompt for a fresh
session, use [output-modes.md](references/output-modes.md). Preserve settled
requirements while leaving unverified project details for the executor to
confirm. Match the requested medium and amount of detail.
