# C++ Comment Style

## Scope

Apply to comments in C++ source and headers. Test first-line comments follow
[test-style.md](test-style.md) for content and this reference for mechanical
format. Preserve an existing user-authored comment when it remains true and
readable; do not rewrite it merely for stylistic uniformity. Fix a comment that
the current behavior change makes false, and report uncertainty about a
user-authored comment instead of silently rewriting it.

Source comments use zh-CN unless a stronger project rule explicitly chooses
another language. Runtime-visible text is not a source comment and remains
English under the main skill.

## Commenting Stance

Write for a maintainer who understands ordinary C++ and can read nearby code,
but does not automatically know the current module, domain model, pipeline,
task discussion, or design history.

A comment supplies what the signature, type, names, and applicable surrounding
context cannot. First cover the contract or component model the declaration
area must carry. Then remove information the surrounding context already makes
clear. Complete means enough to understand, use, and maintain the code in
context; it does not mean proving that no misuse is possible.

Readable, idiomatic Chinese is required. Establish the facts and structure
first, then write as a fluent Chinese-speaking maintainer would explain them.
Use direct sentences and established terms. Preserve every contract fact and
mechanical rule while polishing. A phrase from the signature may also be the
most natural description; use it when it contributes needed meaning.

## Hard Checklist

For header and non-test source comments, apply items 1–11. Item 12 applies to
every source comment, including test first-line comments.
This is the executable checklist; the sections below explain its application.

1. Model the reader above. A public API caller reads declarations without
   implementation knowledge.
2. Use the applicable limiting context. A public comment may rely on its public
   namespace, type, declaration, and adjacent public comments, but not on
   implementation. An internal comment may also rely on adjacent implementation.
3. For a non-obvious type or module-facing operation, make the declaration area
   establish what the component is, what it produces or changes, and why that
   result exists. Internal headers may include the stable pipeline role or
   consumer; public headers express only caller-visible purpose and use.
   A complex or special type establishes its use model in the opening paragraph.
4. After the required contract and model are covered, keep only maintenance
   information that the context does not already carry. Omit the comment when
   none remains.
5. Draft a public API top-down: caller-visible role or transformation first,
   remaining observable contract in the correct Doxygen tags, then reread it as
   a caller and rewrite it as natural Chinese.
6. Describe the current symbol and stable system role, not the task, prompt,
   spec wording, phase, patch, review history, or incidental call sequence. Do
   not import pseudocode terms unless they are established project or domain
   concepts. Public header comments must not use task-relative wording such as
   `这里`, `上面`, `下面`, `本次`, or `后续`.
7. Keep public API documentation to observable behavior, inputs, return
   meaning, ownership or lifetime, failure form, and important boundaries.
   Internal comments may explain a stable implementation model or integration
   role needed by maintainers.
   Keep the tone neutral and understandable.
8. Use implementation comments for non-obvious strategy, state transitions,
   data flow, invariants, index relationships, and boundary-preserving reasons.
   Do not translate nearby statements step by step.
   Do not write internal validation steps in checklist voice or describe
   recovery/reset procedures for states no supported path produces.
9. Keep established domain terms and acronyms stable. Prefer natural Chinese
   over copied low-value identifiers or English fragments.
10. Use enough detail for the missing model. Length is not a target: do not add
    boilerplate, and do not compress a complex explanation until it is cryptic.
11. Give every Doxygen tag its own responsibility. Do not put return meaning,
    parameter rules, or failure form into `@note`, and do not promote an ordinary
    fact into `@note` or `@warning`. Use noun-centered language for types,
    results, and fields; verbs for behavior; predicates for boolean queries.
12. Apply the mechanical format exactly:
    - Use ASCII punctuation. The enumeration mark `、` is the sole exception.
    - Follow an in-prose comma, semicolon, or colon with exactly one ASCII
      space.
    - Add no spaces at Chinese-English or Chinese-identifier boundaries.
    - Put no spaces inside or around parentheses.
    - End each logical comment line without sentence-ending punctuation. When a
      formatter wraps one sentence, keep punctuation required inside it.
    - Running prose is plain text: no backticks, emphasis, heading markers, or
      HTML tags. Doxygen lists and `@code` blocks remain available when needed.

After editing, inspect every touched `//`, `///`, and `/** */` line against this
list. Nearby comments do not override the mechanical rules even when they are
the local majority.

## Explain The Model, Not The Signature

### Prepare The Model

Before drafting a non-obvious component model, answer in order:

1. What do the declaration and nearby context already tell the maintainer?
2. What component-specific role, pipeline relation, or operating model is missing?
3. What does it produce or change, why does that result exist, and who uses it?
4. Which invariant, precondition, transition, or interpretation makes the code
   understandable?

Explain a real gap directly, even when it needs several sentences. A reader's
ability to inspect implementation does not replace the model that gives those
details meaning. Put the distilled conclusion in the comment, not the questions
or deliberation.

### Draft Public Comments In Three Passes

1. State the caller-visible operation or the type's role. For a function, think
   input -> operation -> observable result before writing the brief.
