---
title: Harness Engineering
created: 2026-04-14
updated: 2026-04-25
type: concept
tags: [concept, harness-engineering, agentic-engineering, workflow, reliability, observability]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/harrison-chase-x-post-2042612328701812789-2026-04-14.md, raw/articles/rohit-x-post-2041548810804211936-2026-04-14.md, raw/articles/viv-x-post-2041927488918413589-2026-04-14.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md, raw/articles/langchain-agent-improvement-loop-2026-04-16.md, raw/articles/cognition-swe-check-10x-faster-2026-04-16.md, raw/articles/cursor-x-post-2044136953239740909-2026-04-16.md, raw/articles/langchain-x-post-2044429013301485916-2026-04-16.md, raw/articles/ltbase-harness-engineering-2026-04-24.md, raw/articles/ltbase-harness-engineering-faq-2026-04-24.md, raw/articles/lijiuer-harness-electricity-analogy-2026-04-09.md, raw/articles/akshay-pachaar-anatomy-of-agent-harness-2026-04-25.md]
---

# Harness Engineering

## 定义
在 OpenAI、Anthropic 和 LangChain 这些文章里，harness engineering 指的都不是单一工具，也不是 prompt 技巧，而是围绕 coding agent 设计一整套“可执行环境 + 约束 + 反馈回路 + 记录系统”，让智能体能够在真实软件工程中持续地产生可靠结果。LangChain 这篇文章给出了一个很干脆的边界：Agent = Model + Harness；如果你不是模型，那你大概率就在 harness 里。

## 核心命题
文章的核心命题可以概括为：当代码主要由智能体生成时，工程杠杆不再主要来自手写实现，而来自对系统边界、上下文组织、验证机制和修复循环的设计。换句话说，真正稀缺的不是代码产能，而是人类对环境和标准的定义能力。

## 四个案例给出的互补视角
- [[humanlayer]] 这篇文章补上了最强的实践派视角：很多 coding agent 失败首先不是模型不行，而是 harness 配置错了。它把 harness engineering 进一步收敛成一组高杠杆配置面：agentfiles、skills、MCP、sub-agents、hooks 与 back-pressure。
- [[openai]] 更强调：让智能体在一个真实产品代码库里持续交付，需要代码仓库可读、可观测性可消费、架构边界可执行、审查与垃圾回收可闭环。
- Anthropic 的上一版文章更强调：当任务跨越多个 context window 时，harness 必须承担“跨 session 接力系统”的角色，确保下一轮 agent 能快速理解现场并继续推进。
- Anthropic 的应用开发文章再补了一层：对于长链路应用开发，harness 还要负责把模糊 prompt 扩成 spec、把执行与评判拆开、并随着模型能力变化动态简化流程。
- [[langchain]] 这篇文章则把 harness 的边界讲得最抽象：system prompts、tools/skills/MCP、filesystem、sandbox、browser、orchestration logic、hooks/middleware 都属于 harness 组成。
- [[inngest]] 这篇文章再补了一层基础设施视角：如果 retry logic、state persistence、job queues、event routing、step-level observability 和 concurrency control 都是 agent 稳定运行的必要条件，那 workflow infra 本身也属于 harness。
- Harrison Chase 最近两条短帖把这层抽象进一步压实：他明确提出 harness 可能是当前第一层真正稳定的 agent abstraction，而 memory 本质上也是 context，因此 memory design 和 harness design 很难真正拆开。
- Sarah Wooders 的原帖则把这种“很难拆开”具体化成一组 harness 级决策：`AGENTS.md` / `CLAUDE.md` 怎么进上下文、skill metadata 如何展示、compaction 后留下什么、交互是否可查询、filesystem 暴露多少，这些都直接决定 memory 长什么样，因此 memory 不是 harness 外面的插件，而是 harness 内部的 context governance。
- Rohit 对 Claude Code 结构的逆向阅读则强调：production agent system 的可复用价值不只在 prompt，而在 permissions、compaction、retry pipelines、streaming loop 与 sub-agent isolation 这些“基础设施层 harness”。
- Viv 的 Better-Harness 文章型短帖又把 evals 拉进来，提出可以把 evals 视为 harness 的学习信号，用 holdout、tagging 与 human review 驱动持续 hill-climbing。
- João Moura 则从另一面提出反论：即便 harness 比 framework 更厚、内建 planning、memory、filesystem 与 compaction，这一层也会继续 commodity 化，因此 harness 更像 plumbing，而不是长期防御层。
- NLAH 论文则把另一条很值得重视的路线推清楚了：如果 harness 真的是决定 agent 行为的高杠杆层，那它不该永远埋在 controller code 里，而应该被外化成可迁移、可比较、可消融的对象。作者用 [[natural-language-agent-harnesses]] 与 [[intelligent-harness-runtime]]，把 harness 的 pattern layer 明确拆成 contracts、roles、stages、state semantics 与 artifact discipline。

