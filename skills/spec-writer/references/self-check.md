# Self-check

## Binding Rules

- Check whether the spec will produce consistent implementations across capable agents.
- Check whether routine execution can be handled by capable implementation agents with finite attention and clear structure.
- Check that the spec targets capability level with agent-runtime-neutral guidance.
- Check that the spec aligns implementation at the contract level and preserves private implementation latitude.
- Check that minimal-entity execution is encoded as brief structure and final review guidance.
- Treat ambiguity, scope expansion, fixture drift, and cross-component leakage as blockers.
- Treat unbounded generality as a blocker for local or limited-domain features.
- Review the actual repo landing points and the prose together.
- Check phase briefs independently from canonical docs.
- Check stable/dynamic document mutability: stable docs, phase briefs, and frozen fixtures require explicit revision scope; dynamic records preserve existing unrelated content.
- For self-check review requests, report issues that can cause implementation error or divergent execution.

## Spec Architecture Check

- Does the spec start from repo evidence: modules, tests, public APIs, fixtures, and existing conventions?
- Is the work classified as refactor, incremental feature, or new development?
- Are stable docs and dynamic records separated?
- Are phase briefs planned as independently feedable slices?
- Is there a fresh-agent entry path from stable plan to current brief to latest progress?
- Is there a current-phase pointer naming the current phase, current brief, blocker state, and next action?
- Are new-development file paths, names, public surfaces, fixtures, and commands concrete?
- Are refactor allowlists and frozen paths explicit?
- Is the feature classified as repo-local, limited-domain, or general-purpose?

## Contract Check

- Does each component contract state role, pipeline position, input source, upstream guarantees, local checks, output, and failure behavior?
- Are important internal invariants stated positively and guarded with repo-standard assertions where appropriate?
- Does it state the intended generality boundary and implementation depth?
- Does the spec say how much error handling is required?
- Does the text default to minimal failure behavior and use a dedicated contract for richer failure handling?
- If failure behavior is implementation-visible, is the error shape specified by the contract or inherited from repo convention?
- Are public capabilities concrete enough to implement and test?
- Does the spec preserve private helper bodies, exact control flow, and mechanical edits as implementation latitude when they are contract-neutral?
- Are rationale and alternatives kept out of execution-facing contracts?
- Does the spec target capability level rather than named execution-model assumptions?

## Brief Check

- Can the current phase brief be given to an implementation agent as a self-contained slice?
- Can the brief be read with finite attention and still produce the intended implementation from current-phase contracts?
- Can a new agent started with a short repo-local prompt identify the current phase, files to read, first action, and handoff condition from repo-local docs?
- Does it include current-phase contracts and directly relevant component details?
- Does it include allowed create/modify paths and frozen paths?
- Does it state out-of-contract input behavior where upstream guarantees matter?
- Do internal assertions preserve the stated validation and failure-handling depth?
- Does it state the current feature's generality boundary and keep local behavior at the required mechanism depth?
- Does it preserve implementation latitude for contract-neutral private mechanics?
- Does it include a final minimal-entity check as end-of-implementation review guidance?
- Does it include fixture/table acceptance?
- Does it define verification commands and handoff condition?
- Does it use boundary reporting for defined boundary conditions?

## Acceptance Check

- Are natural-language rules backed by `input -> expected` fixtures or tables when interpretation matters?
- Are fixture files marked frozen?
- Is there a fixture errata path through `progress/decisions.md`?
- Does the fixture errata rule distinguish partial contradictions from sole or canonical acceptance contradictions?
- Would two capable agents infer the same expected behavior from the acceptance section?

## Dynamic Record Check

- Does `progress/` record state points as its operational history?
- Are decisions written before implementation choices that fill spec gaps?
- Do decisions include phase, source, question, decision, reason, and canonical-update flag?
- Are dynamic records append-oriented, with corrections added as new entries while unrelated content remains preserved?
- Are fixture contradictions recorded while frozen fixtures remain unchanged?
- Are canonical updates promoted explicitly through stable docs?

## Output Standard

If any check fails, state the concrete risk and the file or section that should change. When a self-check review has no substantive blocker, output exactly:

```text
未发现实质问题
```
