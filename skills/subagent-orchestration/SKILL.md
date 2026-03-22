---
name: subagent-orchestration
description: Guide selective subagent orchestration when delegation or independent checking is genuinely on the table. Use when Codex needs to decide whether subagents are justified, shape neutral delegation prompts, request independent parallel checks for critical decisions, evaluate weak or low-confidence subagent output, retry with better context or stronger capability, and synthesize multiple subagent results without over-delegating. Prefer this skill for code, algorithms, logic-heavy analysis, technical design, and research planning only when the work would materially benefit from delegation or independent review. Do not use it as the default for routine tasks, for clarification-only planning, for defining custom agents, or for building a full multi-agent runtime.
---

# Subagent Orchestration

## Overview

Use this skill as a selective orchestration policy for subagents. It is a decision layer for when the main agent should delegate, when it should stay single-agent, how to request independent checks without leading the result, and how to synthesize advisory outputs without outsourcing judgment.

This skill is general-purpose, but default examples and heuristics should stay grounded in code, algorithms, logic-heavy analysis, technical design, and research planning or execution-briefing. Use the same rules for other intellectual work only when the task similarly benefits from delegation, independent checks, parallel analysis, or careful synthesis.

Do not treat this skill as a runtime controller. It does not require custom agents, fixed model identities, or special infrastructure. If subagents or capability controls are unavailable, keep the same decomposition and checking discipline, but do not present same-context self-checks as independent validation.

## Workflow

### 1. Start with a delegation decision, not a delegation habit

- Default to a single-agent pass for ordinary tasks.
- Consider subagents only when they can add independent information, coverage, or verification that the main agent would not get as efficiently alone.
- Prefer this skill when the task involves high-impact reasoning, high-risk changes, conflicting hypotheses, or a meaningful need for independent confirmation.
- Do not use subagents just because the task is long. Use them when the work can be separated cleanly enough to benefit from parallel or independent analysis.
- If the task mainly needs clarification or plan shaping before any delegation choice exists, use `planning-clarification` first instead of invoking this skill as a generic planning layer.

Read [references/task-selection.md](references/task-selection.md) when deciding whether delegation is justified.

### 2. Classify the task shape before delegating

- First classify the task as mainly execution, exploration, review, design critique, verification, or synthesis.
- For clear execution work with explicit acceptance criteria, delegation is often unnecessary unless a targeted check can reduce risk.
- For review, design critique, debugging hypotheses, command-risk assessment, or research planning with meaningful challenge value, an independent check is more likely to pay off.
- Treat code and other intellectual work consistently: the question is whether independent analysis helps, not whether the task fits a narrow domain label.

Read [references/task-selection.md](references/task-selection.md) when the task shape or risk level is unclear.

### 3. Use the lightest useful subagent pattern

- Use one subagent when a single independent check or bounded side task is enough.
- Use two independent subagents only when the task is important enough to justify comparison or conflict detection, for example high-risk review, design tradeoff analysis, or ambiguous root-cause reasoning.
- Do not keep spawning agents by default. More agents add coordination cost, repeated blind spots, and synthesis burden.
- Reuse an existing agent only when its current context helps more than it contaminates. Prefer a fresh agent for independent review, design critique, or any task where prior conclusions may bias the result.

Read [references/task-selection.md](references/task-selection.md) when choosing between no subagent, one checker, or two independent perspectives.

### 4. Shape delegation prompts so subagents do not have to guess

- State the task goal, task type, scope, non-goals, relevant context, operating boundaries, and expected output clearly.
- Keep prompts neutral. Do not smuggle the preferred answer into a review or critique request unless the task explicitly requires evaluating a proposed answer.
- Give enough local context to let the subagent succeed, but avoid unnecessary conversation history or peer conclusions that would contaminate independence.
- When asking for review or critique, prefer concrete artifacts, code paths, diffs, designs, requirements, hypotheses, or commands over abstract summaries.
- When the task benefits from standardized comparison, define a minimal response structure so outputs can be synthesized cleanly.

Read [references/dispatch-patterns.md](references/dispatch-patterns.md) when drafting a delegation prompt or output contract.

### 5. Match effort to the task, then verify the result

