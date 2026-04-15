---
title: What NLAH RQ2 and RQ3 Actually Show
created: 2026-04-15
updated: 2026-04-15
type: query
tags: [query-note, harness-engineering, workflow, best-practice, benchmark, reliability]
sources: [raw/articles/carlos-e-perez-x-post-2042565202357420542-2026-04-14.md, raw/articles/nlah-arxiv-abs-2603-25723-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md]
---

# What NLAH RQ2 and RQ3 Actually Show

## 问题
NLAH 论文里最值得工程上认真读的，不是概念定义，而是 RQ2（模块消融）和 RQ3（code-to-text migration）。那这两部分到底说明了什么？

## 短答案
如果把论文里最花哨的叙事都去掉，RQ2 和 RQ3 真正说明了 4 件事：

1. 不是“结构越多越好”，而是“结构是否更贴近最终 evaluator 的接受条件”
2. self-evolution 是少数既有效又相对不重的模块
3. file-backed state / evidence-backed answering 更像 process-structure 增强器，而不是万能提分器
4. code harness 迁成 NLAH 后，最大变化不是语言形式，而是系统从 implicit context juggling 转向 contract-first + artifact-backed closure

## 一、先说 RQ2：模块消融到底在测什么
论文的 RQ2 不是在问“哪种模块最酷”，而是在问：
- 一旦 harness pattern 被显式化
- 它能不能像模块一样被组合、拆掉、单独测试

在 SWE 侧，他们从一个更 bare 的 Basic 条件开始，逐步加：
- file-backed state
- evidence-backed answering
- verifier
- self-evolution
- multi-candidate search
- dynamic orchestration

在 OSWorld 侧，Basic 本身已经是结构化 harness，所以这些模块是在一个更“像系统”的基础上继续叠加。

### 真正的核心发现
论文明确说了：
- 模块影响主要集中在一个小的 solved frontier 上
- 大多数任务并不会因为某个模块就整体翻盘
- 所以 RQ2 更像是在研究“哪些模块会改写边界样本”，而不是给模块排一个简单总分榜

这点很重要，因为它直接反驳了很多 agent 圈常见误解：
- 不是加一个 verifier 就普遍更稳
- 不是上 multi-candidate 就必然 frontier expansion
- 不是 orchestration 更复杂就一定更强

## 二、RQ2 对各模块真正给出的判断

### 1. Self-evolution：目前最像“有效增强器”的模块
论文给得最正面的，是 self-evolution。

作者的关键判断不是“它会开放式反思”，而是：
- 它会把 solve loop 收紧成 acceptance-gated attempt loop
- 让系统先把一次修复做干净
- 而不是过早扩成昂贵搜索树

也就是说，self-evolution 的价值不是增加想象力，而是提高修复回合的纪律性。

我对这个点的理解是：
- 它本质上更接近 [[agent-feedback-loops]] 的 loop tightening
- 而不是“agent 自我意识增强”那种玄学叙事

所以如果你问“什么模块最值得先借鉴”，我会优先看 self-evolution 的 acceptance-gated retry discipline，而不是先看大规模 candidate branching。

### 2. File-backed state：不是暴力提分器，而是状态续接器
file-backed state 在论文里不是零作用，但它带来的更像：
- 更清晰的 child handoff
- 更稳定的 artifact lineage
- 更 explicit 的 task history / manifest spine

换句话说，它优先改善的是：
- state continuity
- artifact discipline
- path-addressable recovery

而不是简单“分数暴涨”。

这和我们库里的 [[agent-memory-patterns]]、[[agent-readable-repositories]] 非常一致：
- 外部化状态首先改善的是系统稳定性与续跑性
- 不一定立刻让 benchmark 分数飞升

### 3. Evidence-backed answering：帮助收紧 release discipline
这类模块在论文里同样不是“普遍提分神器”。
它更像是：
- 强迫系统留下 standalone analysis artifact
- 把 patch、观察、根因推理、验证证据串起来

所以它最像什么？
我觉得它最像一种更强的 [[agent-feedback-loops]] + [[agent-observability]] 落盘版本。

### 4. Verifier：有价值，但极容易“局部正确、全局失焦”
这可能是 RQ2 最值得工程团队记住的一条。

论文没有说 verifier 没用。
论文说的是：
- verifier 在“局部 acceptance object”与“benchmark 最终 acceptance gate”足够接近时，会很有帮助
- 但只要两者错位，它就会制造一种危险状态：系统更结构化、更会解释自己，但最后还是错

这和我们之前库里的 [[evaluator-driven-qa]] 其实完全同向：
- evaluator 最大的风险不是没有判断
- 而是它判断的对象，跟真正的完成标准不一致

所以 verifier 的难点从来不是“要不要有独立评估者”，而是：
- verifier 在验证什么
- 这个验证对象和最终 evaluator 是否同构

### 5. Multi-candidate search：最容易被高估
论文对它相当不客气。
结论基本是：
- 搜索行为确实更 visible
- 但在当前 runtime / budget 下，开销太重
- 很容易成为 dominated choice

一句人话：
- 它更像“昂贵但不稳定的 solved-set replacer”
- 而不是一个可靠的 frontier expander

