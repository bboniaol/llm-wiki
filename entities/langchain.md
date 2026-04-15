---
title: LangChain
created: 2026-04-14
updated: 2026-04-15
type: entity
tags: [company, open-source, harness-engineering, agentic-engineering]
sources: [raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/harrison-chase-x-post-2042978500567609738-2026-04-15.md]
---

# LangChain

## 它是什么
LangChain 是构建 LLM 应用、agent runtime 与相关工程基础设施的公司/开源生态。在当前知识库里，它的重要性不只是“又一家 agent 框架”，而是它开始明确用工程语言解释 harness engineering，把 harness 从一个口头黑话拆成可枚举的系统组件，并进一步给出 deepagents 这种具象实现载体。

## 当前在库中的重要信号
- 在《The Anatomy of an Agent Harness》中，把 harness 明确定义为“除了模型本身以外的所有代码、配置与执行逻辑”。
- 明确提出：Agent = Model + Harness，并把 state、tool execution、feedback loops、constraints、filesystem、sandbox、browser、subagent orchestration、hooks/middleware 都纳入 harness 范围。
- 强调 filesystem 是最基础的 harness primitive，memory file、skills、tool output offloading、git 历史和多 agent 协作都依赖它。
- 用 [[deepagents]] 作为其 harness 研究与实践载体，说明 LangChain 不只是做应用层调用封装，也在往 agent runtime / harness library 方向推进。
- deepagents overview 进一步说明，LangChain 想把 planning、subagents、filesystem、sandbox、permissions、memory、human approval 这些能力做成默认组合的 runtime，而不是让用户从零拼。
- 更进一步，deepagents 还把 backend 明确做成可插拔抽象，说明 LangChain 在思考的不是“如何给一个 agent 加功能”，而是“如何给 agent 提供可迁移的运行面”。
- Harrison Chase 2026-04-15 的帖子把这条路线从“工程抽象”升级成了“平台立场”：LangChain 不只是主张 harness 必然存在，还明确主张 memory ownership 应该留在开放 harness 一侧，否则 agent 体验的核心资产会被 provider API 吞掉。

## 在知识库中的位置
如果说 [[openai]] 提供了真实产品闭环案例，Anthropic 提供了长任务与 context/memory 方法论，那么 LangChain 这条线的价值更像“概念统一器 + 运行时实现者”：它既把 harness 的边界、组成和未来演化讲得抽象，又用 [[deepagents]] 把这些抽象落到可实现的 SDK / CLI 上。

## 关联
- [[harness-engineering]] 是理解 LangChain 这条线的主入口。
- [[deepagents]] 是 LangChain 在当前知识库里最直接的 harness 实现载体。
- [[pluggable-agent-backends]] 则是理解它 runtime 设计取向的一个新入口。
- [[agent-readable-repositories]]、[[agent-memory-patterns]]、[[agent-sandboxing]]、[[long-running-agent-tasks]] 都被这条线从底层 primitive 角度重新串了一遍。
- [[harness-vs-context-vs-agentic-engineering]] 可以借它来进一步澄清 harness 与 context 的关系。

## 来源
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
- [[harrison-chase-x-post-2042978500567609738-2026-04-15]]
