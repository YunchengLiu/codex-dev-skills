---
name: modern-cpp
description: Adopt modern C++ in a pragmatic cross-project way. Use when Codex needs to analyze, review, refactor, or design C++ code with C++17, C++20, C++23, or C++26 considerations; choose whether a language or standard-library feature is appropriate; plan or execute incremental migrations; or explain tradeoffs around compatibility, readability, diagnostics, ABI, performance, and maintainability.
---

# Modern C++

## Overview

Use this skill to make pragmatic modern C++ decisions across projects. Favor clear, compatible, maintainable code, then adopt newer language and library features when they provide a concrete benefit and fit the effective standard and toolchain.

## Workflow

### 1. Establish the effective standard first

- Respect an explicitly requested standard.
- Otherwise inspect the project declaration, build configuration, compiler flags, and toolchain hints.
- If the effective standard is still unclear, the evidence conflicts, or compiler/library support cannot be inferred reliably, ask the user which standard to target before recommending or applying version-specific changes.
- Treat C++26 as opt-in. Confirm that compiler and standard-library support are sufficient before relying on it.

Read [references/standard-selection.md](references/standard-selection.md) when the target standard or toolchain needs clarification.

### 2. Prefer high-value, low-churn adoption

- Prefer changes that improve correctness, ownership clarity, resource safety, interface clarity, and maintainability.
- Prefer local migrations over broad rewrites.
- Use newer features when they simplify the code or make contracts clearer, not just because they are newer.
- Stay conservative around public APIs, ABI-sensitive boundaries, hot paths, compile-time-heavy code, and code that must remain easy to debug.

Read [references/adoption-principles.md](references/adoption-principles.md) for the default decision rules.

### 3. Keep the engineering style simple

- Prefer value semantics when ownership is local and cheap enough.
- Make ownership and lifetime explicit.
- Prefer standard-library types and facilities over custom helpers when they express the intent well.
- Use templates, concepts, ranges, constexpr, and metaprogramming with restraint. Keep diagnostics and call sites understandable.
- Preserve readable control flow. Avoid abstraction that hides cost or semantics.

Read [references/style-principles.md](references/style-principles.md) for the semantic style defaults.

### 4. Make migrations incremental

- Start with contained upgrades that have a clear payoff.
- Keep behavior stable unless the user requested a contract change.
- When a larger migration would be better, say so explicitly and separate the immediate patch from the follow-up direction.

Read [references/migration-patterns.md](references/migration-patterns.md) for common migration shapes.

### 5. Pull in version-specific guidance only when needed

- Read [references/cpp17.md](references/cpp17.md) for C++17 decisions.
- Read [references/cpp20.md](references/cpp20.md) for C++20 decisions.
- Read [references/cpp23.md](references/cpp23.md) for C++23 decisions.
- Read [references/cpp26.md](references/cpp26.md) for C++26 decisions.

Do not load every version file by default. Read only the files needed for the user's target standard and migration scope.

## Response Expectations

When recommending or applying a change:

- State the target standard and how it was determined.
- Explain why the change is worth making.
- Identify the main compatibility, ABI, diagnostic, performance, or maintenance risks.
- Say whether the change should be applied now, deferred, or recorded as a future migration.
- Prefer minimal diffs unless the user explicitly asks for a redesign.

When multiple valid approaches exist, present the tradeoffs briefly and recommend one.
