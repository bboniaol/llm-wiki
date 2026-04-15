---
title: Agent-readable Repositories
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, context-engineering, workflow, documentation, tooling, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md]
---

# Agent-readable Repositories

## 定义
agent-readable repository 指一种专门为智能体导航、检索、验证和修改而组织的代码仓库。它要求关键知识以本地、版本化、结构化的形式存在，使智能体无需依赖聊天记录、Google Docs 或人的隐性记忆，就能在仓库内完成推理和执行。

## 文章中的具体做法
- 用短小的 `AGENTS.md` 作为目录，而不是百科全书。
- 在 `docs/` 中维护结构化知识库，包含架构文档、设计文档、执行计划、产品规格、参考资料、质量与可靠性规则。
- 计划、决策日志和技术债务都进入仓库，成为智能体可追溯的上下文。
- 通过 lint、CI 和专门的 doc-gardening agent 检查文档新鲜度、交叉链接和结构正确性。
- LangChain 这篇文章则从更底层解释了为什么仓库这么重要：filesystem 是最基础的 harness primitive，agent 需要靠它读代码、存中间产物、跨 session 持久化状态，还能作为多 agent / 多人协作的共享账本。
- Sarah Wooders 这条原帖再补了一个更偏 memory 的视角：如果记忆最终要通过 `AGENTS.md` / `CLAUDE.md`、prompt rewriting、external state 与 compaction 策略进入上下文，那么 repo / filesystem 不只是存档层，而是 memory 被 harness 组织和重写的主战场。Letta 甚至把 agent memory 投影到 git-backed filesystem，并允许 background memory subagents 并发维护，这说明“仓库可读”正在向“仓库可承载记忆”演化。
- Karan 的实现帖则给了一个更草根但很实用的补充：`.md` / readme files 被直接当成 agent brain，强调其易读、可迁移、可跨平台复用。这说明 agent-readable repository 不只是大型文档体系，也可以从高杠杆 markdown 工件开始。
- NLAH 论文则把这条线再往前推了一步：自然语言工件不只承载说明书，还可以直接承载 harness logic 本身。contracts、roles、stages、state semantics 和 failure taxonomy 都能被写成可执行文本对象，这让 repo 内的文本工件第一次更明确地接近 control plane。

## 为什么重要
对智能体而言，“上下文里拿不到的东西就等于不存在”。因此，仓库如果不能直接承载关键知识，智能体就会在错误、不完整或过期的信息上工作。这也是 [[harness-engineering]] 中“代码仓库是记录系统”的核心理由。LangChain 进一步强调，filesystem 之所以重要，不只是因为方便存文件，而是因为模型本身已经在海量训练语料里“学会了如何和文件系统打交道”，因此它天然是 agent 最顺手的 durable interface。

## 设计原则
- 给智能体的是地图，不是巨型说明书。
- 采用渐进式披露：先给稳定入口，再引导到更深层文档。
- 把规则尽量编码成可验证结构，而不是散落在人类口头约定中。
- 让文档和代码一起接受版本控制、lint 和持续修剪。
- 把 repo 当成协作面，而不只是代码存储面：多 agent、人类 reviewer、CI 和 hooks 都可以围绕共享文件工作。

## 关联
- [[harness-engineering]] 依赖 agent-readable repository 作为上下文底座。
- [[codex]] 在文章中直接消费仓库内的文档、计划、脚本和反馈。
- [[langchain]] 的拆法说明，repo / filesystem 其实是很多 harness primitive 的共同底座。
- [[agent-memory-patterns]] 里的工件记忆，大多最终都要落回 repo / filesystem。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
- [[nlah-arxiv-html-2603-25723-2026-04-15]]
