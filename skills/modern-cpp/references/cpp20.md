# C++20 Guidance

Use C++20 to improve interfaces, contracts, and concurrency, but keep the adoption selective.

## Commonly valuable features

- `std::span` for non-owning contiguous views
- Concepts for constraining public templates when the result is clearer diagnostics and intent
- Ranges for local, readable transformations over standard iterator-heavy code
- Three-way comparison when the type has a natural total or partial ordering
- `std::jthread` and `std::stop_token` for cancellation-aware thread management
- `std::source_location` for diagnostics and tracing hooks
- `std::format` when available and preferred over ad-hoc formatting

## Default posture

- Use concepts to simplify template contracts, not to build a type-system showcase.
- Use ranges when the pipeline stays readable at the call site and under a debugger.
- Keep modules and coroutines opt-in unless the project explicitly wants them and the toolchain story is mature enough.

## Migration note

C++20 is a strong target for teams that want better contracts and standard concurrency primitives without jumping straight to the newest language mode.