- For explicit execution tasks with clear success criteria, a medium-effort subagent is often enough even if the work is non-trivial.
- For review, design critique, risk judgment, or conflict resolution, prefer stronger capability and deeper reasoning when the environment supports it.
- Treat model and effort guidance as recommendations, not hard assumptions. This skill must still work when those controls are unavailable.
- Never assume a stronger subagent makes synthesis unnecessary. The main agent must still inspect whether the subagent understood the assignment and used the context correctly.

Read [references/evaluation-and-synthesis.md](references/evaluation-and-synthesis.md) when deciding whether to retry with better context or stronger capability.

### 6. Wait long enough to get the value you asked for

- Do not cut off a critical subagent run just because the main agent has moved on mentally.
- If the main answer depends on an independent check, wait for it unless a clear timeout, failure, or scope change justifies stopping.
- If the subagent is taking too long, first decide whether the problem is scope, prompt shape, or unjustified delegation before replacing the task with a weaker one.
- If a subagent result is no longer needed because the task changed materially, say so explicitly rather than silently discarding the work.
- If no real subagent path exists, do not simulate independence. Describe any self-check as same-agent verification rather than an independent pass.

Use these waiting rules before simplifying, cancelling, or replacing an in-flight subagent request.

### 7. Treat subagent outputs as advisory and quality-gate them

- Do not accept subagent output at face value.
- Check whether it answered the actual question, respected scope, used the supplied context, and provided evidence or reasoning proportional to the task.
- Be skeptical of outputs that are generic, repetitive, shallow, contradictory, overconfident, or obviously anchored by the wording of the prompt.
- Agreement between multiple subagents is useful but not decisive. Shared blind spots remain possible.
- If the output quality is poor, decide whether the failure came from missing context, poor task framing, insufficient independence, or insufficient capability.

Read [references/evaluation-and-synthesis.md](references/evaluation-and-synthesis.md) when evaluating weak or low-confidence subagent output.

### 8. Retry or escalate deliberately

- First tighten the task statement or supply the missing local context when the failure looks like misunderstanding or ambiguity.
- Prefer a fresh subagent for retries when independence matters or the prior context is likely to bias the second pass.
- Escalate capability or reasoning depth when the task is genuinely judgment-heavy and the earlier pass failed despite adequate task framing.
- Do not chain retries indefinitely. If repeated subagent attempts are not clarifying the situation, inspect directly or reduce the problem locally.

Read [references/evaluation-and-synthesis.md](references/evaluation-and-synthesis.md) when choosing between retry, fresh pass, stronger capability, or stopping.

### 9. Synthesize results instead of averaging them

- The main agent remains responsible for the final judgment.
- Compare outputs on evidence, scope coverage, assumptions, and remaining uncertainty rather than simply counting votes.
- When outputs conflict, identify whether the disagreement is factual, interpretive, or caused by different scopes or assumptions.
- Preserve uncertainty when the conflict is real. If needed, run one more focused verification step instead of pretending the conflict has been resolved.
- Summaries should distinguish confirmed points, plausible but unverified claims, and unresolved disagreements.

Read [references/evaluation-and-synthesis.md](references/evaluation-and-synthesis.md) when combining multiple outputs into one answer.

### 10. Stay within the skill's responsibility

- This skill is about delegation judgment, prompt shaping, quality gates, and synthesis discipline.
- It is not the place to define custom agents, hard runtime control, deep domain standards, long-lived agent memory, or complex orchestration frameworks.
- If the task becomes primarily domain-specific, apply the appropriate domain skill alongside this one rather than inflating this skill into a domain manual.

## Response Expectations

When using this skill:

- State whether delegation is justified and why.
- State which subagent pattern is appropriate: none, one bounded check, or two independent perspectives.
- Keep delegation prompts neutral, concrete, and tightly scoped.
- Prefer code-centric or artifact-centric context over long conversational backstory.
- Use `planning-clarification` first when the task mainly needs clarification or planning rather than delegation judgment.
- Say when independent review should use a fresh context rather than reusing an existing thread.
- Treat subagent outputs as advisory and explain how they were quality-checked.
- Retry only when there is a clear reason to believe a better prompt, better context, or stronger capability will help.
- Make the main agent's synthesis explicit, including uncertainty and unresolved conflict when they remain.
- Degrade gracefully if subagents or capability controls are unavailable by applying the same decomposition and checking discipline directly, while stating clearly that same-context self-checks are not independent review.
