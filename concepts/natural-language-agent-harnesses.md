---
title: Natural-Language Agent Harnesses
created: 2026-04-15
updated: 2026-04-15
type: concept
tags: [concept, harness-engineering, workflow, best-practice, open-source]
sources: [raw/articles/carlos-e-perez-x-post-2042565202357420542-2026-04-14.md, raw/articles/nlah-arxiv-abs-2603-25723-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md]
---

# Natural-Language Agent Harnesses

## 定义
Natural-Language Agent Harnesses（NLAHs）是一种把 agent harness 的高层控制逻辑外化为可编辑自然语言工件的做法。它不试图用自然语言替代所有确定性代码，而是把 contracts、roles、stages、state semantics、adapters、scripts 和 failure taxonomy 这些“设计模式层”从控制器代码里抽出来，变成可执行、可迁移、可消融、可比较的文本对象。

## 这篇论文要解决什么问题
论文抓得很准：很多 agent 系统真正决定成败的不是底模，而是 harness。但现实里的 harness 往往被埋在 scattered controller code、prompt、runtime assumptions 和 framework-specific conventions 里，结果就是：
- 很难比较不同 agent 到底差在模型还是 harness
- 很难迁移一套 harness 到新 benchmark / 新任务
- 很难把 harness 当成可研究、可优化的对象

NLAH 的核心主张是：把 harness 的 pattern layer 显式外化出来。

## 核心结构
- NLAH：承载高层 harness 逻辑的自然语言工件
- [[intelligent-harness-runtime]]：共享运行时，负责解释和执行 NLAH
- file-backed state：把关键状态写入 artifacts，而不是只留在 transient context 中

论文里明确强调，自然语言负责的是可编辑 orchestration logic；真正低层、确定性的动作仍由 adapters、scripts、tests、linters、verifiers 等钩子承担。

## 这篇论文补出的几个关键点
### 1. Harness 可以被当作“可研究对象”
这篇论文最大的价值，不是又发明一个 runtime，而是把 harness 从“隐形胶水层”变成了可单独比较的对象。它让 harness engineering 更像一门工程科学，而不只是经验主义手艺活。

### 2. 更容易做模块级消融
论文把 harness pattern 拆成可显式增删的模块，例如：
- self-evolution
- file-backed state
- evidence-backed answering
- verifier
- multi-candidate search
- dynamic orchestration

这让 [[harness-engineering]] 首次能在 shared runtime 下做更接近 apples-to-apples 的 pattern ablation。

### 3. 更容易做 code-to-text migration
论文里最有传播力的结果，就是把 code harness 迁成 NLAH 后，在 OSWorld 的 paired setup 里拿到了 47.2 vs 30.4 的结果。更重要的不是这个数字本身，而是作者解释的机制：迁移后的 harness 更偏 contract-first、artifact-backed closure，而不是停留在 implicit context juggling。

### 4. 更强调 file-backed state 与 artifact-backed closure
NLAH 不是“把 prompt 写长一点”。它的一个关键落点是：把关键状态写到 path-addressable、compaction-stable 的 artifacts 里，让系统在 truncation、restart、delegation 后还能续跑。这和 [[agent-memory-patterns]]、[[agent-readable-repositories]]、[[context-engineering]] 都高度同向。

## 我对这条路线的判断
我认可它的研究价值，但也不完全买账它的全部叙事。

### 我认可的部分
- 它确实把 harness externalization 往前推了一步。
- 它让 harness 可以被迁移、比较、消融，而不是永远锁在框架源码里。
- 它非常适合补强我们库里一直在讲的：rules / contracts / markdown brains / file-backed state / explicit artifacts。

### 我保留意见的部分
- 自然语言并不天然等于更稳。它更 editable，但未必更 precise。
- shared runtime 也可能重新形成新的“隐形 charter behavior”，只是把不透明性从 framework 源码挪到了 runtime charter。
- 论文当前仍是研究样本与 subset benchmark 结果，不是普适生产结论。

所以我更倾向把 NLAH 定位为：
- 一个很强的 harness externalization 研究路线
- 一个值得工程借鉴的 pattern language
- 但还不是已经证明自己能替代主流 production harness 的行业标准

## 在当前知识库中的位置
- [[harness-engineering]]：它把 harness 进一步从“实践黑话”推成可研究对象。
- [[agent-readable-repositories]]：它说明文本工件不只是文档，而可以承载可执行 control logic。
- [[agent-memory-patterns]]：它强调 file-backed state 与 explicit artifacts 对长期任务的重要性。
- [[context-engineering]]：它把 context、contracts、artifacts 和 runtime charter 组合成一套更外显的控制面。

## 来源
- [[carlos-e-perez-x-post-2042565202357420542-2026-04-14]]
- [[nlah-arxiv-abs-2603-25723-2026-04-15]]
- [[nlah-arxiv-html-2603-25723-2026-04-15]]
