# codex-skills

My personal Codex skills for day-to-day development tasks.

These skills are intended to stay cross-project and reusable. They are built and iterated with Codex, with help from the `skill-creator` skill when scaffolding and refining new skills.

## Scope

This repository is for general development targets, for example:

- C++/Python/etc: modern language features and best practices
- CMake/etc: build system best practices
- Some best-practice for engineering guidance

## Existing Skills
- `planning-clarification`: A multi-turn planning loop for turning vague or partially specified requests into clear, execution-ready briefs. It should summarize current understanding, ask only high-value questions, research authoritative sources when external facts matter, make uncertainty explicit, and keep the final plan tightly scoped instead of overdesigned.
- `subagent-orchestration`: A selective orchestration policy for using subagents well. It should help the main agent decide when delegation is justified, when independent parallel checks are worth the cost, how to shape neutral delegation prompts, how to detect weak subagent output, when to retry or escalate, and how to synthesize advisory results without over-delegating, while still degrading honestly when no custom agents or subagent controls are available.
- `personal-markdown-note-writer`: A personal knowledge note writer for turning rough discussions, drafts, excerpts, and command snippets into long-lived Chinese Markdown notes. It should default to synthesis mode when a prior discussion exists (write agreed conclusions first), avoid chat meta, prefer writing to a user-provided output path, and use web scan to widen the view (terminology/examples/pitfalls) without silently changing conclusions (pause and confirm if a material correction is found). It is not intended for handoff specs, process docs, or repo-level document rewrites.
- `plan-progress-tracker`: Create and maintain a durable on-disk workpack for multi-agent handoff: INDEX/OVERVIEW plus per-module specs, and PLAN/STATUS/DECISIONS tracking. It should keep overview and module boundaries consistent across changes, avoid noisy exclusion-list writing, and keep a stable entrypoint for fresh chats and agents.
- `modern-cpp`: A practical reminder layer for modern C++ work. It should nudge Codex toward better-fit language or library features when they are worth it, but still stay grounded in project constraints, toolchain reality, and stable interface boundaries.
- `modern-cmake`: A practical reminder layer for modern CMake work. It should keep new and existing build systems target-based and demand-driven, without turning simple projects into overdesigned package scaffolding.
- `ai4science`: A stage-aware workflow decision layer for Python-based AI experiments. It should keep training and evaluation work reproducible, portable, and easy to iterate on, while preferring mature framework or open-source infrastructure and avoiding premature experiment-platform design.
- `pytorch`: A PyTorch-specific decision layer for model code, runtime behavior, state handling, and performance. It should keep modules, dataloaders, train loops, precision, and checkpoint logic native and readable before reaching for heavier machinery.

## Repo Layout

```text
skills/
  <skill-name>/
    SKILL.md
    agents/
    references/
    scripts/
    assets/
```

Each skill keeps its own instructions and any related resources inside its own folder.

## How To Use

1. Clone this repository on the machine where you use Codex.
2. Copy or sync the skill folders you want into `$CODEX_HOME/skills`.
3. Use the skills by name in prompts when needed. Some skills may also be eligible for implicit selection when their descriptions match the task, while more policy-oriented skills may intentionally require explicit `$skill-name` invocation.

Current example:

```text
skills/modern-cpp/
```

That folder can be synced into:

```text
$CODEX_HOME/skills/modern-cpp/
```
