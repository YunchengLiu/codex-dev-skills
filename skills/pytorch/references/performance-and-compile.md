# Performance and Compile

## Treat performance features as opt-in

- Do not recommend `torch.compile`, AMP, multi-GPU features, or loader tuning by default.
- Use them when there is a clear payoff and the runtime stack supports them.
- Keep the fallback path understandable.

## `torch.compile` needs extra caution

- Verify that the active Python and PyTorch runtime actually support the intended compile path.
- Remember that compile behavior can change debugging, tracing, autograd expectations, and startup cost.
- Do not present `torch.compile` as a free speedup without checking official guidance.
- Prefer official PyTorch documentation as the primary source, then compare against mature ecosystem usage before recommending compile-related changes.

## Prefer measurement over folklore

- Base performance suggestions on an actual bottleneck when possible.
- Prefer official PyTorch troubleshooting and runtime guidance over hearsay.
- If performance behavior is unclear, say so and verify before recommending a complex change.
