# C++17 Guidance

Treat C++17 as a solid modernization baseline for legacy code and conservative environments.

## Commonly valuable features

- Structured bindings for local unpacking with clear names
- `if` and `switch` initializers to keep temporary state scoped
- `std::optional` for value-or-no-value contracts
- `std::variant` when a closed set of alternatives is the real model
- `std::string_view` for non-owning read-only string parameters with clear lifetime
- `std::filesystem` when platform file work no longer needs custom wrappers
- `if constexpr` to simplify template branching

## Default posture

- Prefer C++17 upgrades that remove ambiguity and boilerplate.
- Avoid clever template tricks just because `if constexpr` makes them possible.
- Keep `std::variant` visitation readable. If it becomes a metaprogramming exercise, step back.

## Migration note

C++17 is often a good first stop for projects moving from older dialects because many upgrades are local and low-risk.