2. Place each remaining fact in the tag that owns it before considering its
   removal. Observable algorithm edge cases remain part of the contract.
3. Read the declaration as a caller without the implementation. The brief must
   not promise more than the detailed tags. Fix awkward prose by separating
   mixed tag responsibilities, then reread for natural Chinese phrasing.
   Preserve facts, tag responsibilities, and mechanical format while polishing.

For example, a resampling operation preserves endpoints and permits a shorter
final segment. This implementation-led brief makes the caller reconstruct it:

```cpp
/// @brief 按弧长参数化逐段遍历路径, 在累计弧长达到间距整数倍处线性插值生成采样点,
/// 间距不整除总弧长时末段按剩余弧长收尾, 单位为微米
ScanPath resample(ScanPath const& path, double spacing);
```

This shorter draft loses the endpoint and final-segment behavior:

```cpp
/// @brief 把路径上的点重新撒均匀
ScanPath resample(ScanPath const& path, double spacing);
```

Keep the operation, inputs, result, and failures in their respective places:

```cpp
/// @brief 按给定弧长间距重采样路径
///
/// @param spacing 目标采样间距, 单位为微米
/// @return 包含原路径起点和终点的采样路径; 除末段外, 相邻采样点间距为spacing, 末段长度不大于spacing
/// @exception std::invalid_argument spacing不是正有限值时抛出
[[nodiscard]] ScanPath resample(ScanPath const& path, double spacing);
```

The same method applies to a device setter. In this example, `Milliwatt` is the
unit type and the named exceptions are the API's public error types. This draft
describes private execution order:

```cpp
/// @brief 设置目标值; 调用时先检查ready状态, 再检查范围, 然后更新缓存并调用实现
void target(Milliwatt value);
```

State the operation, unit, and observable failure conditions instead:

```cpp
/// @brief 设置目标值
///
/// @param value 目标值, 单位为mW
/// @exception DeviceNotReadyError 设备未就绪时抛出
/// @exception DeviceControlError 值越界或设备拒绝写入时抛出
void target(Milliwatt value);
```

The caller needs these conditions; validation order, cache updates, and private
calls remain implementation details.

### Establish A Component Model

Do not restate input and output types or turn implementation order into a
contract. State the role, operating model, invariant, produced result, or
consumer relationship that a reader cannot recover cheaply.

Weak:

```cpp
/// @brief 以已排序边表为输入, 输出配对后的填充线段
class ScanlineEngine;
```

Better:

```cpp
/// @brief 扫描线填充的核心扫描循环
///
/// @details 边按下边界排序后, 扫描线沿单调方向线性推进, 而非按整数行分桶;
/// 每条扫描线对当前活动边做Even-Odd配对, 产出该行的填充线段, 逐行回调给消费者
class ScanlineEngine;
```

The second comment gives the missing algorithm model and output use. It does
not list private storage or task history.

A buffered controller needs to explain when a caller's actions take effect:

- A reader may expect a setter to act on the device immediately.
- Here it only appends to a command list; a separate execute request triggers
  the deferred, batched actions.
- The signature already shows the setters and execute method. Explain their
  operating model instead of listing those methods again.

```cpp
/// @brief 基于命令列表的控制接口
///
/// @details 调用方先写入命令列表, 再请求设备执行; 写入本身不触发硬件动作
class BufferedController;
```

An internal component may rely on upstream guarantees and explain how its
result is consumed. Use a diagram when it makes a feedback relation clearer:

```cpp
/// @brief 根据已验证的依赖关系构造任务执行顺序
///
/// @details 会话加载阶段已经保证依赖图无环; 本组件维护每个任务的剩余前驱数,
/// 将新就绪任务持续加入队列, 最终产出供执行器顺序消费的任务列表
///
/// @code
/// 已就绪任务 -> 就绪队列 -> 输出顺序
///                  |
///                  +-> 解除后继依赖 -> 新就绪任务
/// @endcode
class ExecutionOrderBuilder;
```

For an obvious operation, the name may already carry the action. Add only the
missing unit, reference frame, side effect, lifetime, or failure form:

```cpp
/// @brief 平移整条扫描路径, 坐标单位为微米
/// @exception std::invalid_argument 偏移量不是有限值时抛出
ScanPath& translate(double dx, double dy, double dz);
```

Do not add documentation to a trivial getter, setter, or predicate when the
name, signature, type, and surrounding type comment already make the behavior
complete.

## Information Placement

Keep repeated semantic explanations in one closest owner:

- type comment: what the component or result represents, carries, produces, and
  how it is used;
- field or local variant comment: the local distinction that would otherwise
  confuse maintainers;
- function comment: responsibility, inputs, result, mutation, failure, and
  caller-relevant boundary;
- implementation comment: strategy, invariant, transition, or non-obvious
  reason.

A local result type or variant explains the local semantic distinction most
likely to confuse a maintainer. When a special rule has a practical purpose,
state that effect instead of saying only that the rule exists. Keep definition,
use, result, and diagnostic roles distinct.