## 关键组成
- 代码仓库从一开始就被设计成智能体的工作环境，而不是人类工程师的附属产物。
- 对某些 agent 系统，event-driven orchestration、durable execution 和 step-level retries 也应被视为 harness 基础层，而不是“外部平台细节”。
- 文档、计划、设计约束和技术债都进入版本控制，构成智能体可访问的事实边界。
- UI、日志、指标、追踪被接入到 agent runtime，形成可验证的反馈回路。
- 架构边界、lint、结构测试和“品味不变式”以可执行规则形式存在，而不是停留在人类共识层。
- 对长任务，harness 还要提供 feature list、progress file、git history、init script、contract file 等跨窗口或跨角色工件。
- 当任务存在明显的自评偏差时，harness 还需要单独的 evaluator、评分标准和验收阈值，而不是让生成 agent 自己给自己打分。
- 从 LangChain 的拆法看，hooks/middleware 也属于 harness 核心：compaction、continuation、lint checks、tool-output offloading 这些都不是细枝末节，而是决定 agent 能不能长期稳定工作的执行逻辑。
- HumanLayer 则把这些抽象组件拉回实战：好 harness 不是把所有规则和工具一次性塞给模型，而是围绕 instruction budget 做 [[progressive-disclosure]]；好 sub-agent 不是为了“多 agent 看起来高级”，而是为了建立 context firewall，控制上下文污染、成本和信息回流粒度。
- 2026-04-16 这批新信号又把另一层边界压实：成熟 harness 不只是执行系统，也包含一条持续改进层。[[langchain]] 把 traces、online evaluators、annotation queues、offline datasets 与 CI gate 连成闭环；[[cognition]] 则把 specialized checker 直接做成产品内常驻角色；[[cursor]] 这类执行面信号则说明 execution frontier 仍在外扩。
- Karan 的实现帖又补了一张偏工程清单式的落地面：critic-in-loop、SQLite/Redis 持久 history、session continuity、guardrails、memory compaction、repo snapshot 注入、以及 `.md` files 作为 agent brain。这说明很多团队口中的 harness，现实里就是一组可直接拼装的系统设计件。
- HumanLayer 的配套文章则进一步把 harness 细化成三类高杠杆工法：短小高信号的 `CLAUDE.md` / `AGENTS.md`、frequent intentional compaction，以及 deterministic back-pressure。

