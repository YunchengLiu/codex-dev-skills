# High-Risk Areas

These areas deserve extra caution because they often make CMake code harder to maintain.

## Global state

- Avoid broad `include_directories`, `add_definitions`, `link_libraries`, and raw global flag mutation when target APIs can express the intent.
- Avoid cache variables as the primary control-flow mechanism for ordinary project structure.

## File discovery

- Do not recommend `file(GLOB...)` for core source management by default.
- Prefer explicit source lists unless the project has a specific low-risk case for automatic discovery.

## Generator expressions

- Use generator expressions when they solve a real target or configuration problem.
- Do not let them turn the build into a second scripting language.

## Dependency management

- Prefer `find_package` with imported targets when the dependency story is already package-oriented.
- Use `FetchContent` deliberately, not as the automatic answer for every dependency.
- Inherit the project's existing dependency model before recommending a different one.
- Call out reproducibility, offline, CI, and consumer-impact tradeoffs before recommending vendoring or build-time acquisition.
- Keep third-party acquisition logic from taking over the core project structure.

## Cross-platform and cross-compiling

- Be careful when recommendations depend on generator behavior, IDE integration, toolchain files, or cross-compiling.
- Verify the exact behavior against official CMake documentation when these concerns matter.

## Policy handling

- Do not recommend policy changes casually.
- Verify the policy meaning, version floor, and behavioral impact against the official CMake documentation before suggesting it.
