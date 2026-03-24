---
name: personal-markdown-note-writer
description: 个人知识笔记整理：把多轮讨论、零散想法、草稿、摘录、命令片段整理成长期可用的中文 Markdown 个人笔记（学习笔记 + 工具/配置记录，写到用户指定输出路径）；默认 synthesis：先落盘已达成的结论，再补必要背景，不写对话元信息，重点是归档和澄清已有材料，让笔记自然、独立、可回看。
---

# Personal Markdown Note Writer

## Intent

Turn messy material (chat notes, bullet points, excerpts, partial drafts, commands) into **long-lived Chinese Markdown personal knowledge notes**:

- `learning-note`: understanding + at least one complete toy example + one-sentence teach-back
- `tool-note`: runnable steps/commands + environment + verification

Default to grounded synthesis from the provided material: preserve the user's thread of thought, surface agreed conclusions first, and add only the background needed to make the note self-contained and reusable later.

This skill is for personal notes, not for repo docs, specs, handoffs, or process docs.
Default bar: reads like a human note (paragraph-first, minimal form/checklist vibe). Unknowns go to `待确认 / 未验证`, not confident prose.

## Workflow

### 1. Output Target

- Prefer writing directly to a **user-provided output file path**.
- If missing, ask one short question (path or “聊天输出”). Do not invent a default path.
- Write to the requested file only. If it exists: if the user intent is update/append/merge, apply a patch; otherwise ask before overwriting.

### 2. Pick note type and mode

- Type: `learning-note` vs `tool-note`. If unclear, ask one short question.
- Mode:
  - Synthesis: when there is prior discussion/corrections. Treat it as the source of truth and write the agreed conclusions first.
  - Open-ended: when the user provides a topic together with some seed material, direction, or provisional conclusions. Keep assumptions explicit.
- If the user provides only a bare topic with no prior discussion, notes, excerpts, or conclusions, ask for the minimum source material before drafting.
- Depth: infer the user's level from the material; expand real gaps, keep the rest short.

### 3. Draft with templates, then revise once

- Use the matching template:
  - Learning: [references/learning-note.md](references/learning-note.md)
  - Tool: [references/tool-note.md](references/tool-note.md)
- Always follow style rules: [references/style-rules.md](references/style-rules.md)
- If content mixes intents, split into top-level sections; read: [references/splitting-and-scope.md](references/splitting-and-scope.md)
- Tool notes: follow command rules (includes stop-and-ask + safety): [references/tool-command-rules.md](references/tool-command-rules.md)
- Start from the provided material and prior discussion. Only widen the view with web scan when the user asks for it; if new information would change an agreed conclusion, pause and confirm. Follow: [references/synthesis-mode.md](references/synthesis-mode.md)
- Run the final checklist and revise at least once before writing: [references/quality-checklist.md](references/quality-checklist.md)
