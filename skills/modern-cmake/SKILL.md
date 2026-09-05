---
name: modern-cmake
description: >
  Choose and apply modern CMake facilities for target-based builds, usage
  requirements, source and header ownership, presets, dependencies, testing,
  and packages. Use when implementing, reviewing, initializing, or modernizing
  CMake code and build structure.
---

# Modern CMake

Use modern CMake to make the build's targets, dependencies, and usage
requirements explicit. Actively adopt facilities that simplify the current
build and its recurring workflows within the project's supported CMake
version, generators, and platforms.

## Working Defaults

Use first-principles reasoning: derive the build structure from current targets,
their requirements, consumers, and supported workflows. At each design,
implementation, and validation stage, use ablation to compare added targets,
helpers, settings, and checks with their removal or the simplest complete
alternative. Retain what serves a current requirement or distinct evidence,
preserving concrete project rules. When a material tradeoff needs measurement,
hold other conditions fixed and compare the same acceptance signal.

- Establish the declared CMake floor, generator, platform, dependency model,
  and current build or consumer needs from project evidence. Match existing
  target naming and directory responsibilities.
- Prefer target APIs and imported dependency targets. Set `PRIVATE`, `PUBLIC`,
  and `INTERFACE` according to who needs each requirement.
- Apply compiler options to the project-owned targets that require them, not
  through global flags or transitive leakage. Project-owned C++ targets using an
  MSVC-compatible command-line frontend use target-scoped `/utf-8` by default.
- For regular project `.cpp` source discovery, use a constrained
  `file(GLOB[_RECURSE] ... CONFIGURE_DEPENDS)` by default when the target owns
  the entire searched subtree. Do not let it cross into an independently owned
  child target, and `unset()` every temporary source list after registration.
  Use explicit entries when exact membership is a deliberate target constraint,
  for exceptional or generated files, or when a stronger project rule requires them.
- Inherit the project's dependency acquisition model unless the task revisits
  it. Add targets, helpers, presets, install rules, or package machinery for
  present needs; keep their size proportional to the actual build graph.
- Verify version-sensitive facilities, policies, presets, generator behavior,
  and install/export semantics against official CMake documentation. Respect
  the requested floor and state when a recommendation would raise it.
- Fail early on invalid or contradictory build options. Keep existing user,
  CI, and consumer entry points coherent when changing build structure.

## Choose Facilities for the Task

Read only the references relevant to the current build work.

- **Target configuration and dependencies:** use `target_compile_features`,
  `target_include_directories`, `target_link_libraries`, and imported targets
  to express requirements once at their owner. Use an `INTERFACE` library for
  a header-only component or a shared set of genuine usage requirements.
  Read [adoption-principles.md](references/adoption-principles.md).
- **Repeated configure, build, and test commands:** use presets to name and
  share real workflows. Keep machine-specific choices in user presets.
  Read [migration-patterns.md](references/migration-patterns.md) for applying
  these facilities in new and existing projects.
- **Sources, generated files, and configuration differences:** use owned source
  discovery, declared custom-command outputs, and focused generator
  expressions so build dependencies and per-configuration behavior stay
  explicit. Read [high-risk-areas.md](references/high-risk-areas.md).
- **Headers and external consumption:** use `FILE_SET HEADERS` when header
  membership should be shared by target, IDE, and install rules. Use exported
  targets and package configuration when downstream projects need
  `find_package`. Read [package-and-install.md](references/package-and-install.md).
- **Testing:** integrate tests with CTest when testing is part of the current
  project; keep test targets and dependencies with their owning component.
- **Project initialization or version/generator decisions:** choose the
  smallest target graph that serves the current product. Read
  [project-profile.md](references/project-profile.md).

## Reporting

State the relevant project profile and current needs. Explain the facility's
practical benefit, relevant CMake floor or generator constraints, and validation
performed. Identify the main version, generator, portability, packaging, or
maintenance risks. For a change affecting installation or consumption, include
evidence from that path. Recommend one approach and keep broader build
reorganization separate from the requested work.
State whether to apply the recommendation now, defer it, or leave it as a
future extension point.
