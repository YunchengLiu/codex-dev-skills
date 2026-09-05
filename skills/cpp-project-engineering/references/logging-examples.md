# Logging Examples

These examples use illustrative macros. Use the project's actual logging API
and logger owner; closer interface rules control their assigned levels.

## Trace The Operation And Its Stages

Log the caller's operation rather than the tiny helper it happens to use:

```cpp
LOG_DEBUG("graph assembly started: records={}", records.size());
auto graph = buildGraph(records);
LOG_DEBUG("graph assembly completed: nodes={}", graph.nodeCount());
```

A predicate such as `index < size` does not independently explain the caller's
intent or failure. Keep it quiet. For duration traces, scope a trace to the
stage it measures:

```cpp
TRACE_FUNCTION_DURATION();
{
    TRACE_DURATION("export: preparing records");
    prepareRecords();
}
{
    TRACE_DURATION("export: writing output");
    writeOutput();
}
```

## Choose Levels From Outcomes

Routine early return is debug; meaningful idempotent success is info:

```cpp
if (records.empty()) {
    LOG_DEBUG("export skipped: no records");
    return;
}
if (isConnected()) {
    LOG_INFO("device '{}' already connected", name);
    return;
}
```

A legal optional-capability result is warn when it may surprise the caller:

```cpp
if (!probe_supported) {
    LOG_WARN("device '{}' connection probe unsupported", name);
    return;
}
```

A failed requested operation is error even when returned without throwing:

```cpp
if (!isReady()) {
    LOG_ERROR("device '{}' value query failed: device is not ready", name);
    return std::unexpected(notReadyError(name));
}
```

The result transport does not set the log level. Use error for a rejection or
failure, not for an ordinary request marker. Critical belongs to a system or
resource state that cannot continue reliably.

## Record A Failure Once

An owning boundary can identify the operation and preserve the exception:

```cpp
try {
    connectImpl();
} catch (...) {
    LOG_ERROR("device '{}' connection failed", name);
    throw;
}
```

Lower helpers should not repeat that failure. Use an ordinary error log when
throw-site diagnostics already supply the useful stack; capture the current
stack only for a distinct diagnostic need or an explicit interface rule.

## Check The Substituted Message

If `name` is `"laser emulator"`, this reads naturally:

```cpp
LOG_ERROR("device '{}' simulates connection failure", name);
```

`"emulator '{}' simulates connection failure"` would repeat the emulator
identity. The same check applies to filenames, tags, and logger names. Prefer
`"export failed: path={} error={}"` to a sentence that repeats a file extension
already present in the path.

## Bound Cost And Failure Risk

Summarize large values and gate work that is not already available:

```cpp
if (logger.shouldLog(Level::Debug)) {
    auto summary = summarizeCommands(commands);
    logger.debug("command list summary: {}", summary);
}
```

The summary must still be bounded and low-risk. Prefer count, range, identifier,
or a selected sample; full dumps require an explicit diagnostic request.

Aggregate repeated events outside a hot loop:

```cpp
std::size_t rejected_count = 0;
for (auto const& item : items) {
    if (!accept(item)) {
        ++rejected_count;
        continue;
    }
    process(item);
}
LOG_DEBUG("processing completed: input={} rejected={}", items.size(), rejected_count);
```

Use stable context already in hand:

```cpp
LOG_WARN("device '{}' status query skipped: reason={}", name, reason);
```

Calling `sdkQueryFirmwareVersion()` solely to enrich that warning can block,
fail, or touch hardware. Likewise, check optional state before inspecting it;
omit unavailable context instead of dereferencing it for logging.
