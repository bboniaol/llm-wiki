---
title: Context Constitution
created: 2026-04-15
updated: 2026-04-15
type: concept
tags: [concept, context-engineering, memory, best-practice, harness-engineering]
sources: [raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md]
---

# Context Constitution

## 定义
Context Constitution 是 [[letta]] 提出的一套面向 agent 的正式上下文治理原则。它关注的不是“如何写一句更好的 prompt”，而是 agent 应该把什么放进 context window、按什么顺序放、保留多久、以及怎样通过 external context 持续学习。

## 为什么它重要
这份文档把一个原本零散存在于记忆设计、agentfile、skills、compaction 和 repo 工件里的问题正式制度化了：context management 本身就是 experiential learning 的核心机制。也就是说，agent 的长期成长首先是上下文治理问题，而不是单纯模型升级问题。

## 这份文档补出的关键结构
- 把 context 直接解释成 identity、memory 与 continuity 的共同载体。
- 明确区分 context window 与 external context 两层，并把两者的治理关系写成正式原则。
- 明确列出 context primitives：system prompt、tools、messages、skills。
- 把 System Prompt Learning、[[progressive-disclosure]]、efficiency 提升到原则层，而不是实现细节。
- 给出一种更强的判断：如果 agent 明天换模型，它是否还能保持同一身份、同一记忆与同一行为边界。

## 它在当前知识库里的价值
在当前库里，[[context-constitution]] 像是把 [[context-engineering]] 从“最佳实践集合”推进成“规范性操作系统文档”。

它特别强化了几件事：
- [[agent-memory-patterns]] 不只是存储策略，而是 identity continuity 的设计问题。
- [[harness-engineering]] 不只是工具接线，而是如何把 context primitives、hierarchy 和 learning loop 编组成可持续系统。
- [[agent-readable-repositories]] 与外部文件系统不只是持久化容器，而是 context 被索引、引用、版本化和回收的主承载面。

## 我的阶段性判断
这份文档很有价值，但要区分两层：
- 作为判断框架，它很强：把 memory / identity / continuity / context scarcity 串成一整张图。
- 作为通用行业共识，它还不够中立：目前更像 Letta 路线的系统化宣言，而不是跨生态标准。

所以更稳的用法是：把它当成一套高分辨率框架，用来审视别的 agent harness 是否真的具备长期学习与记忆主权能力，而不是直接把它当作行业定论。

## 关联
- [[letta]] 是这套方法的提出者与产品载体。
- [[context-engineering]] 是理解这份文档的总入口。
- [[agent-memory-patterns]] 解释它为何把 memory 写成 context governance。
- [[progressive-disclosure]] 是它被正式原则化的一条操作方法。
- [[agent-readable-repositories]] 对应 external context 与 git-backed memory 的落盘面。

## 来源
- [[letta-context-constitution-blog-2026-04-15]]
- [[letta-context-constitution-constitution-md-2026-04-15]]
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
