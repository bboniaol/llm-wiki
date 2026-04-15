---
title: Pluggable Agent Backends
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, infrastructure, tooling, workflow, best-practice, harness-engineering]
sources: [raw/articles/langchain-deepagents-overview-2026-04-14.md]
---

# Pluggable Agent Backends

## 定义
pluggable agent backends 指 agent harness 把底层执行与存储能力抽象成可替换 backend 的设计模式。它解决的核心问题不是“换个存储实现”，而是让同一套 agent 逻辑能在不同运行面上切换：内存、本地磁盘、持久化 store、sandbox、甚至自定义执行环境。

## 为什么它重要
很多团队一开始把 agent 当成“模型 + prompt + 工具”的轻组合，但一旦任务变长、状态变多、环境变复杂，backend 就会变成真实工程约束。Deep Agents 这份文档很值钱的地方在于，它把 filesystem backend、sandbox backend、memory backend 明确做成了一等抽象，而不是散在不同 feature 里。

## Deep Agents 给出的关键信号
- virtual filesystem 可以切换到 in-memory、local disk、LangGraph store、sandbox backends 或自定义 backend。
- shell execution 不是默认就有，而是在 sandbox backend 存在时通过 `execute` tool 暴露。
- same agent logic 可以在不同 backend 上跑，说明 harness 设计被刻意从“具体环境”里解耦出来。
- backend 不只影响存储位置，还影响 context management、permissions、memory persistence 与安全边界。

## 设计原则
- 把 agent 逻辑和底层运行面解耦，避免业务流程和单一环境强绑定。
- backend 要同时考虑：持久化、权限、可观测性、执行能力，而不是只看吞吐或存储。
- 允许不同 backend 组合使用，例如本地文件 + 持久 memory store + sandbox execute。
- 把 backend 当作 harness primitive，而不是后期优化项。

## 与相近概念的关系
- [[pluggable-agent-backends]] 是 [[harness-engineering]] 的实现层问题。
- [[agent-readable-repositories]] 关心仓库怎么作为协作与上下文面；backend 关心这块面落在哪、怎么接入。
- [[agent-sandboxing]] 是其中一种 backend 方向，强调隔离执行。
- [[agent-memory-patterns]] 则关注在不同 backend 上怎么做长期记忆与状态回收。
- [[cloud-agent-operations]] 也可以看作把 backend 问题扩展到分布式 / 云端运行面。

## 常见误区
- 以为 backend 只是存储实现细节。
- 一开始把 agent 强绑定到本地磁盘，后面再硬迁移到云端或持久 store。
- 只换 backend，不重新审视 permissions、memory 和 observability 设计。
- 把 sandbox 当成工具开关，而不是 backend 级别的运行面差异。

## 来源
- [[langchain-deepagents-overview-2026-04-14]]
