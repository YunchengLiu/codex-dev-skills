# Build Mechanics and Pitfalls

Use these rules when source discovery, generated artifacts, conditional
requirements, or platform behavior affect build correctness.

## Global state

- Avoid broad `include_directories`, `add_definitions`, `link_libraries`, and raw global flag mutation when target APIs can express the intent.
- Avoid cache variables as the primary control-flow mechanism for ordinary project structure.

## File discovery

- Use `file(GLOB[_RECURSE] ... CONFIGURE_DEPENDS)` by default for a project
  target's regular `.cpp` files when it owns the complete searched directory or
  subtree.
- Keep the search rooted inside that ownership boundary. Do not recursively
  capture sources belonging to an independently defined child target, and do
  not use one broad repository glob followed by exclusion lists.
- Keep collection variables local to the owning target setup and `unset()`
  every temporary source list after registration. Validate a newly discovered
  file with a fresh configure followed by a build so discovery is part of the
  evidence.
- Use explicit lists for exceptional or generated files that do not follow
  the target's normal discovery pattern or when the project itself explicitly
  requires them.

## Generated files

- Use `configure_file` for inputs resolved during configuration and
  `add_custom_command(OUTPUT ...)` for files produced by a build-time tool.
- Declare inputs with `DEPENDS`, outputs or byproducts as appropriate, and
  register the generated files with their owning target. This gives the build
  graph enough information to regenerate them when inputs change.
- Keep generated files in the build tree and use `VERBATIM` for custom-command
  argument handling. Add a custom target when the operation needs an explicit
  build entry point or a dependency anchor.

## Generator expressions

- Use generator expressions for target properties that vary by configuration,
  language, or build/install context. Evaluate configuration-dependent choices
  at generation time so they also work with multi-config generators.
- Do not let them turn the build into a second scripting language.

## Dependency management

- Prefer `find_package` with imported targets when the dependency story is already package-oriented.
- Use `FetchContent` deliberately, not as the automatic answer for every dependency.
- Inherit the project's existing dependency model before recommending a different one.
- Do not switch dependency acquisition models casually just because another option looks more modern on paper.
- Call out reproducibility, offline, CI, and consumer-impact tradeoffs before recommending vendoring or build-time acquisition.
- Keep third-party acquisition logic from taking over the core project structure.

## Cross-platform and cross-compiling

- Be careful when recommendations depend on generator behavior, IDE integration, toolchain files, or cross-compiling.
- Verify the exact behavior against official CMake documentation when these concerns matter.

## Policy handling

- Do not recommend policy changes casually.
- Verify the policy meaning, version floor, and behavioral impact against the official CMake documentation before suggesting it.

## Official references first

- Prefer official command, guide, policy, and presets documentation before relying on memory for version-sensitive CMake behavior.
- When the exact behavior may differ across releases, prefer documentation that matches the project's effective CMake version.
- When useful, inspect mature public CMake projects for pattern reference only after the official documentation path is clear.
