# Synthesis Mode

Use this mode when the user has already gone through one or more rounds of discussion and the note should mainly capture the agreed understanding.

## Source of truth

- Treat the multi-turn discussion, user corrections, accepted tradeoffs, and stable decisions as the main source of truth.
- Do not silently replace the agreed picture with a generic textbook explanation.
- Brief background is allowed only to make the final note coherent and readable. Do not use “background” to sneak in new technical conclusions or decisions.
- Do not mention the discussion/chat explicitly in the final note (no “在对话中/我们讨论/如上所述”). Keep it as a normal standalone note.
- If adding background or an example that was not in the discussion, keep it short and never override the agreed conclusions. If it changes what should be concluded, move it to `待确认 / 未验证` (or ask).

## Web scan (optional but encouraged)

When internet is available, web scan can be used as material gathering for:

- Fact checking and catching common misconceptions
- Finding better examples or standard terminology

Rules:

- Do an aggressive sweep if helpful (scan multiple sources quickly, then keep the best 2–5).
- Prefer official/primary sources for factual claims (vendor docs, standards/specs, original papers).
- Rewrite explanatory prose in your own words; do not paste long chunks. Verbatim copy is reserved for reproducibility literals (commands/config/flags/error text/version IDs).
- If you must quote prose, keep it clearly marked, attributed, and short (<= 25 words per source).
- If a web scan contradicts an agreed conclusion, do not silently replace it. Ask or record under `待确认 / 未验证`.
- If you used web scan, add 2–5 links under `参考` (each with a one-line “用于：…” note).

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
