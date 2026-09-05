# Adoption Principles

Choose facilities that state the target graph and usage requirements directly
and make recurring build work easier to maintain.

## Default goals

- Prefer target-based configuration over directory-scoped or global configuration.
- Keep usage requirements explicit through target APIs.
- Keep project layout and helper modules consistent by responsibility.
- Fail early on invalid configuration combinations.
- Preserve portability and consumer compatibility where they matter.

## Good default candidates

- **Requirements owned by a target:** use `target_link_libraries`,
  `target_include_directories`, `target_compile_definitions`, and
  `target_compile_features`. `PRIVATE` serves the target, `INTERFACE` serves
  its consumers, and `PUBLIC` serves both. Set the minimum language feature
  level where it is required, including propagation when headers need it.
- **Dependency consumption:** link imported targets from `find_package` so
  include paths, compile requirements, and link dependencies travel together.
- **Header-only components:** use an `INTERFACE` library to carry their usage
  requirements. Use a helper target or module for shared settings when it
  removes current repetition and has clear ownership.
- **Header membership:** use `target_sources(... FILE_SET ... TYPE HEADERS)`
  to associate header files and their base directories with a target, then
  reuse the same set in installation when needed.
- **Recurring commands:** use configure, build, and test presets to give actual
  workflows repeatable names. Share project choices in `CMakePresets.json`
  and keep local paths or machine choices in `CMakeUserPresets.json`.
- **Tests:** integrate with CTest and register executable tests using
  `add_test(NAME ... COMMAND <test-target>)` so target resolution stays with
  CMake.

## Keep it simple

- Start with the smallest clear target graph that matches the real requirements.
- Prefer obvious target names and dependency flow over clever indirection.
- Do not multiply targets or helper modules just to look more modern.
- Keep compiler options conservative by default, especially for small projects.
- Project-owned C++ targets using an MSVC-compatible command-line frontend use
  target-scoped `/utf-8` by default. Keep it off imported and third-party
  targets. Detect the effective frontend, including clang-cl, using a form
  available at the declared CMake floor.

## When uncertain

If a modern feature seems promising but support or tradeoffs are unclear, verify it against the official CMake documentation before recommending it as the default path.

Start with the [buildsystem guide](https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html),
[target sources](https://cmake.org/cmake/help/latest/command/target_sources.html),
or [presets manual](https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html)
for the corresponding facility; select the project's documentation version
when the behavior or version floor matters.
