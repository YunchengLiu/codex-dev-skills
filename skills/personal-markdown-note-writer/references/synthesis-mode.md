# Synthesis Mode

Use this mode when the user has already gone through one or more rounds of discussion and the note should mainly capture the agreed understanding.

## Source of truth

- Treat the multi-turn discussion, user corrections, accepted tradeoffs, and stable decisions as the main source of truth.
- Do not silently replace the agreed picture with a generic textbook explanation.
- Brief background is allowed only to make the final note coherent and readable. Do not use “background” to sneak in new technical conclusions or decisions.
- Do not mention the discussion/chat explicitly in the final note (no “在对话中/我们讨论/如上所述”). Keep it as a normal standalone note.
- If adding background or an example that was not in the discussion, keep it short and do not silently override the agreed conclusions. If it would change what should be concluded, pause and ask; if the user confirms, update the conclusion; otherwise move it to `待确认 / 未验证`.

## Web scan (recommended for public/common topics)

When internet is available, web scan can be used as **material gathering to widen the view** for:

- Fact checking and catching common misconceptions
- Finding better examples or standard terminology
- Sampling 1–2 common alternative approaches or pitfalls (so the note does not overfit the thread)

Rules:

- Definition: a `material correction` changes recommended path, key versions/commands/flags, prerequisites, core mechanism, or risk level.
- Do an aggressive sweep if helpful (scan multiple sources quickly, then keep the best 2–5).
- Prefer official/primary sources for factual claims (vendor docs, standards/specs, original papers).
- Rewrite explanatory prose in your own words; do not paste long chunks. Verbatim copy is reserved for reproducibility literals (commands/config/flags/error text/version IDs).
- If you must quote prose, keep it clearly marked, attributed, and short (<= 25 words per source).
- If a web scan contradicts an agreed conclusion, do not silently replace it:
  - If it is material and high-confidence, pause and ask the user to reconcile before finalizing the note (present 1–3 candidate corrections with links).
  - If the user does not want to change the conclusion, record it under `待确认 / 未验证` with links.
- If you used web scan, add 2–5 links under `参考` (each with a one-line “用于：…” note).
- Skip web scan when the topic is clearly private/personal or internal-only, or when the user explicitly requests “只用本对话/不查资料”.
- Query hygiene: never search with secrets (tokens/passwords/private keys). Avoid pasting large internal text or unique internal identifiers (internal domains, repo codenames, ticket IDs) into queries; use keywords.

## Writing flow

1. Extract the stable conclusions first.
2. Separate what was agreed from what is still open.
3. Decide which gaps belong to the note itself and which are just discussion noise.
4. Rewrite into a coherent note with the agreed conclusions up front.
5. Expand only where the discussion shows the user still had a real understanding gap.

## Depth calibration

Use the user's observed understanding to decide where to spend words:

- If the user already understands the broad picture, do not re-explain it at textbook length.
- If the user repeatedly asks about one mechanism, give that part more room.
- If the user corrected style/tone several times, preserve that preference explicitly in the final note.

## Common failure modes

- Replacing a negotiated conclusion with a “cleaner” but different generic explanation
- Re-expanding already-settled background while skipping the actual sticking point
- Letting the note read like a fresh tutorial instead of a polished record of the agreed understanding
