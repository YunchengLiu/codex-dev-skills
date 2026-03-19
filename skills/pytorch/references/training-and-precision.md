# Training and Precision

## Keep the main loop understandable

- Make the train, eval, and inference flow easy to follow.
- Keep forward, loss, backward, optimizer step, scheduler step, and metric handling visible enough to debug.
- Avoid abstractions that make it hard to see where tensors change device, dtype, or gradient state.
- For baseline training-loop structure, prefer official PyTorch examples, mature ecosystem implementations such as Hugging Face when they fit, and official documentation before inventing a local pattern.

## Use AMP deliberately

- AMP is useful when the runtime and model behavior justify it, but it is not a default requirement.
- Keep autocast and grad-scaler behavior explicit enough to reason about.
- Prefer correctness and clarity first when debugging unstable training.

## Keep train and eval boundaries explicit

- Be clear about `model.train()` and `model.eval()` transitions.
- Make no-grad or inference-mode usage explicit where it matters.
- Do not let helper layers hide important mode changes.
