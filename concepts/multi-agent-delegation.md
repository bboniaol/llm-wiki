---
title: Multi-agent Delegation
created: 2026-04-14
updated: 2026-04-25
type: concept
tags: [concept, orchestration, workflow, automation, coding-agent, agentic-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/claude-code-docs-sub-agents-2026-04-14.md, raw/articles/cursor-docs-subagents-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/suryansh-tiwari-sub-agents-vs-agent-teams-2026-04-25.md]
---

# Multi-agent Delegation

## 定义
multi-agent delegation 指把复杂任务拆分后，交给多个智能体或多个智能体角色并行/串行处理，再通过汇总、审查或仲裁机制合并结果的工程模式。重点不是“多 agent 更酷”，而是利用角色分工、并行性和隔离上下文来提高吞吐与质量。

## 为什么值得单独讨论
当任务复杂度、反馈回路数量和上下文负载持续增长时，单个智能体可能同时承担实现、审查、验证、文档更新和回归分析，容易顾此失彼。适当 delegation 能把执行、复查和维护分开，这和 [[openai]] 文章里“智能体对智能体审查”的思路是相通的。Claude Code 与 Cursor 的 subagent 文档则把这种分工做成了更明确的产品能力。

## 典型角色
- 实现 agent：负责写代码、修 bug、改配置。
- 审查 agent：负责 review、找漏洞、提结构问题。
- 验证 agent：负责跑测试、查日志、查 UI、做回归。
- 文档 agent：负责更新规范、计划和知识库，例如 [[doc-gardening-agents]]。
- 规划 / 探索 agent：只负责研究代码库、写计划、找上下文，不直接改代码。

## 从 Claude Code / Cursor / Anthropic / LangChain 得到的新信号
- Claude Code 内置 Explore、Plan、general-purpose 等 subagents，并支持自定义 subagents、模型选择、工具限制、foreground/background、persistent memory。
- Cursor 也强调 subagents 的 context isolation、verification agent、orchestrator pattern 与并行执行。
- Anthropic 的上一版长任务文把 initializer agent 和 coding agent 作为角色化 delegation：先铺地基，再做增量推进。
- Anthropic 的应用开发文章把角色继续细化成 planner / generator / evaluator：planner 负责扩规格，generator 负责构建，evaluator 负责基于 Playwright MCP 和评分标准做独立验收。
- Anthropic 的 context engineering 文章则把 sub-agent architectures 讲成一种“上下文治理手段”：主 agent 保持高层计划，子 agent 在各自干净窗口里做深挖，只把压缩后的高信号结果带回主线程。
- [[deepagents]] 则把这套东西直接产品化成 built-in `task` tool：主 agent 可以显式委派 specialized subagents，依靠 context isolation 保持主线程干净，同时允许 subagents 继承或覆盖权限规则。
- [[humanlayer]] 补了一刀很实用的判断：sub-agents 最值得用在 research、codebase exploration、grep/日志检索、文档扫描这类“答案很短、过程很吵”的任务上；它们应返回压缩结论与可追溯引用，而不是把中间噪音倒回父线程。
- [[inngest]] 则给了一个更基础设施化的实现：主 agent 通过 `step.invoke()` 拉起独立 agent function run，让子代理天然拥有自己的 retries、durable execution、step-level observability 和独立 session key。

## Sub-Agents vs Agent Teams

来自 [[suryansh-tiwari-sub-agents-vs-agent-teams-2026-04-25]] 的核心框架：

| | Sub-Agents | Agent Teams |
|---|---|---|
| 焦点 | 执行（并行隔离） | 协作（通信协调） |
| 状态 | 无状态 | 持久 |
| 交互 | 一次性 | 持续 |
| 控制 | Parent 控制 | 点对点 |
| 上下文 | 完全隔离 | 共享 |
| 适用 | 任务独立、可干净分离上下文 | 任务相互依赖、需实时协作 |

**关键洞察**：不要按角色（planner/developer/tester）拆分，要按**上下文边界**拆分。如果两个任务共享深层上下文，放在同一个 agent；只有当上下文能干净分离时才拆分。

## 5 个关键模式

1. **Prompt chaining** — 顺序步骤
2. **Routing** — 任务路由到正确 agent
3. **Parallelization** — 独立任务并行（sub-agents 主战场）
4. **Orchestrator–worker** — 一个 agent 委派给多个 worker
5. **Evaluator–optimizer** — 生成+精炼的闭环

## 设计原则
- 先分清是"需要并行隔离"还是"需要协作通信"，再选 sub-agents 或 agent teams。
- 委派单元必须足够独立，避免上下文彼此强耦合。
- 汇总阶段要有明确裁决机制，否则只是把混乱并行化。
- delegation 不是替代 [[agent-approval-patterns]] 和 [[agent-sandboxing]]，而是要和它们协同。
- 用 subagent 的独立上下文来隔离高噪声工作，而不是把所有日志、搜索结果塞回主线程。
- 把 subagent 当成 context firewall：任务边界、可用工具、返回格式和回流粒度都要事先设计。
- 子 agent 不一定要和父 agent 用同一档模型；高成本模型可留给规划与仲裁，廉价模型处理高噪声子任务。
- 如果任务在共享会话上容易冲突，要显式设计 singleton concurrency 或等价并发边界。
- 给不同角色不对称的权限和评价职责：规划者不乱定实现细节，执行者不自己给自己盖章，评估者不直接改目标。

## 与相近概念的关系
- [[multi-agent-delegation]] 属于 [[agentic-engineering]] 的协作形态之一。
- 它依赖 [[agent-memory-patterns]] 和 [[repo-as-system-of-record]] 共享事实基础。
- 在 [[coding-agent-workflow-patterns]] 中，它通常以实现/评审/验证分工方式出现。
- [[agent-feedback-loops]] 让 delegation 不只是分工，还能形成 generator → evaluator → generator 的纠偏循环。
- 从 [[context-engineering]] 视角看，delegation 还是一种上下文压缩与污染隔离机制。
- 如果没有 [[agent-reliability-patterns]] 约束，delegation 会把问题放大成群体噪声。

## 常见误区
- 把任何任务都拆成多 agent，结果协调成本比收益更高。
- 角色定义不清，多个 agent 互相打架。
- 只有分工，没有汇总与仲裁，最后输出互相冲突。
- 把 subagent 当成单纯并行加速器，忽略它的核心价值其实是上下文隔离与职责分离。
- 子 agent 返回完整过程转录，导致父线程重新被噪音污染。
- **按角色拆分（planner/developer/tester）而不是按上下文边界拆分**，导致每次交接都丢失上下文。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[claude-code-docs-sub-agents-2026-04-14]]
- [[cursor-docs-subagents-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
