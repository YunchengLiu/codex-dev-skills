# Runtime Logging

## Scope

Apply when adding, modifying, planning, or reviewing runtime logs. Read the
project's actual logging API, level definitions, logger ownership, and sink or
initialization code when those details affect the change; this reference is not
an API catalog.

Runtime messages use concise, natural English unless a stronger product rule
explicitly chooses another language.

## Hard Rules

1. Prefer no log over a low-value log.
2. Put logs on main paths, key stages, state changes, unusual-but-valid paths,
   and failure boundaries. Keep tiny predicates, conversions, getters, and
   helpers quiet unless they own independent diagnostic meaning.
3. Preserve the existing logger owner. Add a facade, module logger, or logging
   dependency only when the user explicitly requests that design. If ownership
   is unclear, keep the change local and ask for the intended owner before
   adding infrastructure.
4. Use trace for the execution skeleton, debug for diagnostic context, info for
   important successful timeline events, warn for legal but non-standard paths,
   error for failed or rejected operations, and critical only when reliable
   continuation is no longer possible.
5. A returned error status or expected-like failure is still a failure boundary;
   do not lower it merely because it does not throw.
6. Record one failure once, at the boundary with the best stable context. Do not
   log the same event in every helper, wrapper, implementation, and catch.
7. Use a stacktrace only when the current call stack has explicit diagnostic
   value. Most failure paths use an ordinary error log.
8. Keep messages short, stable, grep-friendly, and meaningful after value
   substitution. Do not repeat words already carried by an identifier, device
   name, filename, tag, or operation value.
9. Prefer readable enum or domain values. Include underlying numbers only when
   wire format, ABI, bitmask, serialization, or out-of-range diagnosis makes the
   numeric value material.
10. Summarize large data by count, range, size, identifier, checksum, sample, or
    other bounded metadata. Do not dump secrets, credentials, large payloads,
    meshes, buffers, command lists, or containers by default.
11. Target near-zero cost when logging is disabled and low, bounded cost when
    enabled. Explicitly gate heavy summaries, stack capture, scans, joins,
    dumps, and expensive conversions.
12. Logging must not become a likely new failure or state-change path. Do not
    access a file, network, device, live hardware, risky lock, mutable operation,
    or large allocation solely to construct a log. Inspect optional or nullable
    context only when its presence is established; otherwise omit that detail.

## Decide Whether To Log

Ask what a maintainer could learn from the event that is not already clear from
the caller's log or returned failure. Useful locations include:

- public or module entry points whose execution matters;
- file, I/O, configuration, SDK, hardware, and cross-module boundaries;
- lifecycle transitions and important state changes;
- major stages of a long or expensive workflow;
- explicit skip, no-op, fallback, degraded, or unsupported paths that may
  surprise a caller;
- the boundary that converts, returns, throws, or propagates a failure.

A helper that only classifies, compares, normalizes, converts, or returns a
field normally inherits its caller's logging. Reuse does not make a helper a
logging owner.

For a public wrapper and a concrete backend or device implementation, assign
each lifecycle or operation event to one layer. The public layer may record the
caller-visible request or common rejection; the concrete layer may record the
native operation and backend context. Do not repeat the same lifecycle message
at both layers. A project-specific interface rule overrides this general split
where it explicitly assigns ownership.

## Trace Coverage

Use the project's established trace mechanism for important API entry points and
workflows. Duration traces fit I/O, device calls, serialization, geometry or
numeric processing, and other plausibly expensive operations. Step traces fit
major sub-stages of one complex operation.

Keep traces out of tiny helpers and hot-loop iterations unless the task
explicitly requests that instrumentation. Give a new key entry point created
by the current task a trace through the project's established mechanism.
Merely touching an existing function does not require retrofitting trace
coverage; that is separate logging work.

Trace provides the execution skeleton. Debug supplies parameters, normalized
values, decisions, and state needed to explain that skeleton.

## Level Policy

- **trace:** function or process entry/exit and major workflow movement;
- **debug:** request parameters, normalization, branch decisions, legal early
  exits, and detailed diagnostic context;
- **info:** important successful operations, lifecycle transitions, state
  updates, and idempotent completion that matters to callers;
- **warn:** legal but non-standard behavior, fallback, degraded mode,
  recoverable anomaly, unsupported optional capability, or surprising no-op
  that does not fail the requested operation;
- **error:** the current operation fails, rejects the request, throws, returns a
  failure status, or propagates a failure across a boundary;
- **critical:** the process, logging system, resource state, or safety boundary
  cannot continue reliably.

An info-and-above view should reconstruct the important timeline. Trace and
debug explain how it was reached. Do not use info for routine high-frequency
events or error for a successful but merely unusual path.

## Failure And Stacktrace

Log a failure at the boundary that has both the operation identity and stable
context. If the failure already carries accurate throw-site diagnostics, do not
capture another stack by reflex. A current stacktrace is justified at a
non-exception diagnostic point, when throw-site information is unavailable, or
when the user explicitly requests it.

For expected-like, status, or error-code returns, include the operation subject
and the useful reason or code already carried by the result. For catch-and-
rethrow, include only context required to identify the outer operation and
preserve the original failure according to
[error-handling.md](error-handling.md).

Logging never replaces return, propagation, or throwing. A logging failure must
not obscure the primary operation's failure.

## Message Shape

Prefer a stable shape such as:

```text
<subject> '<id>' <operation> <state>: key=value
```

Read likely value shapes before choosing surrounding words. If a device name may
already contain its device type, do not repeat that type in the message. Use
direct technical wording rather than narrative, decoration, mechanical labels,
or implementation history.

Good message pairs make the request and result easy to correlate without
copying every parameter:

```cpp
LOG_DEBUG("device '{}' power update requested: value={}", name, value);
LOG_INFO("device '{}' power updated: value={}", name, value);
LOG_ERROR("device '{}' power update rejected: value={} is out of range", name, value);
```

The macro names are illustrative. Use the project's configured API and owning
logger family.

Read [logging-examples.md](logging-examples.md) for contrasting no-op and
failure paths, substituted identifiers, trace scopes, and bounded context.

## Performance And Failure Budget

- Pass cheap already-available values to a logging macro so its level check can
  skip formatting.
- Put heavy summaries, scans, joins, stack capture, filesystem work, and
  expensive conversions behind an explicit level check.
- Aggregate high-frequency progress instead of logging each item.
- Do not introduce repeated allocation or conversion into hot paths for routine
  logs.
- If useful extra context has meaningful failure or side-effect risk, log the
  stable context already in hand or omit the detail.
- Preserve primary control flow, performance, and failure behavior before
  improving observability.

## Review And Ablation

For each log, ask:

1. Which timeline, state, unusual branch, or failure would become materially
   harder to understand if it were removed?
2. Does another layer already own and record the same event?
3. Is its level determined by path semantics?
4. Is its context stable, bounded, non-sensitive, and cheap to obtain?
5. Would removing an argument retain the same diagnostic value?

Remove logs and arguments that do not change diagnosis or timeline
reconstruction. Do not use ablation to remove a project-required audit or safety
event.
