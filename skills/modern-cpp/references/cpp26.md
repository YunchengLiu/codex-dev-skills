# C++26 Guidance

Use this reference when the user explicitly targets C++26 or asks about a
named C++26 facility. Select by a concrete benefit and verify that feature's
compiler and library support.

## Useful candidates

- **Pack indexing:** select an element of a parameter pack directly when
  existing recursive helpers or tuple indirection serve only that purpose.
  See [pack indexing](https://eel.is/c++draft/expr.prim.pack.index).
- **`std::inplace_vector`:** use a variable-size contiguous container with
  fixed capacity and in-object element storage when that capacity is part of
  the problem. Choose the insertion operation to match the required
  full-capacity behavior. See the
  [container overview](https://eel.is/c++draft/inplace.vector.overview).
- **`std::function_ref`:** use a non-owning callable wrapper when bounded
  borrowing and type erasure are needed. The callable must outlive invocation;
  retain the internal repeated-callback template default when erasure has no
  concrete benefit. See the
  [callable wrapper](https://eel.is/c++draft/func.wrap.ref).

These are starting points, not a complete feature list. For another named
facility, consult its standard wording and implementation evidence.

## Support checks

- Verify compiler and standard-library support for the selected facility;
  partial language-mode support is insufficient.
- Keep adoption local to the useful feature. State the required compiler and
  library evidence before using it in shared or long-lived code.
- When the active toolchain lacks the facility, identify a supported
  alternative or the toolchain decision needed. Add a code fallback only when
  an actual supported toolchain or consumer requires both paths.
- Check consumer requirements for a supported API or ABI boundary. C++26
  remains an explicit choice, not the default baseline for general C++ work.
