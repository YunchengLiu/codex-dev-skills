# Tool / Setup Note Template

Goal: reproduce a working setup quickly later.

## Template

Treat this as a section menu, not a mandatory outline. Keep the note short and runnable. If a section adds ceremony but no value, drop it.

```md
# <Title>

## 目标
<这篇笔记要解决什么问题，一句话即可>

## 要点
<2–5 行：推荐做法/关键选择/踩坑提醒；让人不看步骤也能知道“最后应该怎么做、为什么这么做”。>

## 环境
<OS + shell>；执行位置：<本机/远程/容器/WSL>；工作目录：<...>；关键版本点：<仅写确认重要的版本点>

## 前提
<可选：只写真正会影响成功率的前提，最多 3 条。若某个权限/依赖只影响某一步，优先写在那一步附近，不要单独扩成“注意事项”小节。>
- <依赖/已有文件/网络条件等>

## 参数/变量
<可选：集中解释占位符/变量。没有占位符就删掉本节。>
- <HOST>: <如何确定它>
- <PATH>: <如何确定它（绝对路径或相对于工作目录；含空格需引号）>

## 步骤
<推荐路径：按顺序写未来最常用的一条路径。>
1. <Step 1>
2. <Step 2>
3. <Step 3>

<若步骤需要在特定远程主机/容器或特定工作目录执行，先单独写明执行位置与工作目录。>
<若某一步不自解释，在该步后追加 1 行说明“做什么/为什么”。>
<若需要同时支持多个环境，不要把命令混写在同一组步骤里；按环境拆成独立小节。>

## 验证
- <如何确认配置成功（最好包含期望输出/成功判据）>

## 常见问题
<可选：只有确实高频、而且能一句话说清时再写。>
- <症状 -> 原因 -> 解决>

## 可选变体
<可选：没有就删掉本节。仅在确实常用且稳定时添加。>
- <变体：什么时候用 + 怎么改>

## 回滚 / 清理
<可选：没有就删掉本节。如何撤销关键改动；如果不建议撤销就写“不建议/不适用”。>

## 待确认 / 未验证
<可选：没有就删掉本节。>
- <不确定点 + 下一步>

## 参考
<可选：没有就删掉本节。做过 web scan/查资料时，放 2–5 条未来可能会回看的链接。每条链接加一句“用于：…”，避免 URL dump。>
- [<Title>](<URL>) — 用于：<术语定义/事实核对/示例来源>
```

## What “good” looks like

- Steps are copy-pasteable.
- Each step is minimal but complete (no missing prerequisites).
- Includes at least one verification method.
- Commands are specific but not overfit.
- Permission or environment caveats are kept close to the relevant step instead of turning the note into a warning list.
- If there is prior discussion material, the “recommended path” should follow the agreed setup and choices instead of introducing new variants.

## Example (Short)

```md
# Windows 上给 Git 配置 HTTP(S) 代理（PowerShell）

## 目标

让 `git clone/pull` 走代理并可随时回滚。

## 要点

- 只改 Git 的 proxy 配置，不改系统代理。
- 优先用 `http.proxy` / `https.proxy`；不用时一键 unset。

## 环境

Windows；PowerShell；执行位置：本机；工作目录：任意。

## 参数/变量

- `<PROXY>`: 形如 `http://127.0.0.1:7890`

## 步骤

1. 设置代理

```pwsh
git config --global http.proxy "<PROXY>"
git config --global https.proxy "<PROXY>"
```

2. 验证（查看当前配置）

```pwsh
git config --global --get http.proxy
git config --global --get https.proxy
```

## 回滚 / 清理

```pwsh
git config --global --unset http.proxy
git config --global --unset https.proxy
```
```
