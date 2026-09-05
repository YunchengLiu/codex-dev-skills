---
name: modern-cpp
description: >
  Choose and apply modern C++ language and standard-library facilities for
  clearer interfaces, ownership, lifetime, generic code, and everyday
  implementation. Use for C++ implementation, review, focused modernization,
  or target-standard decisions where these choices affect the result.
---

# Modern C++

Use modern C++ to express the current problem directly. Actively select
supported language and library facilities when they improve correctness,
ownership, interfaces, or implementation clarity. Apply the same judgment to
new code and focused improvements in existing code.

## Working Defaults

Use first-principles reasoning: derive language and library choices from the
required behavior, ownership, consumers, and actual toolchain support. At each
design, implementation, and validation stage, use ablation to compare the chosen
form with its removal or the simplest complete alternative. Retain what adds
correctness, clarity, or useful evidence while preserving contracts and concrete
project rules. When a material tradeoff needs measurement, hold other conditions
fixed and compare the same acceptance signal.

- Establish the effective standard from the user's instruction, project
  declaration, build settings, and compiler/library evidence, in that order.
  Ask when material evidence remains missing or conflicting. C++26 is opt-in.
- Respect project runtime constraints and settled behavior. Verify
  implementation-sensitive facilities with feature-test macros, vendor
  documentation, or a focused compile probe; a language-mode flag alone does
  not prove library support.
- If runtime constraints, including hosted/freestanding operation, exceptions,
  RTTI, allocation, threading, debugging,
  sanitizers, public headers, or ABI remain unclear and affect the choice, ask
  before proposing library-heavy or boundary-crossing modernization.
- Prefer value semantics and RAII for ownership, views for clearly bounded
  borrowing, standard algorithms for sequence operations, and types that
  express meaningful states and results.
- Use the clearest supported form in touched code. Keep control flow,
  allocation, lifetime, and diagnostic costs understandable; keep state and
  behavior together when they share ownership and invariants.
- Match existing local style and keep changes focused. Preserve actual API,
  ABI, and consumer commitments at the boundaries that carry them; internal
  code and its callers can evolve together. Separate behavior changes from
  modernization unless the task includes them.
- Describe interfaces for callers: purpose, inputs, results, and relevant
  ownership, lifetime, and failure semantics.

## Choose Facilities for the Task

Use these as starting points, then select from the effective standard's
facilities. Read only the references relevant to the task.

- **Ownership and interfaces:** use RAII, standard ownership types,
  `std::string_view`, and `std::span` to make storage and borrowing clear;
  use `std::optional`, `std::variant`, or `std::expected` for the state or
  result model they actually express. Read
  [adoption-principles.md](references/adoption-principles.md).
- **Everyday implementation:** use scoped initialization, structured bindings,
  named algorithms, ranges, and standard container operations to replace
  distracting mechanics. Apply the modern-expression, lifetime, efficiency,
  and readability lenses in
  [code-modernization.md](references/code-modernization.md).
- **Generic code and callbacks:** use templates, concepts, `if constexpr`, and
  standard invocation facilities to express the required operations. Read
  [style-principles.md](references/style-principles.md) for ownership,
  abstraction, and callback defaults.
- **Changing an existing representation:** update the relevant callers and
  verify behavior through
  [migration-patterns.md](references/migration-patterns.md).
- **Choosing a baseline or working under runtime constraints:** read
  [standard-selection.md](references/standard-selection.md) and
  [project-profile.md](references/project-profile.md) as needed.

The version references explain facilities introduced by each standard and
when to use them. Earlier facilities remain candidates at a newer baseline.

- [C++17](references/cpp17.md): scoped state, vocabulary types, and simpler
  compile-time branching.
- [C++20](references/cpp20.md): views, constrained templates, ranges,
  diagnostics, and thread lifetime.
- [C++23](references/cpp23.md): value-or-error results, enum conversion,
  move-only callbacks, and local library improvements.
- [C++26](references/cpp26.md): feature-specific candidates when the user
  explicitly targets C++26 or asks about a named C++26 facility.

## Reporting

Briefly state the effective standard and how it was determined, the practical
benefit, and the evidence
that the selected form fits. Report relevant lifetime, support, diagnostic,
or cost tradeoffs and validation performed. Recommend one approach when
several are viable; separate broader follow-up work from the requested change.
State whether to apply the change now, defer it, or record it as a future
migration.
