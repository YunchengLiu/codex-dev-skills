---
name: pytorch
description: Guide modern, reliable PyTorch implementation and runtime decisions for single-machine workloads (CPU, single-GPU, and single-machine multi-GPU, including single-node DDP basics when needed). Use when Codex needs to structure PyTorch modules, datasets and dataloaders, train/eval/inference loops, devices and dtypes, AMP, state_dict checkpoints and resume behavior, torch.compile, or performance tuning with clear, native, maintainable patterns. Prefer this skill for single-machine PyTorch mechanics and implementation choices.
---

# PyTorch

## Overview

Use this skill when the main questions are PyTorch-specific for single-machine workloads: runtime compatibility, model or module structure, tensor and device behavior, train/eval/inference mechanics, checkpointing, or performance. Prefer modern, reliable, official or mature patterns that keep the main code path readable. It also covers common single-machine multi-GPU patterns (including basic DDP via `torchrun --nproc_per_node`) when needed.

## Workflow

### 1. Establish the active runtime stack first

- Confirm the active Python version, PyTorch version, accelerator stack, driver situation, and target device context before recommending code or dependency changes.
- Inspect the existing environment and dependency files before recommending installs or upgrades.
- If runtime compatibility is unclear, inspect first. Prefer explicit environment evidence over memory.
- For PyTorch environment debugging, prefer collecting concrete runtime information before guessing.
- Do not silently create environments, install packages, or upgrade framework components. Get user approval first.

Read [references/environment-and-runtime.md](references/environment-and-runtime.md) when runtime, compatibility, or installation questions matter.

### 2. Classify the PyTorch task

- Decide whether the main issue is model or module structure, data loading, train/eval/inference loops, checkpoint and resume behavior, performance tuning, or single-machine multi-GPU (including basic single-node DDP).
- Keep the recommendation proportional to the task. Do not drag in AMP, compile, multi-GPU, or trainer abstractions unless the current task actually needs them.
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
- Prefer concentrating "global" run configuration (device, dtype, seeds, paths, key hyperparameters) in one small place (a simple global constant, dict, or dataclass is fine) rather than scattering it across files.
- Parameterize only what varies in the current work and provide defaults. If a value is intentionally fixed for this project, hard-code it with a short comment explaining why.
- Keep metrics/logging/checkpoint side effects out of `forward()`. Do them in the train/eval loop where control flow is visible.

Read [references/data-and-dataloader.md](references/data-and-dataloader.md) and [references/training-and-precision.md](references/training-and-precision.md) when loop design is in scope.

### 5. Treat state handling as a first-class concern

- Prefer standard `state_dict`-based save and load flows unless there is a strong reason to do otherwise.
- Keep checkpoint contents and resume behavior explicit enough to understand what is being restored.
- Avoid fragile checkpoint assumptions tied to one machine, one device, or one ad hoc module layout when cleaner PyTorch-native patterns are available.
- Tighten checkpoint and resume rules when the project starts to rely on them, but do not overbuild them for trivial prototype code.

Read [references/module-and-state.md](references/module-and-state.md) when save, load, resume, or module-state questions matter.

### 6. Use performance features deliberately

- Treat AMP, `torch.compile`, pinned memory, persistent workers, loader tuning, and multi-GPU features as opt-in tools, not default ceremony.
- Confirm that the current runtime stack and task justify them before recommending them.
- Prefer correctness and clarity first, then add performance features when there is a concrete payoff.
- When compile or performance behavior is uncertain, verify against official PyTorch documentation before presenting it as ready.

Read [references/performance-and-compile.md](references/performance-and-compile.md) when performance or compilation is the main topic.

### 7. Stay within the skill's responsibility

- This skill is for PyTorch mechanics, runtime behavior, and implementation decisions.
- It is not the primary skill for general experiment-stage planning or domain-specific scientific reasoning.
- If the main issue becomes experiment workflow design, research-method validity, or another framework, say so instead of forcing a PyTorch-shaped answer.
- If the main issue is experiment workflow (stage-appropriate structure, metrics/logging/artifacts policy, integrity guardrails), prefer an experiment-workflow skill.
- If the main issue is general project shape or dependency ownership rather than PyTorch semantics, say so instead of stretching this skill.
- If more specific guidance is available, combine it when helpful. If not, state the limit clearly rather than assuming another skill exists.

Read [references/boundaries.md](references/boundaries.md) when the scope is drifting.

## Response Expectations

When recommending or applying a PyTorch change:

- State the relevant runtime stack and PyTorch assumptions.
- Explain why the suggested PyTorch feature, pattern, or level of machinery is appropriate now.
- Identify the main compatibility, readability, state-management, or performance risks.
- Flag any environment or dependency changes that need user approval.
- Say when the task is no longer mainly a PyTorch decision.
- Prefer clear, incremental changes unless the user explicitly asks for a larger rework.
