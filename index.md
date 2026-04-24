# Wiki Index

> AI 圈 Harness Engineering 学习知识库索引。
> 每个页面按类型登记，并附一行摘要。
> Last updated: 2026-04-24 | Total pages: 80

## Entities
<!-- Alphabetical within section -->
- [[anthropic]] — Claude / Claude Code / Claude Agent SDK / Managed Agents 的发布方，也是长任务与应用开发 harness 方法的重要来源。
- [[circleci]] — Claude Code / Claude Agent SDK 在 CI/CD maintenance automation 与 PR 闭环中的公开案例主体。
- [[claude-code]] — Anthropic 的 agentic coding tool，已出现 initializer/coding 与 planner/generator/evaluator 两类 harness 角色结构。
- [[claude-managed-agents]] — Anthropic 的托管 agent runtime / API 形态，已有客户采用案例，也已出现 public beta 与 managed harness 架构信号。
- [[codex]] — OpenAI 在文中使用的核心 coding agent，负责代码、测试、文档、审查与验证闭环。
- [[cognition]] — 通过 SWE-check 这条 specialized checker model 信号，展示把 bug detection / eval 能力产品化并挂到 coding harness 内部的一条路线。
- [[crewai]] — 同时拥有 framework 与 harness 叙事，但公开主张 harness 也会快速 commodity 化的一条 agent 平台路线。
- [[cursor]] — 带本地控制面、browser tools、cloud agents 和 enterprise controls 的 agent 平台。
- [[deepagents]] — LangChain 基于 LangGraph 构建的 harness SDK / CLI，内置 planning、filesystem、subagents、memory、permissions 和 HITL。
- [[desysflow]] — 把 critic-in-loop、session continuity、memory compaction 与 `.md` brains 收成一套实装 harness checklist 的薄信号对象。
- [[hermes-agent]] — 当前以 WolfBench benchmark 信号进入知识库的 agentic harness 对象，表现亮点在于更高的可靠性下限。
- [[humanlayer]] — 用实践导向文章系统化总结 agentfiles、skills、MCP、sub-agents、hooks 与 back-pressure 的团队/公司。
- [[inngest]] — 用 event-driven durable workflow infrastructure 重新解释 harness 与 framework 边界的编排平台。
- [[lychee-technology]] — 发布 7 层 harness stack 与 4 个生产陷阱框架的工程博客主体，同时开发 Forma 等产品。
- [[langchain]] — 通过 "Agent = Model + Harness" 明确拆解 harness 边界与核心 primitive 的生态/公司。
- [[letta]] — 把 memory-first coding harness、git-backed memory filesystem 与 Context Constitution 收束成一条 experiential AI 路线的公司。
- [[money-forward]] — Cursor 的跨 engineering / QA / product / design adoption 公开案例主体。
- [[openai]] — 通过真实产品实践验证 harness engineering 的组织与方法论主体。
- [[openai-frontier]] — OpenAI 面向 enterprise agent deployment 与 transformation 的平台层上下文。
- [[sentry]] — Claude Managed Agents 在 bug fixing → PR 闭环中的公开采用案例主体。
- [[wolfbench]] — 当前库里关于第三方 harness benchmark 的一个公开信号来源。

