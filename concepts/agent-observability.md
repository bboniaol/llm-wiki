---
title: Agent Observability
created: 2026-04-14
updated: 2026-04-16
type: concept
tags: [concept, observability, tooling, reliability, workflow, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/langchain-x-post-2044429013301485916-2026-04-16.md, raw/articles/langchain-agent-improvement-loop-2026-04-16.md, raw/articles/cognition-swe-check-10x-faster-2026-04-16.md, raw/articles/braintrust-score-production-traces-2026-04-16.md, raw/articles/langfuse-evaluation-overview-2026-04-16.md, raw/articles/phoenix-evaluation-overview-2026-04-16.md]
---

# Agent Observability

## 定义
agent observability 指围绕智能体执行过程建立可观测能力，使系统能够回答：智能体看到了什么、做了什么、为什么失败、哪里变慢、修改后是否真的变好。它把日志、指标、追踪、运行事件和中间状态暴露给人类和智能体自己。

## 在文章中的体现
[[openai]] 的案例明确展示了这一点：他们把日志、指标和追踪接入本地可观测性堆栈，并让 [[codex]] 自己查询这些信号。Cursor 的 cloud agent 文档则补了另一个现实面：在后台 agent 场景里，可观测性不仅是调试信号，还包括 screenshots、videos、log references、audit logs 和 hooks 输出，否则团队根本不知道后台代理到底做了什么。

## 新增信号：observability 正在变成数据供给层
LangChain 这条新线索把 observability 的角色说得更重：trace 不只是为了排障，而是 improvement loop 的起点。在线 evaluators、annotation queues、insights clustering 和 offline datasets 都建立在 traces 之上。Cognition 的 SWE-check 又补了一层——如果 dogfooding 反馈会倒逼团队增加 tracing / lookup tools，那么 observability 实际上也在参与训练和产品对齐。

新补的 Braintrust、Langfuse、Phoenix 资料则把这个趋势产品化了：
- Braintrust 直接把 production traces 自动打分，并把结果挂回 trace / span；
- Langfuse 明确把 live evaluator 绑定到 live traces；
- Phoenix 甚至把 evaluator 自己纳入 OpenTelemetry tracing，连 judge 的输入、prompt、reasoning、score 与 timing 都可追。

这意味着 [[agent-observability]] 已经不只是“让人看见 agent 做了什么”，而是“为在线 eval、evaluator 审计和持续回归监控提供原材料”。更完整的阶段性归纳见 [[from-offline-benchmark-to-online-evals]]。

## 为什么它是工程层核心能力
- 没有可观测性，智能体无法定位复杂故障，只能盲改。
- 没有可观测性，人类也无法审计智能体到底做了什么。
- 在高吞吐智能体系统中，人工 QA 不可能覆盖一切，可观测性必须部分机器可消费。
- 对 cloud agents 和 automations，没有 artifacts 和 audit trails，后台自动化几乎不可治理。

## 典型信号
- 应用日志、错误堆栈、结构化事件
- 性能指标、资源消耗、延迟和吞吐
- 调用链追踪、关键用户旅程跨度
- 浏览器侧运行时事件、DOM 状态、截图
- 任务级运行记录：执行时长、重试次数、失败点、介入点
- PR 附件中的 screenshots、videos、log references
- 企业 audit logs、hooks、compliance logging

## 设计原则
- 优先结构化信号，而不是只留自然语言日志。
- 让智能体可以查询这些信号，而不是只让人类看图表。
- 把可观测性纳入日常 workflow，而不是故障后临时补采样。
- 将可观测性与规则、评测和修复闭环打通。
- 对后台 agent，要区分“运行证据”和“合规证据”：前者帮你修问题，后者帮你追责任。

## 与相近概念的关系
- [[agent-observability]] 提供证据层。
- [[agent-feedback-loops]] 消费这些证据，推动迭代修正。
- [[coding-agent-evals]] 利用这些信号做离线或阶段性评估。
- [[cloud-agent-operations]] 让可观测性从本地调试问题，扩展到后台自动化与组织审计。
- [[harness-engineering]] 则把它们组合进一个长期可运行的系统支架中。

## 常见误区
- 有监控图，但智能体无法访问。
- 只看最终报错，不记录中间决策和运行轨迹。
- 把 observability 当作运维附属，而不是智能体执行基础设施。
- 后台 agent 只留“success/failure”状态，不留证据工件和审计日志。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[cursor-docs-cloud-agent-capabilities-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
- [[langchain-x-post-2044429013301485916-2026-04-16|langchain-x-post-2044429013301485916]]
- [[langchain-agent-improvement-loop-2026-04-16]]
- [[cognition-swe-check-10x-faster-2026-04-16]]
