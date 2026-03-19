# Style Principles

Apply these semantic style defaults across projects unless the repository defines stronger local rules.

## Core defaults

- Prefer simple interfaces with explicit data flow.
- Prefer value semantics for local ownership and regular types.
- Make borrowing, ownership, and lifetime visible in types and function signatures.
- Use RAII to make cleanup automatic and exception-safe.
- Prefer standard-library facilities over custom wrappers when they carry the right meaning.

## Abstraction rules

- Introduce abstraction to capture a stable concept, constraint, or invariant.
- Do not introduce abstraction only to look modern.
- Keep templates and concepts narrow and readable.
- Prefer direct code over generic machinery when the generic version does not materially improve reuse or safety.

## Cost visibility

- Avoid APIs that hide allocation, ownership transfer, or expensive work.
- Be careful with lazy views, proxy types, and deeply composed pipelines in code that must be debugged often.
- Treat compile-time cost as a real cost.

## Contracts

- Use stronger types to express real constraints.
- Use `const`, `constexpr`, and `noexcept` when they are correct and helpful, not by reflex.
- Keep error handling explicit. Choose mechanisms that match the contract and the calling style.

## Change posture

- Prefer focused improvements that leave surrounding stable code alone.
- Suggest follow-up migrations separately when they require broader coordination.
