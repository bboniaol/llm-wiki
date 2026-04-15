---
title: Inngest
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, infrastructure, harness-engineering, workflow, automation]
sources: [raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# Inngest

## 它是什么
Inngest 是一个偏事件驱动、耐久执行（durable execution）的工作流/编排基础设施平台。在当前知识库里，它的重要性不在于“又一个 agent framework”，而在于它明确主张：agent 真正缺的不是更多 framework 抽象，而是一个能提供 retries、state persistence、job queues、event routing、observability 和 concurrency control 的 harness / orchestration substrate。

## 这篇文章提供的独特价值
- 它把 harness 与 framework 的差异讲得更基础设施化：很多人以为自己在选 agent framework，实际上在重复造 harness 运行面。
- 它把 durable execution、event routing、step-level traces、singleton concurrency 这些 workflow infra 能力直接映射成 harness 能力。
- 它给出了一种具体实现思路：把 think → act → observe loop 拆成独立 steps，而不是写成不可恢复的单体循环。
- 它把 sub-agents 进一步落成函数级调用：`step.invoke()` 触发独立 agent run，父会话只接收压缩结果。

## 关键主张
- harness 不只是 prompt、tools 和 rules，还包括重试、持久化、队列、事件与并发控制。
- 每次 LLM 调用和 tool 执行都可以是独立、可重试、可追踪的 step。
- orchestration 应与 agent loop 解耦；这样失败恢复、可观测性和并发治理才更可靠。
- 对 agent 来说，workflow infrastructure 本身就可以是 harness 的一部分，而不是外部附属品。

## 关联
- [[deterministic-backpressure-vs-durable-retries]] 对比了 durable retries 与会话内 deterministic backpressure 的不同职责。
- [[in-process-harness-vs-event-driven-harness]] 对比了 Inngest 代表的 durable orchestrated harness 与更偏会话内 harness 的差异。
- [[harness-engineering]] 是理解这篇文章的主入口。
- [[framework-vs-runtime-vs-harness]] 能直接吸收它对 framework / runtime / harness 边界的重新划分。
- [[multi-agent-delegation]] 能吸收它关于 `step.invoke()` 子代理调用的工程实现。
- [[long-running-agent-tasks]] 会受益于它对 durable execution、step retry 和 singleton concurrency 的论证。

## 来源
- [[inngest-harness-not-framework-2026-04-14]]
