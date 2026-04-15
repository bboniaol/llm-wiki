---
title: Letta
created: 2026-04-15
updated: 2026-04-15
type: entity
tags: [company, open-source, harness-engineering, context-engineering, memory]
sources: [raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md]
---

# Letta

## 它是什么
Letta 是一条明确押注“memory-first / experiential AI”的公司与产品路线。它不是把 memory 当作外挂模块，而是把 agent 的长期身份、连续性、自我改写能力和 context governance 一起打包成 harness/runtime 问题来处理。

## 当前在库中的关键信号
- Sarah Wooders 的原帖把 Letta 放在 MemGPT 脉络里，强调很多人以为是“memory plugin”的东西，本质上其实是 stateful agent harness。
- Letta 发布的 Context Constitution 把这套立场正式文档化：context management 被定义为 experiential learning 的核心机制。
- Letta Code 被描述为 memory-first coding harness，强调 persisted agent，而不是彼此独立的短会话。
- 官方 blog 明确把 Letta Code 的关键 affordances 说成：git-versioned memory filesystem、system prompt 读写、多会话 memory、以及利用 sleep-time compute 的 memory subagents。
- GitHub 上公开的 `CONSTITUTION.md` 进一步把 agent 的长期能力压成一套可执行的上下文治理原则，而不是停留在营销口号。

## 它在知识库中的位置
在当前库里，[[letta]] 的价值不是“又一个 agent 产品”，而是它把 [[agent-memory-patterns]]、[[context-engineering]] 和 [[harness-engineering]] 收束成一条更激进的命题：agent 的长期学习，主要发生在 token-space 的 context management 上，而不只是模型权重更新上。

## 关联
- [[context-constitution]] 是 Letta 当前最成体系的公开方法文档。
- [[agent-memory-patterns]] 解释了它为什么坚持 memory 不是插件。
- [[agent-readable-repositories]] 对应它的 git-backed memory filesystem 路线。
- [[progressive-disclosure]] 和 [[context-engineering]] 是理解其 context governance 的入口。

## 来源
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
- [[letta-context-constitution-blog-2026-04-15]]
- [[letta-context-constitution-constitution-md-2026-04-15]]
