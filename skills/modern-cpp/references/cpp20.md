# C++20 Guidance

Use C++20 facilities to express borrowed data, generic operations, sequence
work, and thread lifetime directly.

The examples below are representative, not exhaustive. The usable feature set is determined by the effective standard, compiler, standard library, project constraints, and local build evidence.

## Language features

- Concepts for constraining templates when the result is clearer diagnostics and intent
- Three-way comparison when the type has a natural total or partial ordering
- Designated initializers when aggregate construction becomes easier to read
- `consteval` and immediate functions only when compile-time enforcement is the actual goal
- Coroutines only when the project explicitly wants them and has a mature runtime story

## Library features

- `std::span` for non-owning contiguous views
- Range algorithms for whole-range operations, projections for member-based
  lookup or ordering, and short view pipelines for lazy selection or
  transformation
- `std::jthread` and `std::stop_token` for cancellation-aware thread management
- `std::source_location` for diagnostics and tracing hooks
- `std::format` when available and preferred over ad-hoc formatting
- `std::bit_cast` when representation-preserving conversion is intended
- Calendar, timezone, and chrono formatting facilities when the project already deals with time-heavy logic
- `std::erase` and `std::erase_if` for straightforward container cleanup
- `std::ssize` when signed sizes improve correctness
- [`std::cmp_*` and `std::in_range`](https://eel.is/c++draft/utility.intcmp)
  for mixed-sign integer comparisons and representability checks before integer
  conversion
- [`std::midpoint`](https://eel.is/c++draft/numeric.ops.midpoint) for an
  overflow-free midpoint and [`std::lerp`](https://eel.is/c++draft/c.math.lerp)
  for interpolation with defined endpoint and monotonicity guarantees;
  preserve the required rounding and numeric semantics

## Good default candidates

- Replace pointer/count interfaces with `std::span` when storage is owned by
  the caller and borrowing fits the contract.
- Constrain generic operations with concepts that match the expressions used;
  use range algorithms and projections to remove repeated iterator or
  comparator mechanics.
- Use `std::erase_if` for container filtering and `std::source_location` for
  caller-site diagnostic information that previously required macros.
- Prefer `std::jthread` for an owned, joinable worker whose lifetime should end
  with its scope; use `std::stop_token` when its work supports cooperative stop.

## Needs extra verification

- Treat `std::format`, chrono formatting or timezone pieces, and heavier ranges facilities as implementation-sensitive even in nominal C++20 projects.
- Keep modules and coroutines opt-in unless the project explicitly wants them and the toolchain story is mature enough.
- Keep view lifetimes and lazy evaluation clear. Check downstream diagnostics
  when constraints are part of a supported template interface.
- For algorithms returning iterators into temporary ranges, respect
  [`borrowed_range` and `dangling`](https://eel.is/c++draft/range.dangling).
  Borrowed-range status does not extend the lifetime of underlying storage.

## When uncertain

For implementation-sensitive choices, check feature-test macros, vendor
support notes, and the active toolchain. The
[standard sorting algorithms](https://eel.is/c++draft/sort) show range and
projection forms.
