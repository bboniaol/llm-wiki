---
title: Agent Feedback Loops
created: 2026-04-14
updated: 2026-04-16
type: concept
tags: [concept, workflow, observability, reliability, testing, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/langchain-x-post-2044429013301485916-2026-04-16.md, raw/articles/langchain-agent-improvement-loop-2026-04-16.md, raw/articles/cognition-swe-check-10x-faster-2026-04-16.md, raw/articles/langsmith-evaluation-overview-2026-04-16.md, raw/articles/braintrust-score-production-traces-2026-04-16.md, raw/articles/langfuse-evaluation-overview-2026-04-16.md, raw/articles/phoenix-evaluation-overview-2026-04-16.md, raw/articles/coderabbit-docs-overview-2026-04-16.md, raw/articles/meticulous-product-overview-2026-04-16.md]
---

# Agent Feedback Loops

## 定义
agent feedback loops 指智能体执行任务后，能够通过测试结果、运行时信号、UI 状态、日志、指标、追踪、审查意见和用户反馈持续修正自身行为的一整套闭环机制。没有反馈回路，智能体只能“一次性出手”；有了反馈回路，智能体才有机会迭代逼近正确结果。

## 在工程上的意义
基于 [[openai]] 的案例，智能体真正的工程能力并不只体现在“会生成代码”，而体现在能否在失败后继续推进：复现问题、解释信号、尝试修复、重新验证、响应审查，再次迭代。Anthropic 这篇应用开发文章则把这一点做得更具体：当 generator 自评不可靠时，最好让独立 evaluator 基于明确标准来接管反馈环，而不是让同一个 agent 一边生成一边自夸。

## 常见反馈源
- 单元测试、集成测试与结构测试
- 浏览器中的 DOM 快照、截图与交互结果
- 日志、指标、追踪等 [[agent-observability]] 信号
- Code review、PR 评论与人类验收意见
- 质量评分、lint、规则检查与回归结果
- sprint contract、验收标准、评分 rubric 与硬阈值

## 新增信号：闭环开始从“修一次”走向“持续改进系统”
- LangChain 新 guide 把 feedback loop 讲得更完整：trace 不是日志终点，而是下一轮改进的原材料。生产 traces 会被 enrich 成 evaluators、annotation queues、offline datasets，并在发版前重新验证。
- Cognition 的 SWE-check 则补了另一个现实面：闭环不只靠主代理自己修自己，越来越多团队会把专用 checker / evaluator 常驻到 diff 级工作流里，以低成本高频运行来抬高可靠性下限。
- 新补的 LangSmith、Braintrust、Langfuse、Phoenix 资料则说明，feedback loop 正在平台化：scorer 可以直接挂到 traces / spans / logs 上后台异步跑，结果再回到 UI、审计和数据集。
- CodeRabbit、Meticulous 这类工具又说明，software checker 也在常驻化：一个挂在 PR，一个挂在 browser regression，都是把反馈节点前移到日常工程入口。
- 两条线合起来说明，[[agent-feedback-loops]] 的竞争优势会越来越来自“证据能否沉淀、评估能否常驻、修正能否回灌”，而不是单次对话里 agent 看起来多聪明。

## 设计原则
- 反馈要尽量机器可读，避免只能靠人类口头解释。
- 反馈要尽量短链路，减少“等很久才知道错了”的成本。
- 反馈必须能重新进入下一轮执行，而不是停留在仪表盘上。
- 闭环不仅要能修 bug，也要能修文档、规则和约束本身。
- 当执行者存在明显自评偏差时，把执行和评估拆成两个角色通常更稳。
- evaluator 也需要被持续校准：看它的日志、找判断偏差、反向修 prompt，而不是默认它天然会 QA。

## 与相近概念的关系
- [[agent-feedback-loops]] 是 [[harness-engineering]] 的动力系统，没有闭环就没有稳定改进。
- [[agent-observability]] 提供运行时证据，是反馈的重要输入层。
- [[coding-agent-evals]] 更偏向离线或半在线的能力衡量，而反馈回路偏向在线执行中的持续修正。
- [[multi-agent-delegation]] 可以把 feedback loop 做成“generator → evaluator → generator”的角色化循环。
- [[evaluator-driven-qa]] 是其中一种更强、更结构化的实现方式。
- [[agent-reliability-patterns]] 则更关注如何把这些闭环沉淀成长期稳定的工程机制。

## 常见误区
- 只有最终人工验收，没有中途反馈节点。
- 反馈存在，但智能体读不到或不能据此行动。
- 只收集失败信号，不把修复策略也编码回系统。
- 让生成 agent 自己负责验收自己，最后输出一堆“看起来不错”的虚假正反馈。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[langchain-x-post-2044429013301485916-2026-04-16|langchain-x-post-2044429013301485916]]
- [[langchain-agent-improvement-loop-2026-04-16]]
- [[cognition-swe-check-10x-faster-2026-04-16]]