## Concepts
- [[agent-approval-patterns]] — 定义哪些智能体动作自动执行、哪些动作需要人工批准的控制策略。
- [[agent-feedback-loops]] — 让智能体基于测试、日志、审查与运行信号持续修正的闭环机制。
- [[agent-memory-patterns]] — 区分会话记忆、工件记忆与规则记忆的智能体记忆设计模式。
- [[agent-observability]] — 让智能体和人类都能查询执行过程、运行信号与故障证据的可观测能力。
- [[agent-readable-repositories]] — 让仓库本身成为智能体可导航、可检索、可验证的记录系统。
- [[agent-reliability-patterns]] — 把约束、验证、隔离、审批与治理串成稳定性体系的工程模式。
- [[agent-sandboxing]] — 用隔离环境、最小权限和受控接口限制智能体执行边界。
- [[agentic-engineering]] — 把智能体作为主动执行者纳入工程流程的系统设计。
- [[cloud-agent-operations]] — 把 coding agents 扩展到云端后台执行与组织级治理的工程模式。
- [[coding-agent-evals]] — 用真实任务、工具使用和稳定性指标评测代码智能体系统的能力。
- [[coding-agent-workflow-patterns]] — 将任务拆解、验证、PR 闭环等实践沉淀为可复用 workflow 模板。
- [[context-constitution]] — Letta 把 context management、identity、memory 与 continuity 正式制度化的一套原则文档。
- [[context-engineering]] — 围绕上下文组织、注入、裁剪与更新机制的工程设计。
- [[doc-gardening-agents]] — 周期性修剪、更新和校验文档系统的维护型智能体。
- [[entangled-software]] — 当 harness 也 commodity 化后，软件与客户工作方式双向塑形、持续适配的一种上层产品判断框架。
- [[evaluator-driven-qa]] — 把生成与验收拆给不同 agent 角色的质量保障模式。
- [[harness-engineering]] — 围绕 coding agent 设计环境、约束与反馈回路的工程方法。
- [[intelligent-harness-runtime]] — NLAH 论文提出的共享 runtime substrate，用来解释并执行自然语言 harness。
- [[long-running-agent-tasks]] — 处理长时间、多阶段、可恢复智能体任务的工程方法。
- [[multi-agent-delegation]] — 将复杂任务拆给多个智能体角色协作完成的委派模式。
- [[natural-language-agent-harnesses]] — 把 harness pattern 外化成可执行自然语言工件，并在 shared runtime 下迁移、比较与消融的研究路线。
- [[pluggable-agent-backends]] — 把 agent 底层存储与执行面设计成可替换 backend 的工程模式。
- [[progressive-disclosure]] — 按需暴露规则、知识与工具，避免在会话开始时一次性灌满上下文。
- [[repo-as-system-of-record]] — 把代码仓库作为规则、计划、决策和上下文的主事实边界。
- [[symphony]] — 把 issue work 转成 isolated autonomous implementation runs 的 OpenAI orchestration 服务 / ghost 库。
- [[vibe-coding-production-safety]] — Anthropic Eric 提出的生产环境 vibe coding 安全策略：叶节点/核心架构分层、可验证性设计、TDD 与工具链组合。

## Comparisons
- [[approval-vs-sandbox-vs-observability]] — 对比批准机制、执行隔离与可观测性在控制面中的不同职责。
- [[codex-vs-claude-code-vs-cursor]] — 基于当前案例与官方资料，对三类 coding agent 工具做阶段性框架对比。
- [[cursor-vs-claude-managed-agents-platform-readiness]] — 对比 Cursor 作为平台工作台，与 Claude Managed Agents 作为托管平台底座，在 readiness 上分别强在哪一层。
- [[deterministic-backpressure-vs-durable-retries]] — 对比会话内验证信号治理，与流程级可恢复重试机制的不同职责。
- [[evaluator-driven-qa-vs-human-in-the-loop-review]] — 对比自动评估闭环与人工关键节点审查的不同职责。
- [[framework-vs-runtime-vs-harness]] — 对比构建层、运行层与系统支架层在 agent 工程里的不同职责。
- [[in-process-harness-vs-event-driven-harness]] — 对比会话内实践型 harness 与事件驱动、可恢复编排型 harness 的不同主战场。
- [[harness-vs-context-vs-agentic-engineering]] — 从 actor、context、harness 三个视角区分常被混用的智能体工程概念。
- [[local-agent-controls-vs-cloud-agent-controls]] — 对比本地交互式 agent 控制与云端后台代理治理的不同重点。

