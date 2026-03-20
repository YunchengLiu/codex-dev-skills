---
name: planning-clarification
description: Clarify vague, messy, or partially specified requests into precise, right-sized execution plans for concrete tasks through a multi-turn planning loop. Use when Codex needs to summarize its current understanding, ask a few high-value questions, research authoritative sources when external facts matter, tighten scope and non-goals, avoid overdesign, and produce an execution brief for either a human or another LLM across engineering work, lightweight automation, local artifact handling, structured organization, analysis, and other agent-completable tasks.
---

# Planning Clarification

## Overview

Use this skill to turn an imprecise request into a plan that is clear enough to execute and no broader than necessary. Treat this as a planning loop rather than a one-shot rewrite: summarize the current understanding, identify the few uncertainties that actually matter, research when outside facts affect the plan, and converge on a brief that is actionable without overdesigning the work.

Apply it to concrete, outcome-oriented tasks broadly. That includes rigorous engineering work, but also lightweight automation, local artifact handling, structured organization, analysis, and other tasks that an agent may be expected to carry through while the user mainly cares about the result.

Keep the bar for added complexity high. Do not upgrade a small or local task into architecture work, process design, or defensive future-proofing unless the user explicitly wants that.

## Workflow

### 1. Inspect available local context when it is relevant

- If the user has provided files, a repository, notes, manifests, or another clearly relevant local context, inspect that material before asking avoidable questions or browsing.
- Do not assume the current working directory or active workspace is automatically the real context for the task. Planning conversations may start before the relevant project, files, or execution directory are available.
- Decide whether local inspection is useful from the user's request and the apparent relevance of the current context. If the task is obviously independent of the current filesystem state, do not inspect it just because a workspace exists.
- Prefer evidence from the current request and genuinely relevant local artifacts over generic assumptions.
- Do not inspect aimlessly. Look only for information that would reduce unnecessary questions or materially sharpen the plan.
- Inspect incrementally. Start with the smallest useful check, and only expand if the result shows that deeper inspection is justified. Do not recursively read a whole repository by default.
- If relevant local context is missing, inaccessible, or simply not part of the current request, continue with clarification instead of pretending it was checked.

Read [references/loop-pattern.md](references/loop-pattern.md) when deciding whether to keep inspecting, start clarifying, or move to planning.

### 2. Start with a clear current understanding

- First extract the apparent goal, likely scope, execution target, and expected outcome from the user's request.
- State a short `Current Understanding` summary before asking follow-up questions, unless the request is already precise enough to plan immediately.
- Separate what is explicit from what is inferred. Do not present assumptions as confirmed facts.
- If the request already appears clear, still check whether the remaining ambiguity would materially change the execution plan before deciding to skip questions.

Read [references/loop-pattern.md](references/loop-pattern.md) when deciding whether to keep clarifying or move to planning.

### 3. Classify the execution style before shaping the plan

- Infer the task shape before asking more questions: implementation-heavy work, lightweight automation, local artifact handling, structured organization, analysis, or another concrete execution task.
- Infer whether the user wants process transparency or mainly the final result.
- Do not force a visible taxonomy on the user when the request already makes the execution style clear.
- Ask at most one short clarification question when the process-oriented versus result-oriented distinction would materially change the plan or output style.
- When the user appears result-oriented, shape the plan around required inputs, checks, deliverables, and stop conditions rather than internal implementation detail.

Read [references/questioning-rules.md](references/questioning-rules.md) when deciding whether this distinction is clear enough to infer.

### 4. Ask only a few high-leverage questions

- Ask follow-up questions only when the answer would materially change the plan, scope, deliverable, or execution style.
- Prefer one to three concise questions that are easy to answer quickly.
- Do not turn clarification into a form, checklist dump, or background interview.
- Do not ask the user to restate information that is already obvious from the request.
- Prefer boundary-setting questions such as intended deliverable, non-goals, acceptable scope, execution owner, likely execution environment, or current constraints.
- If the user may care more about the final result than the implementation detail, confirm that only when the distinction would change the plan shape, level of explanation, or handoff format.
- If the task may depend on a repository, file set, or workspace that is not yet available, ask only enough to tell whether local inspection is needed now or can be deferred.
- If the output needs to be shaped differently for a human or another LLM, ask that early rather than after drafting the brief.
- Treat inspection strategy as the agent's responsibility. Do not repeatedly ask the user whether to inspect local files unless the user explicitly wants to control that behavior or the plan is blocked on missing context.

Read [references/questioning-rules.md](references/questioning-rules.md) when deciding what to ask and what to infer.

### 5. Research external facts when they affect the plan