## 这组文章给出的几个强结论
1. 人类角色从“直接写代码”转向“定义任务、环境、验收与约束”。
2. 大而全的 `AGENTS.md` 会失败；更有效的是地图式入口加分层知识库。
3. 可观测性和 UI 可读性不是运维附属品，而是智能体闭环执行的必要条件。
4. 在高吞吐智能体环境中，等待成本可能高于纠错成本，某些传统合并门需要重估。
5. 对跨窗口长任务，harness 不只是“工具合集”，而是 session 接棒机制。
6. planner 和 evaluator 都属于 harness 的一部分：前者防止目标过窄，后者防止自评失真。
7. harness 结构不是一成不变的；当模型能力提升后，一些曾经必要的 sprint 拆分或 context reset 可以被拿掉。
8. harness 不只是“给模型加工具”，而是把 filesystem、state、tools、verification、hooks、routing 组合成一个能工作的系统。
9. 很多所谓“模型不够聪明”的问题，本质上是 harness 没把知识暴露、工具接入、上下文隔离和验证回压设计好。
10. `CLAUDE.md` / `AGENTS.md` 这类 agentfile 是最高杠杆的 harness 配置点之一，但前提是它们短、稳、通用，而不是自动生成的大杂烩。
11. 对长链路或后台 agent，harness 还可能包含 workflow infra：step orchestration、durable retries、event routing 与 singleton concurrency。
12. 第三方 benchmark 如果明确比较的是 agentic harness，并且在相同底模上拉开差距，就说明 harness 本身已经开始成为可独立评测的系统层。
13. 如果连 memory 都被重新解释成 context management，那么 harness 很可能不是临时过渡层，而是 agent 系统里相对稳定的抽象边界。
14. 对 production agent，permissions、compaction、retries、sub-agent isolation 这些基础设施机制，本身就是 harness，而不是“实现细节”。
15. 但如果 João Moura 这条判断成立，那么 harness 即便重要，也未必是长期最可防御的产品层；长期价值可能会进一步上移到 [[entangled-software]] 所强调的 adaptation、trust 与 proprietary usage flywheel。
16. 最近一周的新证据说明，harness 可以先粗分成 execution layer 与 improvement layer：前者负责任务执行与工作流推进，后者负责 traces、evals、annotations、checker 与 regression gate。
17. 因而判断一个 harness 是否成熟，不能只看它会不会跑任务，还要看它有没有把持续观察、评分、标注和防回退做成常驻运行部件。
18. 2026-04-19 的二阶判断把这点再压实了一次：X 上 exact phrase 信号并不密集，但 trace/eval/checker/runtime 这些相邻线索正在合流，说明 harness engineering 的核心边界正在从"agent 执行环境"扩展为"agent 执行 + agent 改进"的复合系统。
19. Akshay Pachaar 的《The Anatomy of an Agent Harness》把 harness 拆成 12 个组件 + 7 个架构选择，是目前知识库里最完整的 harness 组件地图。核心区分：agent 是 emergent behavior，harness 是产生该行为的 machinery。LangChain TerminalBench 证据：只换 harness（同模型同权重）排名从 30 外跳到第 5；LLM 自优化 harness 达到 76.4% pass rate 超过人工设计。Vivek Trivedy 的公式 "If you're not the model, you're the harness" 被收为 canonical。

## 与相近概念的关系
- WolfBench 这条 benchmark 信号说明，[[harness-engineering]] 不只是方法论，也开始成为可以被第三方 benchmark 直接比较的对象。
- [[coding-agent-reliability-stack]] 可以视为当前知识库对 harness 落地层次的一次阶段性综合。
- 相比“让模型会写代码”，[[harness-engineering]] 更关注让系统长期、稳定、可审计地交付代码。
- 它与 [[agent-readable-repositories]] 强相关，因为没有可读仓库，智能体就没有稳定上下文。
- 它也依赖 [[agent-approval-patterns]]、[[agent-sandboxing]]、[[agent-feedback-loops]]、[[agent-observability]] 等能力共同组成控制与纠偏系统。
- 从组织视角看，[[openai]]、Anthropic 和 [[langchain]] 都把它当作真实工程方法论，而不是实验室 demo。
- [[multi-agent-delegation]] 在这里更多体现为角色化分工，而不是单纯并行提速。
- [[humanlayer]] 的说法看，[[harness-engineering]] 也可以被理解为 [[context-engineering]] 在 coding agent 配置面上的具体落点。
- [[natural-language-agent-harnesses]] 则提供了一个更研究化的延伸：把 harness pattern 直接外化成可执行文本对象，在 shared runtime 下做迁移与消融。
- [[harness-engineering-signals-2026-04-19]] 是最近 7 天社交/外链信号的阶段性二阶判断。
- [[harness-engineering-faq-companion]] 把 Lychee FAQ 的 9 个生产决策 + 5 反模式 + 实现优先级收敛成一张判断地图。
- [[claude-managed-agents]] — Anthropic 的托管 harness 实例，验证了"harness 会变薄但不会消失"：不是拆掉 harness，而是把 harness + 基础设施托管起来

