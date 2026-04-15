---
title: Progressive Disclosure
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, context-engineering, workflow, best-practice, harness-engineering]
sources: [raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md]
---

# Progressive Disclosure

## 定义
progressive disclosure 指不要在会话开始时把全部规则、工具、案例和细节一次性灌进智能体上下文，而是先给高层地图，再按任务需要逐步暴露更深的说明、工具和知识。

## 为什么它重要
在 coding agent 场景里，真正稀缺的不是原始知识总量，而是 instruction budget 和上下文清晰度。过早注入大量规则、tool schema、长篇 `CLAUDE.md` / `AGENTS.md` 或无关技能，只会更快把模型推向 [[context-engineering]] 里的信息过载与 context rot。

## 当前知识库里的共识
- [[langchain]] 把 skills 解释为 harness primitive，核心价值就是按需揭示知识和工具。
- Anthropic 的 context engineering 文章把它视为 agent 自主探索上下文的一种组织原则：先拿少量 upfront 信息，其余 just-in-time 获取。
- [[humanlayer]] 则把它落成操作规范：根 `CLAUDE.md` 要短、通用、只放高杠杆规则；更细的说明通过 skills、目录、引用文档和子任务结果按需进入上下文。
- Letta 的 Context Constitution 则把 progressive disclosure 直接写进原则层：主上下文保留索引和引用，细节通过 skills、external context 和按需读取进入，而不是默认常驻 system prompt。

## 典型做法
- 根 `CLAUDE.md` / `AGENTS.md` 只保留 universally applicable 的项目级规则。
- 把细分说明拆进 skills、子文档、目录索引和 example files，而不是常驻主提示。
- 让 sub-agents 只回传压缩结论和引用，不回传完整噪音过程。
- 对工具做裁剪和按需暴露，避免巨量 MCP/tool descriptions 在开局就吃掉上下文。

## 与相近概念的关系
- [[progressive-disclosure]] 是 [[context-engineering]] 的核心策略之一。
- 它也是 [[harness-engineering]] 的高杠杆配置原则，因为它决定了知识、工具和控制信息怎样进入系统。
- 它与 [[agent-memory-patterns]] 相连：长期记忆可以很多，但不等于每次都要全量加载。
- 它和 [[multi-agent-delegation]] 相连：子 agent 的价值之一就是把大过程压成小结果，再按需回流。

## 常见误区
- 把 progressive disclosure 误解成“信息藏起来不给模型”。
- 默认更多 instructions / 更多工具 / 更长 agentfile 一定更稳。
- 在主线程里保留所有搜索、日志和测试输出，最后让上下文被噪音淹没。

## 来源
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[letta-context-constitution-constitution-md-2026-04-15]]
