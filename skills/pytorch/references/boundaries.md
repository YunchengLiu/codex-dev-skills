# Boundaries

## What this skill is for

- PyTorch runtime and compatibility questions
- Model and module organization
- Dataset and DataLoader structure
- Train, eval, inference, precision, and state-handling decisions
- Performance and compile decisions
- Single-machine multi-GPU decisions (including basic single-node DDP)

## What this skill is not for

- General experiment-stage workflow planning
- General Python project structure
- Framework-agnostic ML architecture debates
- Domain-specific scientific validity judgments
- Multi-node distributed training, cluster orchestration, or elastic/fault-tolerant launches
- Sharding strategies such as FSDP/ZeRO/DeepSpeed-level design

## When to hand off

- The main problem is experiment organization rather than PyTorch mechanics.
- The project is not mainly PyTorch anymore.
- The issue is scientific-method or domain correctness rather than framework behavior.
- The task is mainly multi-node distributed training or cluster-level concerns.