## Lychee Technology 的 7 层框架补充
[[lychee-technology]] 的博客文章提供了一个更结构化的 harness 分层视角，与当前知识库中分散的线索形成互补：

### 7-Layer Harness Stack
| 层 | 名称 | 当前知识库中的对应 |
|----|------|------------------|
| 1 | **Cognition** | [[context-engineering]] + [[progressive-disclosure]] |
| 2 | **Tools** | Tool middleware、ranking、dedup、token budget truncation |
| 3 | **Contracts & Interfaces** | Schema validation、type safety、API spec |
| 4 | **Orchestration** | [[coding-agent-workflow-patterns]]、DAG / state machine |
| 5 | **Memory & State** | [[agent-memory-patterns]]、[[long-running-agent-tasks]] |
| 6 | **Evaluation & Observation** | [[coding-agent-evals]]、[[agent-observability]] |
| 7 | **Constraints & Recovery** | [[agent-reliability-patterns]]、idempotency、retry |

这个分层的好处是：**每一层都有明确的职责边界**，而不是把所有东西混在 "harness" 一个大词里。

### 4 设计原则
Lychee 文章把 harness 设计收敛成 4 条可测试原则：
1. **Constrain, don't instruct** — 能用程序限制就不用 prompt 劝说。
2. **Externalize state** — 关键信息必须落在 context window 外面。
3. **Make every step verifiable** — 每层输出都能被非生成方验证。
4. **Fail locally, not globally** — 单步失败只触发单步重试，不重启整条管线。

这 4 条原则与当前知识库中的 [[agent-reliability-patterns]]、[[minimum-viable-agent-harness-checklist]] 直接兼容，但表达更紧凑。

### 4 生产陷阱（Frontline Lessons）
Lychee 文章从长时间运行实践中提炼出 4 个高阶陷阱：
- **Context Anxiety**：token 占用超过 70% 时模型开始跳过步骤或提前收尾。Fix = Context Reset（保存状态→终止实例→启动新 agent）。
- **Self-Grading Illusion**：让模型自评会导致系统性高估。Fix = Sprint Contract（Generator + 独立 Evaluator，Evaluator 必须执行验证且不能看到 Generator 的推理链）。
- **Illusion of Correctness**：在矛盾约束下模型会优化"看起来对"而不是"实际对"。Fix = 反馈必须客观（给编译错误、断言失败、schema mismatch），不能带情绪。
- **Memory Consolidation Cycle**：长期运行后 memory log 膨胀且自相矛盾。Fix = 后台自动压缩日志，去重、消解矛盾、写回 clean state file（有案例把 32K token 压到 7K）。

这些陷阱和修复方法可以直接归入 [[agent-reliability-patterns]] 和 [[long-running-agent-tasks]]。

### Minimum Viable Harness 建议
Lychee 文章给出的 Day 1 起步建议非常务实：
- `state.json` — 结构化任务状态跟踪
- Retry wrapper — 每个 tool call 至少一次自动重试 + 指数退避
- Schema validator — 每个 LLM 输出先过 JSON schema 验证
- Tool output truncation — 硬限制 tool payload token 预算

这与 [[minimum-viable-agent-harness-checklist]] 的结论基本一致，但把起点明确为"从 Layer 7 倒着建"。

## 李韭二的"LLM 是电"心智模型补充
[[lijiuer-harness-electricity-analogy-2026-04-09|李韭二]] 这篇长文从心智模型角度对 harness engineering 做了重要补充，提出了一个与"马"（控制论）完全不同的"电"（基础设施）类比：

### 核心区分：马 vs 电
| 心智模型 | 隐喻 | 工程导向 | 结果 |
|---------|------|---------|------|
| **马** | LLM 是一匹有力但不受控的动物 | 造马鞍、缰绳、甲胄 | 控制论思维 |
| **电** | LLM 是一种通用能源 | 造变压器、输电网、电器 | 基础设施思维 |

