---
name: modern-cpp
description: Adopt modern C++ in a pragmatic cross-project way. Use when Codex needs to choose whether a C++17, C++20, C++23, or C++26 language or standard-library feature is appropriate, review modernization tradeoffs, or plan and execute incremental migration work. Do not use this as the default skill for routine bugfixing, debugging, or build-only tasks unless modernization decisions are part of the request.
---

# Modern C++

## Overview

Use this skill to make pragmatic modern C++ decisions across projects. Favor clear, compatible, maintainable code, then adopt newer language and library features when they provide a concrete benefit and fit the effective standard and toolchain.

## Workflow

### 1. Establish the project profile first

- Check whether the code is hosted or freestanding and whether there are hard constraints around exceptions, RTTI, allocation, threading, debugging, sanitizers, public headers, or ABI stability.
- Treat these project constraints as stronger than general modernization advice.
- If these constraints are unclear and they affect the recommendation, ask before proposing library-heavy or boundary-crossing modernization.

Read [references/standard-selection.md](references/standard-selection.md) when the target standard or project profile needs clarification.

### 2. Establish the effective standard

- Respect an explicitly requested standard.
- Otherwise inspect the project declaration, build configuration, compiler flags, and toolchain hints.
- If the effective standard is still unclear, the evidence conflicts, or compiler/library support cannot be inferred reliably, ask the user which standard to target before recommending or applying version-specific changes.
- Treat C++26 as opt-in. Confirm that compiler and standard-library support are sufficient before relying on it.

Read [references/standard-selection.md](references/standard-selection.md) when the target standard or toolchain needs clarification.

### 3. Prefer high-value, low-churn adoption

- Prefer changes that improve correctness, ownership clarity, resource safety, interface clarity, and maintainability.
- Prefer local migrations over broad rewrites.
- Use newer features when they simplify the code or make contracts clearer, not just because they are newer.
- Stay conservative around public APIs, ABI-sensitive boundaries, hot paths, compile-time-heavy code, and code that must remain easy to debug.

Read [references/adoption-principles.md](references/adoption-principles.md) for the default decision rules.

### 4. Keep the engineering style simple

- Prefer value semantics when ownership is local and cheap enough.
- Make ownership and lifetime explicit.
- Prefer standard-library types and facilities over custom helpers when they express the intent well.
- Use templates, concepts, ranges, constexpr, and metaprogramming with restraint. Keep diagnostics and call sites understandable.
- Preserve readable control flow. Avoid abstraction that hides cost or semantics.

Read [references/style-principles.md](references/style-principles.md) for the semantic style defaults.

### 5. Make migrations incremental

- Start with contained upgrades that have a clear payoff.
- Keep behavior stable unless the user requested a contract change.
- When a larger migration would be better, say so explicitly and separate the immediate patch from the follow-up direction.

Read [references/migration-patterns.md](references/migration-patterns.md) for common migration shapes.

### 6. Pull in version-specific guidance only when needed

- Read [references/cpp17.md](references/cpp17.md) for C++17 decisions.
- Read [references/cpp20.md](references/cpp20.md) for C++20 decisions.
- Read [references/cpp23.md](references/cpp23.md) for C++23 decisions.
- Read [references/cpp26.md](references/cpp26.md) only when the user explicitly targets C++26 or asks about a specific C++26 feature.

Do not load every version file by default. Read only the files needed for the user's target standard and migration scope.

## Response Expectations

When recommending or applying a change:

- State the target standard and how it was determined.
- Explain why the change is worth making.
- Identify the main compatibility, ABI, diagnostic, performance, or maintenance risks.
- Say whether the change should be applied now, deferred, or recorded as a future migration.
- Prefer minimal diffs unless the user explicitly asks for a redesign.

When multiple valid approaches exist, present the tradeoffs briefly and recommend one.
