# C++23 Guidance

Use C++23 to simplify result handling, enum conversion, callable ownership,
and multidimensional or compile-time code when the active toolchain supports
the selected facility.

The examples below are representative, not exhaustive. The usable feature set is determined by the effective standard, compiler, standard library, project constraints, and local build evidence.

## Language features

- Explicit object parameters only when they make a member-like API materially clearer
- Expanded constexpr support when it simplifies implementation or testing
- `if consteval` when compile-time and runtime paths genuinely differ
- Multidimensional subscript support only when the type and compiler support story are already clear

## Library features

- `std::to_underlying` for explicit enum-to-integer conversion
- `std::expected` for value-or-error flows where the calling code becomes clearer
- Monadic operations for `std::optional` and `std::expected` when they simplify local composition without hiding control flow
- `std::mdspan` for multidimensional views only when the toolchain and problem domain make it worthwhile
- `std::print` and `std::println` only when library support is confirmed and simple console output is the real need
- [`std::ranges::to`](https://eel.is/c++draft/range.utility.conv.to) to
  materialize a range into a requested container when the result needs owned
  storage; keep the allocation and element-copy or move cost visible
- `std::move_only_function` when move-only call wrappers are genuinely needed

## Good default candidates

- Use `std::expected` for an agreed value-or-error interface and
  `std::to_underlying` when enum conversion would otherwise repeat the
  underlying type or a cast convention.
- Use `std::move_only_function` for stored callbacks that own move-only state
  when an owning, type-erased callable is needed.
- Use explicit object parameters to share member implementation across
  receiver forms when that removes real overload duplication.
- Use `std::mdspan` when a borrowed multidimensional buffer needs explicit
  extents and layout; keep storage ownership with the existing owner.
- Prefer direct result checks or short monadic composition according to which
  makes error propagation and control flow clearer.

## Needs extra verification

- Be careful with `std::expected`, `std::mdspan`, `std::print`, and newer ranges facilities because support and ecosystem readiness can lag the language mode.
- Keep monadic chaining readable; if it obscures control flow, prefer the direct form.

## When uncertain

Check the selected feature's semantics, feature-test macro, and vendor
implementation evidence. Choose supported facilities for the current code;
the language-mode flag alone is not the acceptance signal.
