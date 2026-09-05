# Migration Patterns

Use these patterns to modernize existing CMake code incrementally.

## Start local

- Prefer a small migration that fixes the current problem over a broad rewrite.
- Update affected targets and build callers coherently, including current
  user entry points, CI workflows, release scripts, and supported consumers.
- Separate structural cleanup from behavior changes when possible.

## Common migration shapes

### Global settings to target settings

- Replace directory-scoped include paths, definitions, and flags with target-based APIs first.
- Move shared behavior into small helper targets or focused helper modules instead of repeating settings everywhere.

### Repeated command lines to presets

- Add presets when the project has repeatable configure and build commands worth standardizing.
- Keep presets aligned with real workflows such as debug, release, sanitizers, or platform-specific development.
- Share common project settings through preset inheritance and put
  machine-specific paths or selections in user presets. Match the preset
  schema to the CMake floor supported by those workflows.
- Do not force many preset combinations into a project whose workflow is still simple.

### Source and header organization

- For a target that owns a complete source directory or subtree, prefer a
  constrained `file(GLOB[_RECURSE] ... CONFIGURE_DEPENDS)` for its regular
  `.cpp` files. Do not cross an independent child target boundary or collect the
  whole repository and subtract exceptions.
- Register the discovered sources with their owner and `unset()` every
  temporary source list afterward. Keep generated and exceptional entries
  explicit.
- Use `FILE_SET HEADERS` when the target, IDE, or install rules benefit from
  shared header membership and base directories at the supported baseline.
- Do not force a fixed directory template such as an explicit `include/` tree unless the project needs that boundary today.

### New project initialization

- Start with the executable or library targets, their source ownership, usage
  requirements, and dependencies. Add tests and repeatable presets for current
  workflows; add install, export, or package config when consumption needs it.
- Still organize targets, include layout, and generated files so future install support does not require a redesign.
- When evolving an existing project, keep target naming and directory conventions aligned with the current project unless the user asked for a broader reorganization.

## When uncertain

If a migration path depends on newer CMake behavior or subtle generator semantics, verify against the official CMake documentation before prescribing the change.
