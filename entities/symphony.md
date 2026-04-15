---
title: Symphony
created: 2026-04-15
updated: 2026-04-15
type: entity
tags: [product, open-source, workflow, orchestration, harness-engineering]
sources: [raw/articles/openai-symphony-spec-2026-04-15.md, raw/articles/latent-space-extreme-harness-engineering-2026-04-15.md]
---

# Symphony

## 它是什么
Symphony 是 OpenAI 开源的一条 coding-agent orchestration 路线。按 README 和 SPEC 的定义，它不是通用 workflow engine，而是一个 long-running automation service：持续读取 issue tracker，把每个 issue 转成 isolated autonomous implementation run，让团队管理 work，而不是盯着 coding agent 敲终端。

## 当前可确认的能力
- 按固定 cadence 轮询 issue tracker（当前 spec 以 Linear 为例）。
- 为每个 issue 创建 deterministic workspace，并在 run 之间保留。
- 在 workspace 中启动 coding agent，会话行为由 repo-owned `WORKFLOW.md` 合约定义。
- 提供 bounded concurrency、reconciliation、restart recovery、structured logs 等运营能力。
- 允许 workflow 在 `Human Review` 之类的 handoff state 停下，而不是强行自动 Done。
- 在 Latent.Space 的文章里，Symphony 被进一步描述为 OpenAI 内部“ghost library”/ orchestration layer：可以 supervise、rework、coordinate 大量 coding agents，并把 PR lifecycle 继续自动推进。

## 为什么它重要
Symphony 让一个很重要的分界更清楚了：
- 本地 coding agent 解决的是“如何让 agent 帮我写代码”
- Symphony 解决的是“如何把 ticket work 变成可持续、可恢复、可审计的 autonomous runs”

也就是说，它更接近 [[cloud-agent-operations]] 的 work execution substrate，而不是单轮会话工具。

## 在知识库中的位置
[[symphony]] 现在更像 OpenAI 版 work orchestration reference implementation：
- 它把 per-issue workspace、repo-owned workflow contract、restart recovery、observability 和 autonomous PR handoff 串成了一条完整 run model
- 它也让 [[framework-vs-runtime-vs-harness]] 这张图里 “runtime / orchestration” 那层更具体了

## 关联
- [[openai-frontier]] 是 Symphony 所属的平台母体。
- [[cloud-agent-operations]] 是理解 Symphony 的主要入口。
- [[coding-agent-workflow-patterns]] 里的 PR 驱动闭环、后台自动化工作流，在这里变成长期服务。
- [[harness-engineering]] 解释了为什么 `WORKFLOW.md`、skills、review surfaces、build loops 都被当成系统的一部分。

## 来源
- [[openai-symphony-spec-2026-04-15]]
- [[latent-space-extreme-harness-engineering-2026-04-15]]
