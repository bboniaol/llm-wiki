---
title: CrewAI
created: 2026-04-15
updated: 2026-04-15
type: entity
tags: [company, framework, workflow, harness-engineering, agentic-engineering]
sources: [raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md]
---

# CrewAI

## 它是什么
CrewAI 是 João Moura 推动的一条多 agent / workflow / harness 路线。在这条帖子里，它不是以“某个具体 benchmark 赢家”出现，而是作为一条亲历 framework → scaffold → harness 术语演化的建设者视角出现。

## 当前在库中的关键信号
- João Moura 明确把 CrewAI 自己的两层结构说开了：
  - framework: CrewAI Flows
  - harness: CrewAI Crews and Agents
- 在他的表述里，CrewAI 的 harness 已经内建 memory、tools、caching、context engineering、prompts、skills、MCP 等能力。
- 他同时给出一个对自身赛道不算讨巧、但很有辨识度的判断：harness 也会像 framework 一样被快速 commodity 化。
- 所以 CrewAI 现在试图往“更高于 harness”的平台层推进，也就是让 agents 随客户流程、数据与使用模式持续适配，而不是停留在静态配置工具层。

## 它在知识库中的位置
[[crewai]] 当前最值得记录的，不是某个具体 API，而是它提供了一种来自赛道建设者内部的判断：即便你自己同时拥有 framework 与 harness，两者也未必是最终防御层。真正长期可防御的东西，可能在 [[entangled-software]] 所代表的 customer-specific adaptation、trust 与 usage flywheel 上。

## 关联
- [[harness-engineering]] 是理解 CrewAI 这条路线如何定义“harness”的入口。
- [[agentic-engineering]] 解释它为什么会把 agent 系统看成平台化工作流层，而不只是工具库。
- [[entangled-software]] 是 João Moura 在这条帖子里提出的下一层概念。

## 来源
- [[joao-moura-x-post-2043726271449112776-2026-04-15]]