## Queries
- [[coding-agent-reliability-stack]] — 把 coding agent 稳定落地所需的上下文、验证、恢复、编排与治理能力压成一张六层方法地图。
- [[claude-managed-agents-platform-readiness-audit]] — 基于 Sentry 案例与 public beta / runtime 架构信号，审 Claude Managed Agents 作为托管平台底座是否已经 readiness 过线。
- [[coding-agent-adoption-patterns]] — 把 coding agent 在组织里的常见扩散路径压成四种 adoption pattern，并指出最稳的扩散顺序。
- [[coding-agent-governance-checklist]] — 把 coding agent 上线前最少该过的任务边界、权限、sandbox、审批、证据、回退和责任检查压成一张 checklist。
- [[coding-agent-maturity-model]] — 把 coding agent 从可试用、可稳定、可复用、可治理到可平台化的五级成熟度压成一张总图。
- [[coding-agent-org-design-patterns]] — 把 coding agent 落到组织里时的职责拆分、验收边界、运行面治理和证据责任压成一张责任地图。
- [[coding-agent-platform-readiness-audit]] — 把 workflow、reliability、governance、org、platform 五层 readiness 压成一张可直接审团队的审计表。
- [[cursor-platform-readiness-audit]] — 基于当前公开 docs 与 Money Forward 案例，审 Cursor 是否真的已经进入平台 readiness 阶段。
- [[deepagents-platform-readiness-audit]] — 基于公开实现与 harness 抽象资料，审 Deep Agents 作为开放平台骨架是否已经 readiness 过线。
- [[extreme-harness-engineering]] — 把 OpenAI Frontier / Symphony / dark factory 这条极端 agent org 线压成一页运行面分析。
- [[from-offline-benchmark-to-online-evals]] — 把 online scoring、live evaluator、PR checker 与 browser regression checker 收成一张“离线评测如何演成常驻质量层”的地图。
- [[from-local-coding-agent-to-team-agent-platform]] — 把个人本地 coding agent 演进到团队级 agent 平台的路径压成六阶段路线图。
- [[harness-engineering-7-day-study-plan]] — 按工作日 2 小时、周末加量的节奏，把 harness engineering 学成一周可执行的系统学习路线。
- [[harness-engineering-system-map]] — 把当前知识库里的 harness engineering 组件串成一张八层思维导图与系统学习地图。
- [[harness-engineering-faq-companion]] — 把 Lychee FAQ 的 9 个生产决策 + 5 反模式 + 实现优先级收敛成一张判断地图。
- [[harness-engineering-signals-2026-04-16]] — 汇总最近 7 天最值得保留的三条 X 信号，并给出 trace/eval/checker/runtime 四层判断。
- [[harness-engineering-signals-2026-04-18]] — 回看最近 7 天 X 信号后，把 harness discussion 收束成 execution layer 与 improvement layer 两层判断。
- [[harness-engineering-signals-2026-04-19]] — 今日信号一般但结构更清楚：把最近 7 天的 X/外链信号收束为 execution layer 与 improvement layer 的二阶判断。
- [[how-to-read-agent-harness-benchmarks]] — 总结读 harness benchmark 时该优先看哪些结构信号，而不是只盯单个高分。
- [[managed-harness-vs-open-harness]] — 从运行面、控制权、组织治理与 lock-in 风险四个角度，判断托管 harness 和开放 harness 各适合什么阶段。
- [[minimum-viable-agent-harness-checklist]] — 把 Anthropic / Letta / Karan 这三条线压成一张最小可落地的 agent harness 清单。
- [[social-benchmark-and-product-signals-2026-04-14]] — 汇总一批短社交信号里关于 harness、self-improvement、long-horizon benchmark、cloud runtime 与 open-vs-managed 路线分化的共振趋势。
- [[three-platform-archetypes-for-coding-agents]] — 把平台工作台型、托管底座型、开放骨架型三条 coding agent 平台路线收成一张 archetype 总图。
- [[what-nlah-rq2-rq3-actually-show]] — 提炼 NLAH 论文里模块消融与 code-to-text migration 真正说明了什么。
