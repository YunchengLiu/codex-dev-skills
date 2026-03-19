---
name: modern-cmake
description: Adopt modern CMake in a pragmatic cross-project way. Use when Codex needs to initialize a new CMake-based project, choose or review modern CMake structure, evaluate migration from legacy CMake patterns, decide whether a newer CMake feature is appropriate, or reason about target-based design, presets, dependency management, testing, installation, packaging, and portability tradeoffs. Do not use this as the default skill for routine configure or build invocation help, cache cleanup, missing-package diagnosis, generator-specific break-fix, or ordinary compile or link failures unless structural build-system decisions are part of the request.
---

# Modern CMake

## Overview

Use this skill to make pragmatic modern CMake decisions across projects. Favor target-based structure, clear build intent, and version-aware recommendations, then adopt newer CMake features when they provide a concrete benefit and fit the project's current requirements.

## Workflow

### 1. Establish the project profile first

- Check whether the task is a new project, a small practice project, an internal tool, or a long-lived library or application.
- Confirm present-day needs before designing the build: tests, presets, installation, export, package config, IDE support, cross-platform support, cross-compiling, or external consumers.
- Do not add install or package complexity for a practice or local-only project unless the user needs it now.
- Keep the structure clear enough that install or export support can be added later without a redesign.
- When restructuring an existing project, align target names, directory organization, and helper-module style with the established project unless the user asked for a broader refactor.

Read [references/project-profile.md](references/project-profile.md) when the project shape or build requirements are unclear.

### 2. Establish version and generator constraints

- Respect an explicitly requested minimum CMake version.
- Otherwise inspect the project declaration, presets, toolchain files, generators, and platform requirements before recommending newer features.
- Prefer recommendations that are comfortably supported by the effective CMake baseline instead of sitting on the version edge.
- If a feature depends on a newer CMake release, generator behavior, cross-compiling semantics, preset schema details, install or export behavior, or policy changes, verify against official documentation before presenting it as ready.

Read [references/project-profile.md](references/project-profile.md) when version, generator, or platform constraints need clarification.

### 3. Prefer high-value, low-churn modernization

- Prefer target-based configuration over directory-scoped or global-state configuration.
- Prefer clear usage requirements, explicit dependencies, and helper modules that match real responsibility boundaries.
- Keep target and helper-module granularity proportional to the real dependency graph. More targets is not automatically better.
- Prefer presets when the project has recurring workflows that benefit from a stable user-facing entry point.
- Use newer features such as `FILE_SET` when there is a real public or generated-header boundary and the effective version supports it.

Read [references/adoption-principles.md](references/adoption-principles.md) for default decision rules.

### 4. Keep initialization simple and demand-driven

- For new projects, guide the user toward the simplest modern structure that satisfies current needs.
- Think through directory responsibilities before reaching for a standard template. Do not force a fixed `include/` layout or package-oriented tree unless the project actually needs it.
- Do not front-load warning matrices, platform-specific flag tuning, or packaging scaffolding unless the task calls for them.
- For MSVC projects without special requirements, consider UTF-8 compatibility settings as a low-cost default.
- Leave natural extension points instead of speculative infrastructure.

Read [references/migration-patterns.md](references/migration-patterns.md) for how to keep new and existing projects easy to evolve.

### 5. Treat install and package boundaries as explicit decisions

- If the project must be installed, exported, or consumed by other projects, design those boundaries intentionally.
- If the project does not need install or export today, do not add the full package structure preemptively.
- Keep public headers, generated headers, and exported targets organized so later install support is straightforward.

Read [references/package-and-install.md](references/package-and-install.md) when install, export, or package config is part of the task.

### 6. Check high-risk areas before recommending them

- Be careful with global compile flags, cache-variable-driven control flow, `file(GLOB...)`, heavy generator expressions, `FetchContent` sprawl, and cross-compiling logic.
- Be careful with policy changes. Do not set or recommend policy behavior casually without understanding its version floor and effect.
- Prefer consistency in file layout, helper module structure, and dependency wiring across the project.
- Fail early on invalid or contradictory build options instead of letting the build drift into undefined behavior.

Read [references/high-risk-areas.md](references/high-risk-areas.md) before recommending higher-risk CMake patterns.

## Response Expectations

When recommending or applying a CMake change:

- State the relevant project profile and current needs.
- Explain why the suggested structure or feature is worth adopting now.
- Identify the main version, generator, portability, packaging, or maintenance risks.
- Say whether the recommendation should be applied now, deferred, or left as a future extension point.
- If support or semantics are uncertain, check the official CMake documentation before presenting the recommendation as ready, and state the version floor you relied on when it matters.
