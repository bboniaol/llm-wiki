---
title: Agent Memory Patterns
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, memory, context-engineering, workflow, best-practice, harness-engineering]
sources: [raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/claude-code-docs-memory-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/harrison-chase-x-post-2042978845347745871-2026-04-14.md, raw/articles/harrison-chase-x-post-2042978500567609738-2026-04-15.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md, raw/articles/ramp-labs-x-post-2042660310851449223-2026-04-14.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md]
---

# Agent Memory Patterns

## 定义
agent memory patterns 指智能体如何把“当前窗口里的短期状态”和“需要跨窗口/跨会话保留的长期信息”分层存储、更新和回收的一组设计模式。重点不是“让 agent 记住更多”，而是把该留的信息放到对的位置。

## 为什么它重要
智能体真正的问题通常不是完全没有信息，而是记忆放错了地方：短期状态留成长期噪音，长期规则只存在于聊天记录，关键决策没有沉淀。这样一来，[[context-engineering]] 会越来越脏，长任务也难以续跑。

## 典型分层
- 会话记忆：当前上下文窗口中的即时状态，最鲜活但最容易溢出。
- 工件记忆：repo 内的 TODO、进度文件、notes、spec、feature list、contract、日志。
- 规则记忆：`CLAUDE.md`、rules、instructions、团队约束。
- 托管记忆：平台提供的 memory / auto memory / 文件型记忆工具。

## Anthropic + LangChain 这条线补出的关键信号
- 在 long-running harness 里，`claude-progress.txt`、`feature_list.json`、`init.sh`、git history 承担的是“接棒型工件记忆”。
- 在 Claude Code 文档里，`CLAUDE.md` 与 auto memory 形成了“规则记忆 + 托管记忆”的产品化分层。HumanLayer 又补了一条很实用的边界：`CLAUDE.md` 是默认进入每次会话的高杠杆规则记忆，因此必须短、小、通用，而不是把所有细节都塞进去。
- 在 context engineering 文章里，structured note-taking 被明确列为长任务核心策略：把阶段性状态持续写到上下文窗口外，再在后续窗口回收。
- LangChain 那篇 blog 进一步强调，filesystem 是 memory 的底层 primitive：memory file 标准（如 `AGENTS.md`）会在 agent 启动时重新注入上下文，tool output 也可以被 offload 到文件系统，只有需要时再回读。
- [[deepagents]] 则把这件事进一步实现化：支持 long-term memory、LangGraph Memory Store、pluggable filesystem backends，以及用 write_todos 和文件系统工具来持续管理阶段性状态。
- Harrison Chase 最近那条短帖把一个经常被拆开的概念重新并回来了：如果 memory 本质上就是 context，那么 memory design 其实是在定义 harness 如何组织和回收上下文，而不是给系统外挂一个“记忆插件”。
- Sarah Wooders 的原帖把这件事再往下拆了一层：真正决定 memory 体验的，不只是有没有一个 memory store，而是 harness 如何注入 `AGENTS.md` / `CLAUDE.md`、如何展示 skill metadata、compaction 后保留什么、怎样暴露 filesystem 与当前工作目录。这些 invisible decisions 都在 harness 里，而不在外接插件里。
- 同一条帖还用 MemGPT / Letta 的脉络提醒了一点：很多被市场叫作“memory 产品”的东西，本质上其实是 stateful agent harness；memory 来自 prompt rewriting、external state management 与 context management 的联合作用，而不是单独一层检索服务。
- Letta 的 Context Constitution 和公开 `CONSTITUTION.md` 把这种立场进一步正式化：memory 不只是“保存旧信息”，而是 context as identity、context as memory、context as continuity 的联合治理；agent 要主动决定哪些 token 常驻、哪些下沉到 external context、以及怎样通过 system prompt learning 把经验回写到自己身上。
- Karan 这条更实现导向的短帖则补了一个很实操的分层：CLI 侧用 SQLite 保持本地持久会话，UI 侧用 Redis 做交互层状态，follow-up session 显式复用既有 history / memory / latest result。这说明 memory pattern 不一定先长成理论框架，也可以先长成一套多界面、多会话的状态续接机制。
- 同一条帖还把“memory ownership”这个商业与架构问题讲透了：stateful API、server-side compaction、closed harness、provider-hosted long-term memory，都会把记忆形状、迁移路径和运行经验一起锁在供应商那边。也就是说，memory pattern 不只是检索与存储策略，还是 provider optionality 的边界。
- Ramp Labs 的 Latent Briefing 则提示了另一条前沿方向：多 agent 场景里的“共享记忆”未必总是文本摘要，也可能是更底层、更压缩的表示层传递，目的是在不爆 token budget 的前提下把有效上下文交给下游 worker。
- memory 的目的不是无限囤积，而是让主上下文保持高信号，同时保证关键状态可回放。
- 频繁 compaction 产生的 research note、plan、summary 其实也是记忆工件：它们替代了把整段旧上下文原样拖入下一轮。

## 设计原则
- 把“规则”“状态”“证据”分开放，不要混在一个巨型文件里。
- 让长期记忆尽量版本化、可审计、可被 agent 重新读取。
- 只要可能，就把 memory 数据面与 harness 控制面做成可迁移对象；否则“记忆”很容易退化成 provider lock-in 机制。
- 会话窗口只保留当前决策真正需要的内容，其余信息沉淀到工件。
- 记忆文件要有明确职责：todo 管待办，progress 管阶段状态，spec 管目标边界，rules 管行为约束。
- 记忆是为了服务 [[context-engineering]]，不是为了制造新的上下文垃圾。
- 长期规则记忆要遵守 [[progressive-disclosure]]：让根文件负责导航，把低频细节留在更深层文档或技能里。
- 对长输出和大工具结果，要优先 offload 到 filesystem，再按需回读，不要硬塞满上下文窗口。

## 与相近概念的关系
- [[agent-memory-patterns]] 是 [[context-engineering]] 的持久化部分。
- [[repo-as-system-of-record]] 解决记忆的事实边界问题。
- [[long-running-agent-tasks]] 是最依赖 memory patterns 的场景。
- [[multi-agent-delegation]] 中，不同角色也需要共享或隔离不同层级的记忆。
- [[agent-readable-repositories]] 提供 memory 落盘的主要承载面。

## 常见误区
- 把所有记忆都塞进 system prompt。
- 让 agent 自己随意改目标定义文件，而不是只更新状态字段。
- 长期文件只增不减，最后变成新的上下文污染源。
- 把历史聊天当成唯一记忆系统。

## 来源
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[claude-code-docs-memory-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
- [[harrison-chase-x-post-2042978500567609738-2026-04-15]]
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
- [[letta-context-constitution-blog-2026-04-15]]
- [[letta-context-constitution-constitution-md-2026-04-15]]
- [[karan-x-post-2043618895328932340-2026-04-15]]
