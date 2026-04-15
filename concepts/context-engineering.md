---
title: Context Engineering
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, context-engineering, workflow, tooling, planning, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md]
---

# Context Engineering

## 定义
context engineering 指围绕“给智能体什么上下文、以什么结构给、在什么时候给”而进行的工程化设计。它关注的不是单次 prompt 文案，而是上下文的组织、裁剪、检索、分层、压缩和更新机制。

## 在当前知识库语境中的位置
基于 [[openai]] 的 harness engineering 案例，一个强结论是：智能体能否稳定完成复杂任务，很大程度上取决于它是否拿到了正确、最新、结构化、可执行的上下文。Anthropic 这篇文章则把这个概念正式讲清楚了：prompt engineering 主要处理“怎么写提示词”，而 context engineering 处理的是推理时刻整包 token 配置——包括 system instructions、tools、MCP、外部数据、message history 与运行中动态拉取的信息。

## 核心命题
上下文不是越多越好，而是要在有限 attention budget 内，找到“最小但高信号”的 token 集合。LLM 会随着上下文增长出现 context rot、注意力稀释和长距离依赖精度下降，因此 context 必须被当成稀缺资源管理，而不是无限缓存区。

## 关键问题
- 智能体应该先看到目录还是先看到全部细节？
- 哪些内容应进入长期版本化仓库，哪些只适合作为任务级临时上下文？
- 如何避免过长说明书挤占上下文窗口，反而削弱任务执行？
- 如何让上下文随着代码、设计和规则的变化持续更新，而不是快速腐烂？
- 哪些信息该预先放入上下文，哪些应让 agent 运行时按需检索？

## 典型做法
- 把 instruction budget 当成稀缺资源管理：不要默认 system prompt、agentfile、tool schema 越多越好。
- 用 [[progressive-disclosure]] 做上下文分层，只在需要时暴露更深说明、工具和案例。
- 用目录式入口代替巨型说明书，例如短小 `AGENTS.md` 指向更深层文档。
- 采用渐进式披露：先给地图，再按需展开设计文档、计划、规范和运行信号。
- 用 intentional compaction 周期性把高噪声上下文蒸馏成结构化工件，而不是一直拖着历史窗口往前跑。
- 把架构、计划、产品规格、技术债务和参考资料沉淀到本地、版本化的仓库中。
- Letta 的 Context Constitution 把这件事进一步制度化：context engineering 不只是“给模型喂上下文”，而是定义 identity、memory、continuity 怎样通过 context window 与 external context 被持续维护。
- 通过 lint、索引、交叉链接和文档巡检，降低上下文漂移与过期风险。
- system prompt 维持在“合适高度”：既不要硬编码脆弱流程，也不要空泛到默认模型会自己懂。
- 工具设计要 token-efficient、职责清晰，避免工具集合过大导致 agent 在选择上犹豫和浪费上下文。
- 用 canonical few-shot examples 代替把一堆边角规则塞进 prompt。
- 对大信息空间采用 hybrid context retrieval：少量关键内容 upfront，其余由 agent 通过工具 just-in-time 拉取。

## Anthropic 这篇文章补充出的三类长任务策略
1. Compaction
   - 把接近窗口上限的历史高保真压缩，再进入新窗口。
   - 关键不是“压短”，而是保住架构决策、未解决问题、实现细节，同时清掉冗余 tool outputs。

2. Structured note-taking
   - 让 agent 把阶段性状态写到上下文窗口外的持久工件里，例如 notes、todo、memory 文件。
   - 这让 [[agent-memory-patterns]] 成为 context engineering 的持久化部分，而不是附属功能。

3. Sub-agent architectures
   - HumanLayer 把它进一步讲透了：sub-agents 的核心价值是 context firewall。父线程只看到任务描述和压缩后的最终结果，不被中间搜索、日志和工具噪音淹没。
   - 让主 agent 保持高层计划，把高噪声探索交给独立上下文的 sub-agents。
   - 这本质上是在用 [[multi-agent-delegation]] 隔离上下文污染。

4. Frequent intentional compaction
   - HumanLayer 把这件事从技巧提升成 workflow：research / plan / implement 各阶段都主动压缩与重建上下文，尽量把上下文利用率维持在更安全的区间，而不是等到窗口爆了才被动清理。

## 与相近概念的关系
- [[context-engineering]] 解决的是“喂给智能体什么信息、怎么喂”的问题。
- [[agent-readable-repositories]] 是 context engineering 的重要载体，因为很多高价值上下文最终要落到仓库里。
- [[agent-memory-patterns]] 是它的持久化延伸，负责把信息放到窗口外但可回收的位置。
- [[context-constitution]] 则把这些实践提升成一套更接近规范文档的原则系统。
- [[harness-engineering]] 比它更大，除了上下文，还包含工具接入、反馈回路、验证机制与控制系统。
- 不过从 [[humanlayer]] 这条实践线看，很多 harness 杠杆本质上都是在做上下文治理：控制工具描述、规则注入、技能激活时机和子任务结果回流粒度。
- [[agentic-engineering]] 则更偏向把智能体作为系统参与者来设计整体工作流和组织边界。
- [[progressive-disclosure]] 可以视为它最实用的一条操作原则。

## 常见误区
- 把 context engineering 误解成“写更长的 prompt”。
- 只关注检索召回，不关注信息是否可信、是否最新、是否可执行。
- 把知识散落在聊天记录、文档平台和人脑里，却期望智能体自己补全缺失上下文。
- 一味把所有数据预加载进窗口，结果让 agent 淹死在低信号 token 里。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