### 三个流行比喻的问题
1. **Scaffold（脚手架）** — 暗示 harness 是过渡性的，会随模型增强而消失。反例：Anthropic 和 Manus 确实在移除复杂度，但移除的是复杂度而非 harness 本身。harness 会变薄，但不会被拆掉。
2. **Wrapper（封装层）** — 暗示 harness 是薄薄一层，不如被包裹的模型重要。反例：Vercel 移除 80% 工具定义后成功率从 80%→100%，速度快 3.5 倍。如果 harness 只是包装，移除工具应该让性能变差。
3. **Engine vs Car（引擎与汽车）** — 承认 harness 不是附属品，但品类单一性局限明显。LLM agent 跨越编程助手、客服、医疗诊断等完全不同的品类，更像是电力接不同电器，而非引擎装不同车。

### 最精确的比喻：操作系统
Beren Millidge 2023 年的文章提出：裸 LLM = 没有 OS 的 CPU，harness = 让它可用的操作系统。这个类比在**微观架构层面**最准确，但解释不了**宏观产业层面**的演化。

### 电力类比的三层对应
| 电力产业层 | Harness Engineering 对应 |
|-----------|-------------------------|
| 发电站 | 模型提供商（OpenAI/Anthropic/等） |
| 输电网 | 模型 API / 基础设施 |
| **电器** | **Agent Harness** — 将标准化 LLM 转化为特定场景价值的完整工程系统 |
| **电气工程** | **Harness Engineering** — 制造电器的学科 |

### 历史警告
Dr. Philippa Hardman 指出：工厂只有在围绕电力重新设计之后才变得更高效，简单地把蒸汽引擎换成电动马达是不够的。

今天的数据：McKinsey 2025 报告显示不到 10% 的企业 AI 应用能走过试点阶段；MIT 研究发现 95% 的生成式 AI 项目没有产生可量化的财务影响。企业以为"插上电就行"，但必须围绕新的能源形态重新设计整套系统。

### 与现有知识的关联
- 与 [[framework-vs-runtime-vs-harness]] 直接兼容 — "电"类比解释了为什么 framework ≠ harness
- 与 [[entangled-software]] 形成互补 — João Moura 说 harness 会 commodity 化，李韭二说 harness 会变薄但不会消失，两者合起来看：变薄的是具体实现，不消失的是系统层需求
- 与 [[harness-engineering-7-day-study-plan]] 兼容 — 电力类比提供了学习 harness 的宏观叙事框架

## 未决问题
- 这种做法在别的团队、别的仓库结构上能复制到什么程度？
- 随着模型能力增强，哪些约束会被放松，哪些反而必须更严格？
- evaluator 在什么任务边界上最值得保留，什么情况下已经变成额外成本？
- 模型是否会逐渐吸收今天 harness 里的能力，还是 harness 本身也会持续进化成更复杂的系统层？

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
- [[wolfbench-hermes-agent-x-post-2026-04-14]]
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
- [[joao-moura-x-post-2043726271449112776-2026-04-15]]
- [[karan-x-post-2043618895328932340-2026-04-15]]
- [[nlah-arxiv-html-2603-25723-2026-04-15]]
- [[langchain-agent-improvement-loop-2026-04-16]]
- [[cognition-swe-check-10x-faster-2026-04-16]]
- [[langchain-x-post-2044429013301485916-2026-04-16|langchain-x-post-2044429013301485916]]
- [[cursor-x-post-2044136953239740909-2026-04-16|cursor-x-post-2044136953239740909]]
- [[ltbase-harness-engineering-2026-04-24|ltbase-harness-engineering]]
- [[ltbase-harness-engineering-faq-2026-04-24|ltbase-harness-engineering-faq]]
- [[lijiuer-harness-electricity-analogy-2026-04-09|lijiuer-harness-electricity-analogy]]
- [[akshay-pachaar-anatomy-of-agent-harness-2026-04-25|akshay-pachaar-anatomy-of-agent-harness]]
