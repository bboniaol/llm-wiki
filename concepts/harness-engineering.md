---
title: Harness Engineering
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, harness-engineering, agentic-engineering, workflow, reliability, observability]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/harrison-chase-x-post-2042612328701812789-2026-04-14.md, raw/articles/rohit-x-post-2041548810804211936-2026-04-14.md, raw/articles/viv-x-post-2041927488918413589-2026-04-14.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md]
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

## 与相近概念的关系
- WolfBench 这条 benchmark 信号说明，[[harness-engineering]] 不只是方法论，也开始成为可以被第三方 benchmark 直接比较的对象。
- [[coding-agent-reliability-stack]] 可以视为当前知识库对 harness 落地层次的一次阶段性综合。
- 相比“让模型会写代码”，[[harness-engineering]] 更关注让系统长期、稳定、可审计地交付代码。
- 它与 [[agent-readable-repositories]] 强相关，因为没有可读仓库，智能体就没有稳定上下文。
- 它也依赖 [[agent-approval-patterns]]、[[agent-sandboxing]]、[[agent-feedback-loops]]、[[agent-observability]] 等能力共同组成控制与纠偏系统。
- 从组织视角看，[[openai]]、Anthropic 和 [[langchain]] 都把它当作真实工程方法论，而不是实验室 demo。
- [[multi-agent-delegation]] 在这里更多体现为角色化分工，而不是单纯并行提速。
- 从 [[humanlayer]] 的说法看，[[harness-engineering]] 也可以被理解为 [[context-engineering]] 在 coding agent 配置面上的具体落点。

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