Define a result object's categories at their owner and let returning functions
refer to that model. Explain a component through its purpose, behavior, and
conditions; include a negative boundary only when it prevents realistic misuse.

Simple field comments use trailing `///<` by default. Use a preceding block only
when a field genuinely requires multi-line API documentation. A field comment
explains the field, not the whole enclosing type.

Use a compact ASCII diagram only when a spatial relation, feedback path, memory
layout, or pipeline is materially easier to understand visually than in one
sentence. Put a diagram in a Doxygen block inside `@code`; an ordinary
implementation comment may place it directly below its orienting sentence. Do
not add decorative diagrams.
Label the model being shown and keep the diagram local to the code it explains.

## Doxygen Tag Responsibilities

- `@brief`: one natural sentence stating the stable role, operation,
  transformation, or result in its declaration context.
- `@details`: caller-visible scope, interpretation, evaluation, coverage, or a
  maintainer model that cannot fit naturally in the brief. Internal declarations
  may explain a stable algorithm or pipeline; public declarations describe
  sequence only when it is caller-visible behavior. Keep default-behavior
  reminders, transient reminders, statement-by-statement narration, and failure
  lists out of this tag.
- `@param`: input meaning, unit, accepted range, ownership, or default semantics
  that the type and name do not already make clear.
- `@return`: result meaning, value categories, ownership, and observable
  boundaries.
- `@exception`: the stable direct failure type and trigger condition. Do not
  enumerate incidental allocator, container, or transitive implementation
  failures.
- `@note`: an important, non-obvious reminder that does not belong to another
  tag, such as a material thread-safety, lifetime, stability, performance, or
  common-assumption boundary. It is not overflow space.
- `@warning`: a condition whose omission is likely to cause dangerous or serious
  misuse. Use `@note` or ordinary prose for normal boundaries.

Do not make an exhaustive tag set a goal. Use only tags that carry needed
information.

For a stream operation, distinguish the result from failure and configuration:

```cpp
/// @return 已成功读取字节的哈希摘要; 若读取到文件末尾, 则为完整内容摘要
/// @exception std::ios_base::failure 由std::istream触发, 是否抛出取决于输入流设置
/// @note 不修改is.exceptions(), 也不清除已有状态位; eofbit、failbit、badbit的设置行为与流配置一致
/// @note 若流不抛异常, 则本函数也不因读取失败而抛出; 返回的是"成功读取部分"的摘要
```

## Natural Chinese

- Prefer direct verbs and predicates over `对...进行...` and stacked abstract
  nouns.
- Keep professional domain terminology, but do not invent formal-sounding terms
  when ordinary wording is precise.
- Interpret an ambiguous English identifier through its algorithmic or domain
  role, not a dictionary gloss. If the role is unclear, retain the established
  domain term or rewrite the sentence.
- Do not repeat a type name as its explanation, such as `表示ASTNode类型`.
- Use noun-centered wording for a result and direct verbs for an operation.
- For repository prose and source comments, use a soft target of roughly 80
  ASCII columns when clauses wrap naturally. Keep a sentence or clause together
  when splitting harms readability; code, paths, identifiers, tables, tags,
  and diagrams may run longer. Do not split a sentence merely to even out line
  lengths or move facts between Doxygen tags to fit a line budget.

### Short Types And Natural Terms

A simple type may need only its role and one essential unit:

```cpp
/// @brief 可注入的时间提供者, 返回当前UNIX时间戳(秒)
struct TimeProvider;
```

Use a predicate for a boolean query: `模块是否有效`. Prefer `汇总当前检查结果`
to `汇总当前阶段产物的语义一致性状态`, and `AST的基本节点类型` to
`表示ASTNode类型`.

Keep established domain acronyms while replacing fragmented English prose:

```cpp
/// @brief per-channel设置carrier frequency
void frequency(Channel channel, Megahertz value);
```

```cpp
/// @brief 按通道设置RF频率
void frequency(Channel channel, Megahertz value);
```

### Result Identity And Local Detail

This names storage categories without explaining the result:

```cpp
/// @brief 按内部分类列表汇总结果, 包含若干已解析项、失败项与待处理项
struct ResolveResult;
```

State its meaning and use:

```cpp
/// @brief 引用解析产生的可用目标和诊断
///
/// @details 调用方使用可用目标继续构建依赖关系, 并集中报告无法解析的引用
struct ResolveResult;
```

With those categories owned by the result, this function comment repeats them:

```cpp
/// @brief 解析引用并返回结果; 成功项写入resolved, 失败项写入errors, 待后续处理项写入unresolved
ResolveResult analyzeReferences(Input const& input);
```

The function's responsibility is sufficient:

```cpp
/// @brief 解析当前输入中的引用并返回结果
ResolveResult analyzeReferences(Input const& input);
```

For a special retention rule, `该情况按既定规则继续保留旧记录` only restates
the rule. `继续保留已有结果, 避免后续诊断被级联噪声淹没` explains its purpose.
