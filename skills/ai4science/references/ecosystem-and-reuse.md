# Ecosystem and Reuse

## Prefer mature infrastructure first

- If the user explicitly specifies a framework, follow that choice.
- Otherwise reuse the project's existing mature framework-native infrastructure first. If the framework is still open and the task matches a typical modern deep-learning workflow, PyTorch can be the default first choice together with other mature open-source libraries where appropriate.
- Build custom NN plumbing only when existing tools fail a concrete requirement.
- Prefer borrowing a proven pattern over inventing a local abstraction for common experiment tasks.

## Look for strong precedents

- For training loops, evaluation, metrics, logging, checkpoint helpers, and experiment utilities, actively look for good open-source examples.
- Use external examples to shape local code organization, helper boundaries, and small implementation tricks.
- If a non-obvious trick is worth keeping, document it briefly in code comments.

## Recommend, do not force

- Suggest open-source libraries or helpers when they solve a real problem well.
- Explain what they buy and what they cost.
- Let the user decide whether the dependency is worth adopting.

## Avoid premature framework-building

- Do not turn early experiment code into a local mini-framework.
- Do not hide simple training logic behind abstractions that make iteration slower or less readable.