- If the plan depends on external facts, current tool behavior, standards, regulations, APIs, product capabilities, version-sensitive guidance, or precise source-backed claims, research them unless the user explicitly forbids browsing.
- Prefer authoritative sources first: official documentation, standards bodies, project maintainers, primary papers, or other primary references.
- Do not browse for purely local organization tasks, local codebase inspection, or requests where external facts are not relevant.
- If the user forbids browsing, say so and plan within that constraint instead of pretending the facts are settled.

Read [references/research-and-uncertainty.md](references/research-and-uncertainty.md) when external evidence or source confidence matters.

### 6. Make uncertainty explicit instead of guessing

- After clarifying and researching, distinguish confirmed facts, working assumptions, and unresolved unknowns.
- If multi-source checking still leaves a relevant point uncertain, say that it remains uncertain and explain what is missing.
- Ask the user for the missing information when it is necessary to proceed confidently.
- Do not fill gaps with speculative requirements, architecture, risk posture, or maintenance assumptions.

Read [references/research-and-uncertainty.md](references/research-and-uncertainty.md) when deciding whether uncertainty is acceptable or must be surfaced.

### 7. Keep the plan right-sized

- Aim for the smallest honest plan that is sufficient to execute well.
- Prefer concrete scope, non-goals, and deliverables over elaborate process.
- Separate must-have constraints from optional hardening or future cleanup.
- If a heavier or more extensible approach exists, keep it as a brief follow-up option rather than the default plan unless the user asked for it.
- Actively check whether any part of the draft plan is one layer more complex than the request actually needs.

Read [references/right-sizing.md](references/right-sizing.md) when deciding how much structure or defensive planning is justified.

### 8. Produce an execution-ready brief

- Once the plan is clear enough, produce a concise brief shaped to the executor and the user's level of interest in implementation detail.
- For result-oriented requests, emphasize required inputs, acceptance criteria, execution boundaries, deliverables, and blocking conditions over internal design or implementation detail.
- If some uncertainty remains but no longer blocks execution, produce a provisional brief and label the remaining assumptions clearly.
- Do not keep asking questions once the unanswered points no longer change the practical plan.

Read [references/output-modes.md](references/output-modes.md) for brief structure and output choices.

### 9. Confirm who the plan is for if still unclear

- Ask whether the final plan is intended for the user to execute or for another LLM to execute only if that has not already been established.
- If it is for a human, keep the brief decision-oriented and easy to scan.
- If it is for another LLM, make the brief self-contained enough for a fresh thread with no prior context.
- If it is for another LLM and the user mainly wants results, keep implementation detail secondary to operating boundaries, deliverables, and stop conditions.
- When the user wants a prompt for another LLM, ask whether they want one if that was not already requested.

Read [references/output-modes.md](references/output-modes.md) when switching between human-facing and LLM-facing outputs.

### 10. Generate a fresh-context LLM prompt only when useful

- When asked for an LLM prompt, write it for a new model instance that knows nothing about the current conversation.
- Include the task goal, relevant context, scope, non-goals, constraints, expected output, and any required operating rules.
- State execution boundaries explicitly when they matter, especially for local-workspace execution and actions that require explicit approval.
- When paths, repositories, or working directories matter, state them explicitly. Do not assume the later execution context, current working directory, or current chat workspace is already known or will stay the same.
- Keep the prompt LLM-friendly and as concise as possible without assuming hidden context.
- Do not include schedule, chat history, or irrelevant reasoning unless it changes execution.

Read [references/output-modes.md](references/output-modes.md) when writing a prompt for another LLM.

### 11. Stay within the skill's responsibility

- This skill is for clarifying and planning work, including tasks that may later be executed end to end by another agent.
- Once the plan is stable enough, prefer handing off to a more specific skill, direct implementation work, or source-backed guidance instead of continuing to elaborate the planning layer.
- If the main issue becomes framework internals, domain science, detailed implementation, or repository-specific execution, say so and shift to the more appropriate skill or workflow.

## Response Expectations

When using this skill:

- Start with a concise current-understanding summary when clarification is still needed.
- Inspect relevant local context when it actually exists and matters to the plan.
- Keep local inspection minimal and demand-driven rather than recursively exploring by default.
- Infer whether the user wants process detail or mainly the final result, and ask only if that distinction would materially change the plan.
- Ask only the smallest set of questions that meaningfully sharpens the plan.
- Research authoritative sources when external facts affect the plan and the user has not forbidden browsing.
- Make uncertainty explicit and ask the user for missing information instead of guessing.
- Keep the result tightly scoped and actively avoid overdesign, overdefense, and speculative future-proofing.
- State whether the result is a provisional plan or a final brief.
- Confirm whether the output is for a human or another LLM, and offer a fresh-context prompt when the LLM path is chosen.
- For LLM-facing execution briefs, state the default execution boundary explicitly: work within the current workspace or clearly supplied local artifacts, but do not install global tools, modify the system environment, touch unrelated locations, or take high-risk external actions without explicit approval.
