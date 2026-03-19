# Data and DataLoader

## Prefer clear dataset boundaries

- Keep data access, collation, and transformation logic understandable.
- Use `Dataset` and `DataLoader` idioms before inventing custom loading frameworks.
- Make it easy to see where batching, shuffling, sampling, and augmentation happen.
- For standard loading patterns, prefer PyTorch's official data-loading documentation, `pytorch/examples`, and other mature, reliable implementations before adding custom scaffolding.

## Tune loader complexity to the need

- Start with simple loading behavior that is easy to reason about.
- Add multiprocessing, pinned memory, persistent workers, custom samplers, or prefetch tuning only when the task and runtime justify them.
- Keep worker-side side effects and randomness explicit enough to debug.

## Readability matters

- Do not hide important data-shape or preprocessing assumptions behind thin wrappers that add confusion.
- Keep the path from raw sample to model input easy to inspect.
