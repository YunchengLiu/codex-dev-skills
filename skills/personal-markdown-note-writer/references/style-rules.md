# Style Rules (Chinese Notes)

These rules optimize for: readable later, neutral tone, and “written like a human note”, not like a transcript or a spec.

## Must

- **No chat meta**: do not write sentences like “本笔记整理自对话 / 我们讨论了 / 用户提到 / 下面总结”.
- **Lead with meaning**: explain *what it is* and *why it matters* before naming and stacking terms.
- **Prefer positive statements**: say what is true and what to do; avoid long “not X / not required / do not …” sections.
- **Use paragraphs as the default**. Lists are for stable enumerations, not for carrying the whole narrative.
- **Be explicit about real uncertainty**: if something materially affects the conclusion or next step, put it in a short `待确认 / 未验证` section; otherwise omit that section. Do not pad the note with low-value caveats.
- **Keep the tone neutral**: factual and calm. Avoid self-judgment, hype, or conversational filler.
- **No secrets**: never include real tokens, passwords, private keys, or other sensitive identifiers. Use placeholders and explain how to obtain them.
- **Default to an impersonal note voice**: avoid first-person “我…”, avoid second-person “你…”, avoid “讲稿腔” rhetorical lines. Use concise, subjectless phrasing when it reads naturally.

## Avoid

- Machine-translation tone (“因此…从而…进而…即可…” stacked heavily).
- Term dumps (dense noun phrases without explanation).
- Endless short bullets with no topic sentence.
- Over-defensive writing (too many caveats, “不得擅自”, “必须”, “禁止”).
- Document/spec voice by default (e.g. “本文档/本节/上述/如下/目的/作用/必须/不得”), unless the user explicitly wants a formal spec/manual.
- “Headings with annotations” by default (e.g. `（先讲明白）`, `（可选）` as part of the heading). Prefer plain headings; put guidance in the content if needed.
- Lecture/script stage directions by default (e.g. “想象一下/我们来看看/下面将/先…再…”), unless the user explicitly wants a tutorial tone.
- Awkward narrator phrases like “我想/我觉得/我需要…”.

## Practical heuristics

- Each section starts with **1–3 sentences** that tell the reader what this section is about.
- If a list exceeds ~7 bullets, consider:
  - splitting into multiple sub-sections, or
  - converting it into prose with a small table/list for only the critical items.
- Introduce a new term with a **two-step**:
  1. One sentence on its role (“它用来解决什么/表示什么”)
  2. Then the formal name/definition

## Micro rewrite rules

- Keep sentences short: one sentence carries one main relation (cause/contrast/condition).
- Avoid stacking connectors: do not chain many “因此/从而/进而/即可/同时/此外” in a row.
- Prefer direct verbs: avoid heavy nominalizations like “对…进行…/实现…/完成…的过程” when a verb works.

## Default stance

- Write as a standalone note: clear terms on first use, minimal implicit context, readable if sent to someone else.
- Still keep it note-like: not a manual, not a checklist dump; keep “声明/限制/不确定”内容短而必要。

## Formatting defaults

- Prefer `# Title` then `##` sections.
- Code/commands must be in fenced blocks with language hints (`bash`, `pwsh`, `ini`, `yaml`).
- Prefer “small runnable chunks” over huge dumps.
- Use inline code for identifiers (`ssh`, `~/.ssh/config`, `git config`).