这跟很多团队的直觉相反。很多人默认“多候选 = 更强”，但论文更像在说：
- 如果 acceptance gate 没对齐
- 如果状态管理没跟上
- 如果 verifier 逻辑不靠谱
那你只是更贵地乱试。

### 6. Dynamic orchestration：行为真实，但常常只是换解集，不是扩前沿
论文对 dynamic orchestration 的描述很克制：
- 它不是 inert
- 它确实会改变哪些样本被解出
- 但很多时候只是 solved-set replacer，不是明显 frontier expansion

这点对 [[multi-agent-delegation]] 很有提醒意义：
- delegation / orchestration 的价值，不该默认按“更多 agent = 更强”理解
- 更准确的理解是：它可能在换边界样本，不一定在整体抬升上限

## 三、RQ2 最重要的总判断
如果要把 RQ2 收成一句最值钱的话，我会写成：

“more structure is not always better; explicit modules only help when they tighten the path from intermediate behavior to the evaluator’s actual acceptance condition.”

翻成人话：
- 结构本身不是价值
- 结构与最终验收对象的对齐，才是价值

这点非常值得写回我们整个 wiki，因为它几乎能解释一半 agent harness 失败案例：
- 系统不是不复杂
- 系统是复杂得不对齐

## 四、再说 RQ3：code-to-text migration 真正说明了什么
RQ3 是 paired migration study：
- 原始 code harness
- 重建成 NLAH 后在 shared runtime 下运行

最容易传播的是那个数字：
- OSWorld 上 47.2 vs 30.4

但我觉得论文自己讲得更对：
- 更重要的差异是 behavioral，而不是 purely numerical

### 迁移后到底变了什么
作者的关键判断是：
- native code harness 更像 screenshot-grounded repair loop
- migrated NLAH 更像 contract-first runtime flow
- state 更明确地住在 task files、ledgers、artifacts 中

也就是说，变化不是“自然语言神奇更聪明”
而是：
- 隐式控制逻辑被外显了
- 完成标准更 contract-first
- closure 更依赖 artifact-backed evidence

### 这个结果真正支持什么，不支持什么
它支持：
- harness externalization 可能真的会改变行为结构
- artifact-backed closure 在 computer-use 任务里可能比视觉 plausibility 更稳
- file-backed state + explicit contracts 可能显著改善 recovery / closure

它不支持：
- “自然语言一定优于代码”
- “任何 code harness 迁成文本都能涨分”
- “NLAH 已经是生产标准”

## 五、我对 RQ3 的工程解读
我觉得 RQ3 最值得借鉴的不是“迁成自然语言”，而是下面这三条：

### 1. Contract-first closure 比感觉式 closure 更稳
很多 agent 任务最后失败，不是前面不会做，而是最后停错了。

NLAH 迁移后的优势，很多来自：
- 它要求系统留下更明确的完成证据
- 而不是看起来差不多就停

### 2. Artifact-backed state 对长任务非常重要
这再次证明：
- state 不该只活在 transient context
- 要写到 path-addressable artifact 里

这和我们现有的 [[agent-memory-patterns]] 基本完全吻合。

### 3. Observability density 增加，不等于动作更多
论文明确提醒：
- 迁移后日志更密，不代表动作就更多
- 可能只是 bookkeeping、started/completed pairs、artifact handling 更显式

这点对读 traces 很关键。
否则很容易误判成：
- “系统更复杂所以更强”
而其实只是：
- “系统更可观察所以更容易恢复”。

## 六、这篇论文最值得写进知识库的最终结论
### 值得保留的硬结论
- harness 可以被外化成可研究对象
- 模块消融比整体分数更能暴露真正有效的 pattern
- self-evolution 是目前最像正收益模块的候选
- verifier 的价值高度依赖它与最终 acceptance gate 的对齐程度
- file-backed state 更像稳定性与续跑增强器，而不是直接提分器
- NLAH migration 的最大价值，在于 contract-first + artifact-backed closure，而不在于“自然语言比代码更神”

### 不该过度外推的部分
- 还不能说自然语言 harness 会普遍替代 code harness
- 还不能说这套 shared runtime charter 没有新的隐性偏置
- 还不能把 subset benchmark 结果直接当生产定律

## 结论
如果你问我这篇论文在工程上最重要的收获，我会给两个：

1. harness 的真正杠杆，不在“更复杂”，而在“更对齐最终验收对象”
2. code-to-text migration 最值钱的，不是换了表示形式，而是把控制逻辑、状态、契约和闭环证据显式化

所以 RQ2 / RQ3 合起来，真正补强的是这条判断：

一个更好的 harness，不一定是更厚的 harness，
而是一个更显式、更可迁移、更可验证、也更懂得把状态和完成证据落在 artifacts 里的 harness。

## 关联页面
- [[natural-language-agent-harnesses]]
- [[intelligent-harness-runtime]]
- [[harness-engineering]]
- [[evaluator-driven-qa]]
- [[agent-memory-patterns]]
- [[agent-readable-repositories]]
- [[how-to-read-agent-harness-benchmarks]]

## 来源
- [[carlos-e-perez-x-post-2042565202357420542-2026-04-14]]
- [[nlah-arxiv-abs-2603-25723-2026-04-15]]
- [[nlah-arxiv-html-2603-25723-2026-04-15]]
