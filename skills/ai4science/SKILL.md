---
name: ai4science
description: Guide Python-based AI and AI4Science experiment workflows in a stage-aware way. Use when Codex needs to decide how much structure, reproducibility, portability, logging, checkpointing, artifact management, or framework reuse an experiment workflow needs. Do not use this as the primary skill for generic framework usage, deep framework internals, or scientific-validity judgments unless they directly affect experiment workflow decisions.
---

# AI4Science

## Overview

Use this skill as a stage-aware experiment workflow decision layer for Python-based AI and AI4Science work. Favor the lightest structure that fits the current experiment phase, keep the code and data flow clear enough to evolve cleanly, and only add more process when the current stage actually needs it.

If a separate general Python skill is available, align with its basic environment and code-clarity rules. If not, this skill should still stand on its own.

## Workflow

### 1. Treat project stage as the primary input

- First infer whether the task is early setup, local debugging, an actively changing experiment, or a more mature comparison or repeatable run workflow.
- Match the amount of structure to the current stage. Do not front-load complexity for future phases the user is not in yet.
- Prefer code, configuration, and outputs that are clear enough to clean up and standardize later.
- Remember that AI experiments are rarely truly one-off. Even early work usually benefits from enough structure to rerun, compare, and recover.
- Prefer inferring the stage from the current request and recent workflow. Only ask the user when stage ambiguity would materially change the recommendation.

Read [references/stage-principles.md](references/stage-principles.md) when the current experiment phase is unclear.

### 2. Establish environment and compatibility first

- Confirm the active Python environment, target Python version, framework versions, accelerator stack, and execution context before recommending code or dependency changes.
- Check the existing dependency and environment files before recommending commands or workflow changes.
- Distinguish local-debug and server-run expectations early. Keep the project portable enough that moving between them does not require fragile manual edits.
- Do not silently create environments, install dependencies, or change dependency ownership. Get user approval first.
- If compatibility is unclear, inspect first and ask the user before assuming the environment is ready.

Read [references/environment-and-compatibility.md](references/environment-and-compatibility.md) when the runtime or dependency story matters.

### 3. Reuse mature framework infrastructure first

- When the user explicitly specifies a framework, follow that choice.
- Otherwise prefer the project's existing framework-native infrastructure. If the stack is still open and the task matches a typical modern deep-learning workflow, PyTorch can be the default first choice, together with other mature open-source infrastructure where appropriate.
- Only build custom NN plumbing when existing infrastructure cannot meet a concrete requirement.
- For common patterns such as training loops, evaluation flow, metric collection, checkpointing helpers, and utility layers, actively look for strong open-source precedents before inventing a local pattern.
- Recommend useful external tooling or libraries when they solve a real problem, but let the user decide whether to adopt them.

Read [references/ecosystem-and-reuse.md](references/ecosystem-and-reuse.md) when deciding whether to reuse or build locally.

### 4. Keep experiment structure clear without overbuilding it

- Separate the major concerns enough to stay understandable: data handling, configuration, model definition, training, evaluation, inference, logging, and artifacts.
- Keep the main execution path easy to read, especially after logging, metrics, and checkpoint code start to accumulate.
- Do not assume every experiment needs a heavy configuration system, serialization layer, CLI surface, or trainer abstraction on day one.
- Simple centralized configuration can be acceptable in early phases if it is low-frequency, mostly read-only, and easy to evolve later.
- Prefer the simplest structure that still makes the experiment runnable, debuggable, and portable.

Read [references/structure-principles.md](references/structure-principles.md) when balancing clarity against engineering overhead.

### 5. Make reproducibility and portability practical

- Keep inputs, outputs, run parameters, seeds, and important assumptions visible enough to rerun the experiment.
- Grow reproducibility requirements with the stage. Early work may only need the essentials, while mature comparison workflows should also capture dataset identity, split or preprocessing assumptions, code version, and important runtime context.
- Make local and server execution paths consistent where possible. Avoid hard-coded machine-specific paths, devices, or shell assumptions.
- Define input and output arguments clearly enough that scripts can move between local debugging and server execution without ad hoc patching.
- Treat logging, metrics, checkpoints, and artifacts as support for reruns and comparison, but scale their structure with the current stage.

Read [references/reproducibility-and-artifacts.md](references/reproducibility-and-artifacts.md) when the task involves reruns, saved state, or experiment outputs.

### 6. Keep artifacts and checkpoints stage-appropriate

- In early setup and debugging, checkpoints and artifacts are often mainly for backup, recovery, and quick inspection. A simple directory with clearly named files is often enough.
- Do not force stable schemas, complex directory hierarchies, or rigid compatibility rules before the experiment needs them.
- As experiments mature into repeated comparisons or more stable workflows, tighten naming, saved metadata, and resume behavior gradually.
- Only push for stable, compatibility-conscious checkpoint or artifact rules once the user is clearly in a mature comparison or long-running workflow.

Read [references/reproducibility-and-artifacts.md](references/reproducibility-and-artifacts.md) when deciding how much output structure is justified.

### 7. Stay within the skill's responsibility

- This skill is about experiment workflow, engineering scale, compatibility, and reuse in Python-based AI work.
- It can suggest domain or science concerns cautiously, but do not treat scientific assumptions, physical meaning, or research validity as settled without user confirmation.
- If the main issue becomes deep framework internals, domain-specific scientific reasoning, or another specialized area, say so and recommend more specific guidance instead of bluffing through it.

Read [references/boundaries.md](references/boundaries.md) when the task starts to drift beyond experiment workflow decisions.

## Response Expectations

When recommending or applying a change:

- State the current experiment stage and why it matters.
- State the relevant environment, framework, and portability assumptions.
- Explain why the suggested amount of structure is appropriate now.
- Identify the main compatibility, reproducibility, readability, or maintenance risks.
- Flag any dependency or environment changes that need user approval.
- Say when the task has moved beyond this skill's core responsibility.
- Prefer clear, incremental changes unless the user explicitly asks for a broader reorganization.
