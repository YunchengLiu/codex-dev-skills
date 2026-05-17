---
name: modern-cpp
description: Adopt modern C++ in a pragmatic cross-project way. Use when the task involves modern C++ code design, code-level modernization, language or standard-library feature selection, modernization tradeoffs, target-standard decisions, or incremental migration work. For routine bugfixing, debugging, or build-only tasks, use this skill when modernization decisions are part of the request.
---

# Modern C++

## Overview

Use this skill to make pragmatic modern C++ decisions across projects. Favor clear, compatible, maintainable code, then adopt newer language and library features when they provide a concrete benefit and fit the effective standard and toolchain. Modernization includes local clarity and safety improvements as well as version-specific feature selection.

## Authority

Treat this skill as the primary guide for landing modern C++ code. Project constraints, the effective standard, behavior stability, ownership clarity, and lifetime clarity are hard requirements for implementation decisions. Existing local style guides how those requirements are expressed in the codebase.

The patterns and lenses named here are required review inputs and representative examples. Also apply context-specific C++ judgment from the surrounding code, domain model, performance profile, public API expectations, and observable behavior.

## Workflow

### 1. Establish the project profile first

- Check whether the code is hosted or freestanding and whether there are hard constraints around exceptions, RTTI, allocation, threading, debugging, sanitizers, public headers, or ABI stability.
- Treat these project constraints as stronger than general modernization advice.
- If these constraints are unclear and they affect the recommendation, ask before proposing library-heavy or boundary-crossing modernization.

Read [references/project-profile.md](references/project-profile.md) when project constraints shape the modernization decision.
Read [references/standard-selection.md](references/standard-selection.md) when the target standard needs clarification.

### 2. Establish the effective standard

- Respect an explicitly requested standard.
- Otherwise inspect the project declaration, build configuration, compiler flags, and toolchain hints.
- If the effective standard is still unclear, the evidence conflicts, or compiler/library support cannot be inferred reliably, ask the user which standard to target before recommending or applying version-specific changes.
- Treat C++26 as opt-in. Confirm that compiler and standard-library support are sufficient before relying on it.

Read [references/standard-selection.md](references/standard-selection.md) when the target standard or toolchain needs clarification.

### 3. Prefer high-value, low-churn adoption

- Prefer changes that improve correctness, ownership clarity, resource safety, interface clarity, and maintainability.
- Prefer local migrations over broad rewrites.
- Use newer features when they simplify the code or make contracts clearer.
- Stay conservative around public APIs, ABI-sensitive boundaries, hot paths, compile-time-heavy code, and code that must remain easy to debug.

Read [references/adoption-principles.md](references/adoption-principles.md) for the default decision rules.

### 4. Keep the engineering style simple

- Prefer value semantics when ownership is local and cheap enough.
- Make ownership and lifetime explicit.
- Prefer standard-library types and facilities over custom helpers when they express the intent well.
- Use advanced language and library facilities with restraint. Keep diagnostics and call sites understandable.
- Preserve readable control flow. Keep cost and semantics visible in any abstraction.

Read [references/style-principles.md](references/style-principles.md) for the semantic style defaults.

### 5. Run a code modernization pass when relevant

- Look for focused improvements in the active code that clarify intent, ownership, lifetime, contracts, or cost.
- Review code through four lenses: modern expression, correctness and lifetime, local efficiency, and readability.
- Apply the effective standard and local code context to choose the clearest modern C++ expression.

Read [references/code-modernization.md](references/code-modernization.md) for the code modernization pass and its code-quality lenses.

### 6. Make migrations incremental

- Start with contained upgrades that have a clear payoff.
- Keep behavior stable. Apply contract changes when the user requests them.
- When a larger migration would be better, say so explicitly and separate the immediate patch from the follow-up direction.

Read [references/migration-patterns.md](references/migration-patterns.md) for common migration shapes.

### 7. Pull in version-specific guidance only when needed

- Read [references/cpp17.md](references/cpp17.md) for C++17 decisions.
- Read [references/cpp20.md](references/cpp20.md) for C++20 decisions.
- Read [references/cpp23.md](references/cpp23.md) for C++23 decisions.
- Read [references/cpp26.md](references/cpp26.md) only when the user explicitly targets C++26 or asks about a specific C++26 feature.

Read only the version files needed for the user's target standard and migration scope.

## Response Expectations

When recommending or applying a change:

- State the target standard and how it was determined.
- Explain why the change is worth making.
- Identify the main compatibility, ABI, diagnostic, performance, or maintenance risks.
- Say whether the change should be applied now, deferred, or recorded as a future migration.
- Prefer minimal diffs. Expand the design scope when the user explicitly asks for a redesign.

When multiple valid approaches exist, present the tradeoffs briefly and recommend one.
