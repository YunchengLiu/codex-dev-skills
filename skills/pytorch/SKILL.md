---
name: pytorch
description: Guide PyTorch-specific implementation and runtime decisions. Use when Codex needs to choose how to structure PyTorch modules, datasets and dataloaders, train or eval loops, devices and dtypes, AMP, checkpoint and state handling, torch.compile, performance, or distributed behavior. Do not use this as the primary skill for experiment-stage workflow planning, general Python project structure, or scientific-validity judgments unless PyTorch-specific constraints are the main issue.
---

# PyTorch

## Overview

Use this skill when the main questions are PyTorch-specific: runtime compatibility, model or module structure, tensor and device behavior, train and eval mechanics, checkpointing, performance, or distributed execution. Favor native PyTorch APIs and mature ecosystem patterns, keep the main path readable, and only add heavier PyTorch machinery when the current task truly needs it.

If other relevant skills are available, combine them when the task is broader than PyTorch mechanics. If not, this skill should still stand on its own for PyTorch-specific decisions.

## Workflow

### 1. Establish the active runtime stack first

- Confirm the active Python version, PyTorch version, accelerator stack, driver situation, and target device context before recommending code or dependency changes.
- Inspect the existing environment and dependency files before recommending installs or upgrades.
- If runtime compatibility is unclear, inspect first. Prefer explicit environment evidence over memory.
- For PyTorch environment debugging, prefer collecting concrete runtime information before guessing.
- Do not silently create environments, install packages, or upgrade framework components. Get user approval first.

Read [references/environment-and-runtime.md](references/environment-and-runtime.md) when runtime, compatibility, or installation questions matter.

### 2. Classify the PyTorch task

- Decide whether the main issue is model or module structure, data loading, train or eval loops, inference, checkpoint and resume behavior, performance tuning, or distributed execution.
- Keep the recommendation proportional to the task. Do not drag in AMP, compile, distributed, or trainer abstractions unless the current task actually needs them.
- If the problem is mostly experiment workflow rather than PyTorch mechanics, say so and hand off to more appropriate guidance.

Read [references/boundaries.md](references/boundaries.md) when the main issue is unclear.

### 3. Prefer native PyTorch and mature patterns first

- Prefer official PyTorch APIs and well-understood ecosystem patterns over hand-rolled tensor or autograd machinery.
- Reuse idiomatic `nn.Module`, `Dataset`, `DataLoader`, optimizer, scheduler, and `state_dict` patterns before inventing local alternatives.
- Prefer borrowing proven open-source patterns for common training and evaluation code over writing framework-like infrastructure from scratch.
- For common PyTorch patterns, prefer official PyTorch documentation, `pytorch/examples`, and other mature, reliable ecosystem implementations before expanding local conventions.
- Keep custom extensions justified by a concrete requirement, not by habit.

Read [references/module-and-state.md](references/module-and-state.md) when the structure of PyTorch code is the main issue.

### 4. Keep modules, data flow, and loops readable

- Make it easy to find model construction, forward behavior, loss computation, optimizer steps, evaluation, checkpoint handling, and device transfer logic.
- Keep tensor shapes, device movement, dtype changes, and autograd-sensitive operations visible enough to debug.
- Avoid clever wrappers or hidden mutation that make the training path hard to follow.
- When adding metrics, logging, AMP, or helper utilities, preserve the readability of the main train and eval path.

Read [references/data-and-dataloader.md](references/data-and-dataloader.md) and [references/training-and-precision.md](references/training-and-precision.md) when loop design is in scope.

### 5. Treat state handling as a first-class concern

- Prefer standard `state_dict`-based save and load flows unless there is a strong reason to do otherwise.
- Keep checkpoint contents and resume behavior explicit enough to understand what is being restored.
- Avoid fragile checkpoint assumptions tied to one machine, one device, or one ad hoc module layout when cleaner PyTorch-native patterns are available.
- Tighten checkpoint and resume rules when the project starts to rely on them, but do not overbuild them for trivial prototype code.

Read [references/module-and-state.md](references/module-and-state.md) when save, load, resume, or module-state questions matter.

### 6. Use performance features deliberately

- Treat AMP, `torch.compile`, pinned memory, persistent workers, compile-time graph tricks, and distributed features as opt-in tools, not default ceremony.
- Confirm that the current runtime stack and task justify them before recommending them.
- Prefer correctness and clarity first, then add performance features when there is a concrete payoff.
- When compile or performance behavior is uncertain, verify against official PyTorch documentation before presenting it as ready.

Read [references/performance-and-compile.md](references/performance-and-compile.md) when performance or compilation is the main topic.

### 7. Stay within the skill's responsibility

- This skill is for PyTorch mechanics, runtime behavior, and implementation decisions.
- It is not the primary skill for general experiment-stage planning, general Python project structure, or domain-specific scientific reasoning.
- If the main issue becomes experiment workflow design, research-method validity, or another framework, say so instead of forcing a PyTorch-shaped answer.
- If adjacent skills or more specific guidance are available, combine them. If not, state the limit clearly rather than assuming another skill exists.

Read [references/boundaries.md](references/boundaries.md) when the scope is drifting.

## Response Expectations

When recommending or applying a PyTorch change:

- State the relevant runtime stack and PyTorch assumptions.
- Explain why the suggested PyTorch feature, pattern, or level of machinery is appropriate now.
- Identify the main compatibility, readability, state-management, or performance risks.
- Flag any environment or dependency changes that need user approval.
- Say when the task is no longer mainly a PyTorch decision.
- Prefer clear, incremental changes unless the user explicitly asks for a larger rework.
