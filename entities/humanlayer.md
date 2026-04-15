---
title: HumanLayer
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, harness-engineering, context-engineering, tooling, best-practice]
sources: [raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md]
---

# HumanLayer

## 它是什么
HumanLayer 是一家围绕 coding agent 实践、工作流与工具集成持续输出经验的团队/公司。在当前知识库里，它的重要性不在于“又一个 agent 产品”，而在于它用很强的实战口吻，把 harness engineering 拆成一组可操作的配置杠杆：agentfiles、skills、MCP、sub-agents、hooks 和 back-pressure。

## 这一组文章提供的独特价值
- 它把很多 agent 失败首先归因为配置问题，而不是模型本身不够强。
- 它明确给出一个更偏实践派的定义：`coding agent = AI model(s) + harness`。
- 它把 [[harness-engineering]] 放进 [[context-engineering]] 视角下，强调 harness 的核心工作之一就是管理 instruction budget 与上下文污染。
- 它把 sub-agents 解释成 context firewall，而不是单纯并行器，这对 [[multi-agent-delegation]] 的边界很关键。
- 它把 hooks 与 back-pressure 提升为高杠杆配置面，说明可靠性不只来自更强模型，也来自更好的控制流与验证闭环。

## 关键主张
- `CLAUDE.md` / `AGENTS.md` 是最高杠杆的 harness 配置点之一，因为它会进入每一次会话。
- 好的 agentfile 不是越长越好，而是越短、越通用、越高信号越好；HumanLayer 的经验是根 `CLAUDE.md` 控制在很短的范围内。
- `CLAUDE.md` / `AGENTS.md` 应该短、通用、可指路，不该写成巨型说明书。
- Skills 的价值在于 [[progressive-disclosure]]：按需暴露知识、说明和工具，而不是开局把所有东西塞进 system prompt。
- MCP 主要是工具接入层，但过多工具会吞掉 instruction budget，甚至形成 prompt injection 面。
- Sub-agents 最重要的价值是上下文隔离、上下文压缩和成本分层，不只是角色扮演。
- Hooks 适合做自动化控制流与外部集成；back-pressure 则让 agent 更容易验证自己的工作是否真的完成。
- advanced context engineering 进一步把 HumanLayer 这条线推向 workflow 级：通过 intentional compaction、sub-agents 和 research/plan/implement 流程，把复杂 brownfield 任务持续维持在“smart zone”。
- context-efficient backpressure 则把验证机制做得更具体：输出要尽量 deterministic、成功日志要极简、失败时再放大、并尽量启用 failFast。

## 关联
- [[deterministic-backpressure-vs-durable-retries]] 对比了 HumanLayer 代表的验证信号治理，与 durable orchestration 恢复机制的差异。
- [[in-process-harness-vs-event-driven-harness]] 对比了 HumanLayer 代表的实践型 / 会话内 harness 与编排型 harness 的差异。
- [[harness-engineering]] 是理解 HumanLayer 这篇文章的主入口。
- [[context-engineering]] 解释了它为什么反复强调 instruction budget、progressive disclosure 与 context rot。
- [[multi-agent-delegation]] 能直接吸收它关于 sub-agents = context firewall 的判断。
- [[agent-reliability-patterns]] 能直接吸收它关于 hooks 与 back-pressure 的经验。

## 来源
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
