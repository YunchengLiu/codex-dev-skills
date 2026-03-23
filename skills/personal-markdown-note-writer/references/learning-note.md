# Learning Note Template (Feynman-Style)

Default audience: infer from the material; if unclear, assume a complete beginner.

## Template

Treat this as a section menu, not a mandatory outline. Keep the opening paragraph, the core conclusions, and at least one complete example; keep the other sections only when they materially help the note read naturally.

```md
# <Title>

<开头用 2–4 句短段落说明：这是什么，解决什么问题；避免“你想…/你需要…/一句话概括…”这类口吻。>

## 结论
<写下已确定的核心结论（1–5 条）。synthesis mode 必填；open-ended 可略。>

## 使用场景
<可选：1–3 条具体场景：遇到什么问题 -> 用它能解决什么/解释什么。>

## 前置概念
<可选：最多 5 行。只写真正必要的前置概念，不要铺背景史。>

## 直觉与机制
<先从一个具体困惑/例句/小问题起步；给出一个朴素但不够好的方案，再引出核心机制。尽量让读者“跟着走”，而不是直接下定义。>

## 形式化
<可选：没有就删掉本节。公式、推导、边界条件、假设。若出现公式/符号，必须解释每个变量的含义/单位，并写清适用条件或假设。>

## 例子 / 推演
<至少 1 个完整玩具例子：从“分数 -> softmax 权重 -> 加权和”走通一遍。优先用小句子/小表格表达；必要时再补 3 个数的数值例子。>

## 常见误解
<可选：只有确实常见、而且一句话能澄清时再写。>
- <误解 1：一句话反驳或澄清>
- <误解 2：...>

## 一句话复述
<必填：用 1 句写下最短可复述版本（teach-back）。>

## 待确认 / 未验证
<可选：没有就删掉本节。>
- <不确定点 + 需要什么证据/下一步怎么验证>

## 参考
<可选：没有就删掉本节。做过 web scan/查资料时放 2–5 条。每条链接加一句“用于：…”，避免 URL dump。>
- [<Title>](<URL>) — 用于：<术语定义/事实核对/示例来源>
```

## Writing rules

- Start from the mental model. Terms come after.
- For beginner-friendliness, prefer: example -> intuition -> minimal math (optional) -> recap.
- When a prior discussion exists (synthesis mode): treat the agreed conclusions as the source of truth; write conclusions first, then smooth for coherence. Only add minimal background for readability; do not introduce new technical conclusions/decisions beyond the source material unless web scan suggests a material correction and the user confirms updating the conclusion. Put potential corrections or missing pieces under `待确认 / 未验证` (or ask).
- Calibrate depth to the user's current understanding shown in the discussion (expand the real gaps; keep the rest short).
- If there are multiple subtopics, keep the main note focused. By default, separate them as top-level sections in the same file instead of forcing one giant uninterrupted explanation.
- If the note includes project-specific details, either:
  - move them to a separate top-level section in the same file, or
  - clearly label them as “特定项目背景” so the learning part stays reusable.

## Example (Short)

This is a small example of the desired tone and shape (not a mandatory outline):

```md
# Softmax：把“分数”变成“权重”

Softmax 解决的是同一组候选里“谁更重要”的分配问题：把一串任意实数分数，变成一串非负、和为 1 的权重。权重越大，表示这个候选在后续加权汇总里占比越高。

## 结论

- Softmax 输出可解释为一组权重：每个值在 0 到 1 之间，且总和为 1。
- 分数差距越大，softmax 的权重差距会被放大；分数差距越小，权重更平均。

## 直觉与机制

直接把分数当权重的问题是：可能出现负数，也不会自然归一化。Softmax 的做法是先把分数过一遍指数函数，让它们变成正数，再除以总和完成归一化。

## 例子 / 推演

分数：`[2, 1, 0]`

1. 指数：`[e^2, e^1, e^0] ≈ [7.39, 2.72, 1.00]`
2. 求和：`7.39 + 2.72 + 1.00 = 11.11`
3. 归一化：`[0.665, 0.245, 0.090]`

这组权重就可以用于加权平均或注意力的加权和。

## 一句话复述

Softmax 把任意分数变成一组可解释为“占比”的权重。
```
