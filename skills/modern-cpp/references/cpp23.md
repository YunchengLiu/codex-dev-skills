# C++23 Guidance

Use C++23 for focused improvements after confirming real compiler and standard-library support.

## Commonly valuable features

- `std::expected` for value-or-error flows where the calling code becomes clearer
- `std::to_underlying` for explicit enum-to-integer conversion
- Expanded constexpr support when it simplifies implementation or testing
- `if consteval` when compile-time and runtime paths genuinely differ
- Monadic-style library additions when they simplify local composition without hiding control flow
- `std::mdspan` for multidimensional views only when the toolchain and problem domain make it worthwhile

## Default posture

- Treat C++23 as an incremental upgrade, not a reason to rewrite C++20 code wholesale.
- Prefer features with a clear payoff in local code first.
- Verify library support carefully before proposing library-heavy changes.

## Migration note

C++23 works best as a selective quality-of-life upgrade on top of already healthy C++20-era code.
