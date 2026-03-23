---
name: personal-markdown-note-writer
description: 整理多轮讨论/草稿/摘录/命令片段为长期可用的中文 Markdown 个人笔记（默认写到用户指定输出路径），区分学习笔记与工具/配置笔记；默认 synthesis：先落盘结论，再补必要背景，不写对话元信息。
---

# Personal Markdown Note Writer

## Overview

Use this skill to turn messy material (chat notes, bullet points, excerpts, partial drafts, commands) into Markdown notes that are:

- Natural to read (no "chat summary" framing, no machine-translation tone)
- Useful later (clear structure, clear scope, easy to extend)
- Fit-for-purpose (learning notes vs. tool/setup notes)

This skill is for **personal knowledge notes**, not for writing agent handoff specs or development process docs.

## Workflow

### 1. Confirm the output target early

- Default to writing directly to a **user-provided output file path**.
- If the user did not provide an output path, ask for it first. If the user explicitly wants chat-only output, output Markdown in the response and do not write files.
- Write to the requested output file only; do not create additional files unless the user explicitly asks.
- If the target file already exists, ask before overwriting.
- If updating an existing note, preserve the existing structure and user edits; prefer a small patch unless the user explicitly wants a full rewrite.

### 2. Classify the note before writing

Decide the note type and tone first. If unclear, ask one short question instead of guessing.

- `learning-note`:
  - Audience default: complete beginner (Feynman-style explanation)
  - Goal: understand, remember, and teach back
- `tool-note`:
  - Audience default: future you, in a hurry
  - Goal: reproduce a working setup in minutes

Tone default:

- Neutral, standalone, and readable without this thread.
- Avoid private shorthand; assume the note could be shared and still make sense.

Voice default:

- Prefer an **impersonal note voice** by default (avoid first-person “我…”, avoid second-person “你…”, avoid lecture/script tone).
- If the user explicitly wants a tutorial/teaching style, switch voice accordingly.

Writing mode (source-of-truth):

- **Synthesis mode (default when a discussion exists)**: if this thread already contains multi-turn discussion/corrections, or the user provides a multi-turn discussion, draft notes, or an agreed decision list, treat that material as the source of truth. Write the agreed conclusions first, then smooth for coherence. Only add minimal background to make the note readable; do not introduce new technical conclusions/decisions beyond the source material. If you find something that may be wrong or missing, put it under `待确认 / 未验证` (or ask).
- **Open-ended mode**: if the user only provides a topic prompt (no prior discussion material), write a beginner-friendly note by default. Keep assumptions explicit, and include at least one complete toy example to make the mechanism feel concrete.

Depth calibration:

- Use the user's expressed understanding to allocate explanation budget (e.g. “知道大概但不熟悉注意力” => expand attention; keep known parts short).

Read templates and rules:

- Read the matching template only:
  - Learning note template: [references/learning-note.md](references/learning-note.md)
  - Tool note template: [references/tool-note.md](references/tool-note.md)
- Always read style rules: [references/style-rules.md](references/style-rules.md)
- Read synthesis mode only when a prior discussion exists: [references/synthesis-mode.md](references/synthesis-mode.md)

Stop-and-ask conditions:

- If writing a `tool-note` and OS/shell affects the commands but is not specified, ask before drafting steps.
- If writing a `tool-note` and execution location (local vs remote vs container/WSL), required working directory, or required privilege level affects the commands but is not specified, ask before drafting steps.
- If steps involve destructive/system-level changes and the scope is unclear (deletions, registry edits, broad permission changes, overwriting critical configs), ask before writing commands.
- If the discussion contains materially conflicting conclusions, ask which is final; otherwise record both under `待确认 / 未验证`.

### 3. Split when the content has multiple intents

If the input mixes multiple distinct intents, separate them clearly instead of forcing one overlong note.

Default split behavior:

- Keep a single output file by default: split as multiple top-level sections in one Markdown file.
- Only split into multiple files if the user explicitly asks for multiple outputs.

Common split triggers:

- Theory/explanation mixed with project-specific reverse engineering
- Hardware/algorithm fundamentals mixed with GUI call chains and function lists
- One note tries to serve both "teach a beginner" and "copy-paste config steps"

Read: [references/splitting-and-scope.md](references/splitting-and-scope.md)

### 4. Extract stable facts vs. “to be confirmed”

When drafting, separate content into:

- Confirmed conclusions (write as statements)
- Supporting explanation (why it works, intuition, derivation)
- Steps/commands (tool notes)
- Examples (learning notes)
- Open questions / unknowns (if any, use an explicit `待确认 / 未验证` section; omit if none)
- Secrets / sensitive data: never include real tokens, passwords, private keys. Redact if present.

Never present unknowns as settled. Do not bury uncertainty inside confident prose.

### 5. Draft using the right template, then do a quality pass

Use the appropriate template. After drafting:

- Remove chat meta (no “本次对话/我们讨论/用户提到/如下整理”)
- Reduce defensive/exclusion-heavy language
- Make headings do the organizing, not endless short lists
- Keep only the sections that help this note; do not force the full template if it makes the note read like a manual.
- Ensure commands are “specific but not overfit”
- Rewrite once for voice: remove first-person/second-person phrasing and “script” tone; keep it note-like.
- Do not ship the first draft: run the quality checklist and revise at least once before writing the final file.
- When internet is available, do a proactive web scan for: correctness checks, better examples, and commonly agreed terminology. Do an aggressive sweep if helpful, and prefer official/primary sources for factual claims. Treat it as material gathering: rewrite explanatory prose in your own words and do not paste long chunks. Verbatim copy is reserved for reproducibility literals (commands/config/flags/error text/version IDs). If you must quote prose, keep it clearly marked, attributed, and short (<= 25 words per source). If a web scan contradicts agreed conclusions in synthesis mode, do not silently replace them; ask or record as `待确认`. When web scan is used, include 2–5 links under `参考` (each with a one-line “用于：…” note).

Read:

- Tool command guidance (tool notes only): [references/tool-command-rules.md](references/tool-command-rules.md)
- Final checklist: [references/quality-checklist.md](references/quality-checklist.md)

## Execution Boundaries

When executing this skill in a real workspace:

- Only read/write files that are clearly in-scope for the requested note output.
- Writing to the explicit user-provided output path is in-scope even if it is outside the current repo/workspace. Avoid touching other files in the same folder unless requested.
- Do not modify unrelated notes or reorganize vaults/repos without explicit request.
- Do not install global tools, change system configuration, or perform destructive actions unless the user explicitly asks.

## Response Expectations

When writing or updating a note:

- Produce Chinese Markdown by default (unless the user asked otherwise).
- Write to the user-provided output path (or ask for it if missing).
- Keep the note human-readable: use paragraphs, explain terms, avoid glossary-like dumping.
- Keep the note useful: include “how to verify” for tool notes, and “one-sentence teach-back” for learning notes.
- Be neutral and factual; avoid interpersonal/meta framing.
