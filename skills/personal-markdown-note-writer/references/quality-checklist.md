# Quality Checklist

Run this checklist after drafting a note.

## Content

- The structure makes it obvious whether each top-level section is a learning note or a tool/setup note (no need to label the type in the output).
- The first section explains what the note is about in 1–3 sentences.
- If there are material unknowns, put them in a short `待确认 / 未验证` section; otherwise omit that section.
- The note is not dominated by exclusion/defensive language.
- Learning notes include at least one complete toy example that a beginner can follow end-to-end.
- If prior discussion material exists, the note reflects the agreed conclusions and starts from them, instead of drifting into a fresh, generic write-up.
- If web scan was used in synthesis mode, do not silently override the agreed conclusions: keep new ideas small as `补充` / `可选变体`; if it suggests a material correction, pause and confirm with the user before finalizing; otherwise capture the conflict under `待确认 / 未验证` with links.
- If `参考` is present, each link supports at least one concrete fact/terminology choice/example in the note, and includes a one-line “用于：…” note.
- No long verbatim prose copying. Any prose quote is short (<= 25 words per source), clearly marked, and attributed; verbatim copy is reserved for reproducibility literals (commands/config/flags/error text/version IDs).

## Language

- No chat meta (no “本次对话/我们讨论/用户提到/整理如下”).
- No machine-translation feel (avoid heavy “因此/从而/进而/即可” chains).
- Terms are introduced with meaning before definition.
- Default voice is impersonal: avoid first-person “我…”, avoid second-person “你…”, avoid lecture/script tone unless requested.
- No awkward narrator phrases like “我想/我觉得/我需要…”.

## Structure

- Lists are used sparingly; paragraphs carry the narrative.
- Headings are meaningful and not just “背景/内容/其它”.
- No empty sections (remove template-only sections like `待确认 / 未验证` / `参考` when not used).
- The note does not feel like a filled-out form; sections that add ceremony without value are removed.
- If the note tries to do two different jobs, they are separated into distinct sections (or separate files only if the user asked).
- Headings are plain (no guidance in parentheses like `（先讲明白）` by default).
- The explanation budget matches the user's likely gaps; already-understood parts are not over-expanded.

## Tool notes only

- Includes a short `要点` section (2–5 lines) before steps, stating the recommended path and key choices.
- Steps are copy-pasteable and ordered.
- Placeholders are minimal and explained.
- Includes at least one verification method.
- Destructive actions are clearly flagged.
- Commands match the declared OS/shell; cross-platform commands are separated by subsections.
- Execution location and required working directory are explicit (local vs remote vs container/WSL, repo root, etc).
- Any step requiring elevated privileges is annotated at that step (what privilege is needed and why), instead of a long global warning block.
- Paths are unambiguous (absolute, or explicitly relative to the declared working directory); paths with spaces are quoted using shell-appropriate quoting.
- If multiple environments are supported, each environment has its own subsection with a complete path; commands are not interleaved.
- Verification includes expected output or a clear success criterion.
- No secrets are present (tokens/passwords/private keys are placeholders).
- If web scan was used, include 2–5 links under `参考`.
