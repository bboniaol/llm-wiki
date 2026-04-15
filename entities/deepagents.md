---
title: Deep Agents
created: 2026-04-14
updated: 2026-04-15
type: entity
tags: [product, open-source, coding-agent, harness-engineering, tooling]
sources: [raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/harrison-chase-x-post-2042978500567609738-2026-04-15.md]
---

# Deep Agents

## 它是什么
Deep Agents 是 LangChain 推出的 agent harness / SDK / CLI 体系。按官方 overview 的定义，它不是另一个单纯的 agent helper，而是一套把 planning、filesystem、subagents、memory、permissions、human-in-the-loop、skills 和 sandbox execution 预先组合好的 agent harness。

## 当前可确认的能力
- 提供 Deep Agents SDK，用于构建复杂、多步骤 agent。
- 提供 Deep Agents CLI，作为构建在该 SDK 之上的 terminal coding agent。
- 使用 LangGraph runtime，支持 durable execution、streaming、human-in-the-loop 等能力。
- 内置 write_todos、filesystem tools、task subagent tool、execute shell tool。
- 支持 pluggable filesystem backends：in-memory、local disk、LangGraph store、sandbox backends、自定义 backend。
- 支持 long-term memory、permission rules、skills、provider-agnostic models。
- 支持把 human approval 直接接到 LangGraph interrupt 上，而不是只靠外围 UI 弹框。

## 新增信号：为什么 LangChain 现在强调 Deep Agents
Harrison Chase 在 2026-04-15 的帖子里把 Deep Agents 放进了一个更明确的战略叙事：如果 harness 与 memory 本来就绑在一起，那么 open harness 的价值就不只是“更灵活”，而是让团队继续拥有自己的记忆、上下文形状和 provider optionality。

按这条叙事，[[deepagents]] 被推成的是一种 open / model-agnostic / deployable 的 memory-bearing harness：
- 不是只会调模型的 SDK，而是可承载记忆与状态主权的 agent runtime
- 不是把记忆外包给 provider API，而是允许接 Redis、Postgres 等自有 memory store
- 不是只在 LangChain 生态内自洽，而是想成为可迁移的 open harness 底座

## 它在知识库里的价值
如果说 LangChain 那篇 blog 主要负责定义 harness 是什么，那么 deepagents overview 的价值在于把那套抽象定义落成了一套具体实现：
- harness 不是空概念，而是一组内建 runtime primitive
- filesystem 不是附属功能，而是 context / memory / permission / sandbox 的共同底座
- multi-agent delegation、human approval、context compaction 都能在同一套 runtime 里被组合
- backend 是可插拔的，说明 harness 被当成“可移植运行面”而不是单机脚手架

## 在知识库中的位置
[[deepagents]] 现在更像“LangChain 版 harness runtime reference implementation”：
- 用它可以看到 harness 抽象如何落地
- 也能反推哪些能力应该被看作 agent runtime primitive，而不是产品偶然功能

## 关联
- [[langchain]] 是 Deep Agents 的所属生态与方法论来源。
- [[harness-engineering]] 是理解 Deep Agents 的主入口。
- [[multi-agent-delegation]]、[[agent-memory-patterns]]、[[agent-approval-patterns]] 在 Deep Agents 中都有明确实现映射。
- [[agent-sandboxing]]、[[agent-readable-repositories]]、[[pluggable-agent-backends]] 也能从 Deep Agents 的 filesystem / backend / permission 设计里得到补强。

## 来源
- [[langchain-deepagents-overview-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[harrison-chase-x-post-2042978500567609738-2026-04-15]]
