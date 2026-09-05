# CMake And Install Boundaries

## Scope

Apply when changing targets, sources, headers, compiler options, dependencies,
presets, install, export, packaging, or generated build artifacts.

## Hard Checklist

1. Respect the declared CMake floor, C++ standard, compiler frontends,
   generators, platforms, and project dependency model.
2. Express compile features, options, definitions, include paths, and link
   requirements on the owning target with correct visibility.
3. Apply project defaults only to project-owned targets, not imported or
   third-party targets. Use target-scoped settings rather than broad global flags.
4. Project-owned C++ targets using an MSVC-compatible command-line frontend use
   target-scoped `/utf-8` by default.
5. A source glob remains inside the target's ownership boundary, uses
   `CONFIGURE_DEPENDS`, and never captures an independent child target.
6. Classify each reusable header as module-facing, reachable
   implementation-support, or private, independently of whether the target is
   currently installed.
7. Match dependency visibility to what consumers must compile or link; source-
   only dependencies remain private.
8. Add install, export, package, preset, dependency-acquisition, or helper
   machinery only for a current product or workflow need.
9. Before using a new third-party API, verify its dependency declaration and
   target wiring. Adding a dependency also requires a current reason and an
   appropriate license, maturity, security, performance, and rollback check.
10. Review build-tree, install-tree, exported-consumer, and package-layout
    impact whenever a public header, file set, target, or dependency boundary
    changes.
11. Validate source discovery with configure plus build, and validate install or
    export changes through the actual project-native consumer path when that
    surface is part of the task.

## Target-Based Structure

Prefer a clear target graph over directory-scoped or global state. Use target
APIs for sources, include paths, compile features, options, definitions, and
dependencies. More targets and helper modules are not automatically better;
add one only for a real ownership, dependency, generated-artifact, platform, or
consumer boundary.

Inherit the project's current package manager and dependency acquisition path.
Do not switch among `find_package`, vendoring, submodules, `FetchContent`, or
another model because one looks more modern. Prefer imported targets when the
dependency already exposes them.

Do not patch flags, policies, or build structure to hide a compiler internal
error. Reproduce and report the crash according to project rules.

## MSVC-Compatible UTF-8

Every project-owned C++ compile target driven by an MSVC-compatible command-line
frontend uses `/utf-8` as the default source and execution character-set
baseline. This includes clang-cl when it is operating with MSVC-compatible
options.

The condition determines applicability; it does not make UTF-8 optional:

- apply the option to project-owned compile targets using that frontend;
- do not apply it to GCC-style frontends, imported targets, third-party targets,
  interface-only targets with no compilation, or languages for which the option
  is not valid;
- use target-scoped `target_compile_options` or the project's established
  helper, not `CMAKE_CXX_FLAGS` or another global mutation;
- detect the effective compiler frontend using facilities supported by the
  project's declared CMake floor rather than assuming compiler identity alone
  determines flag syntax;
- a deliberate different source-encoding contract must be explicit in the
  project and overrides this default for the affected target.

Do not add a second fallback source encoding to accommodate unspecified
non-UTF-8 files. A real non-UTF-8 input contract is a project decision, not a default
compatibility obligation.

## Source Discovery And Ownership

For regular project `.cpp` files, use
`file(GLOB ... CONFIGURE_DEPENDS)` or
`file(GLOB_RECURSE ... CONFIGURE_DEPENDS)` when the owning target controls the
complete searched directory or subtree.

- Root the glob at the smallest directory that expresses target ownership.
- Do not use one repository-wide recursive glob followed by exclusion lists.
- Do not cross a subdirectory that defines an independent target. Give that
  target its own collection.
- Use explicit source entries when exact membership is a deliberate target
  constraint, for exceptional files outside the normal owned subtree, for
  generated outputs whose lifecycle requires explicit wiring, or when a
  stronger project rule requires an explicit list.
- Keep collection variables local and `unset()` every temporary source list
  after passing it to the owning target so it cannot be reused by accident.
- After adding or moving a source, run a fresh configure and then build the
  owning target or normal build preset. Compilation alone without reconfigure
  does not prove the glob discovered the file.

Automatic discovery is not permission to blur ownership. Explicit lists are
not inherently safer when they duplicate a directory's already clear target
boundary.

## Header Roles

Classify each reusable-library header by what consumers need:

1. **Module-facing header:** other project targets or external consumers include
   it as the normal interface. Put it in the project's public/build-interface
   file set.
2. **Reachable implementation-support header:** callers do not treat it as the
   module interface, but a module-facing header reaches it through templates,
   inline definitions, traits, or required implementation support. Put it in a
   separate implementation-support file set using the project's established
   visibility.
3. **Private header:** no module-facing header reaches it and no supported
   consumer includes it. Register it privately with the owning target.

Plain private registration is the default for implementation headers. Tests
may still include these headers from the source tree; direct testing does not
make a header module-facing.

Installation status and role are separate. A non-installed library still has a
module-facing build-tree interface. A reachable implementation-support header
may need installation so consumers compile, but reachability does not make it a
stable public contract. A `detail/` path does not automatically prove either
reachability or privacy; follow the include graph.

If classification is unclear, state whether the header is a public contract,
a build-tree-only module interface, reachable implementation support, or
internal-only. Do not infer that role from its path.

Tests, benchmarks, final executables, and device or backend implementations that
expose no reusable header interface register sources and headers privately and
do not need API file sets.

Use the file-set names and install helper already established by the project.
Do not impose generic bucket names when a project has an equivalent model.

For each library target exposing module-facing headers, register its sources,
private headers, interface headers, and reachable support headers in one
coherent `target_sources()` block.

## Dependency Visibility

- A dependency required to compile a module-facing or reachable support header
  is a consumer compile requirement and needs corresponding public or interface
  visibility.
- A dependency used only by `.cpp` files or private headers remains private.
- Optional public extensions must not contaminate the required exported target.
- Moving a header or dependency between categories requires checking current
  consumers, exported targets, package config, and install layout.

Do not mark a dependency public merely because several internal targets use it;
shared internal use and consumer usage requirements are different facts.

## Install, Export, And Packaging

Add install, export, package-config, runtime deployment, or packaging machinery
only when the project currently ships or consumes that surface. A practice
project or local tool does not need a hypothetical package structure.

When the surface is required:

- keep build-tree and install-tree include behavior intentional;
- install every header needed for consumers to compile, while preserving the
  distinction between stable interface and reachable support;
- avoid leaking private compile definitions, options, or implementation helper
  targets into exported interfaces; preserve link dependencies that the final
  consumer actually needs, including a static library's private link
  dependencies;
- keep runtime dependencies, libraries, and package layout coherent across
  build, install, and packaging paths;
- treat an already released package or external consumer as a real
  compatibility commitment and discuss migration before breaking it.

Do not add compatibility for an uncommitted internal target name, helper, path,
or old build entry point. Update all repository callers coherently instead.

## Presets And Environment

Use project presets and user presets as the source of truth for toolchain,
generator, dependency root, build directory, and recurring validation entry
points. Do not manually search for a package-manager root, inject a toolchain
file, or add a parallel build directory when an applicable preset owns it.

Add or change presets only for a repeated workflow the project needs. Do not
multiply configurations or build a compiler matrix for theoretical coverage.

## Version-Sensitive Decisions

Before using a CMake feature, policy, generator expression, preset schema, file
set, install/export form, or cross-compiling behavior whose support matters,
verify it against official documentation for the project's effective CMake
version. State any raised version floor. Do not lock this skill to one clever
expression when a clearer form compatible with the project's floor provides the
same target-scoped behavior.
