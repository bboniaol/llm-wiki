---
title: Harness vs Context vs Agentic Engineering
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, harness-engineering, context-engineering, agentic-engineering, workflow, best-practice]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md]
---

# Harness vs Context vs Agentic Engineering

## 为什么要区分
这三个词经常被混用，但如果不区分，讨论很容易失焦：有时团队谈的是上下文注入，有时谈的是智能体工作流，有时谈的是保证整个系统可靠运行的支架。基于 [[openai]]、Anthropic 和 [[langchain]] 的材料，现在可以把三者的边界讲得更清楚。

## 对比表
| 维度 | [[context-engineering]] | [[agentic-engineering]] | [[harness-engineering]] |
|---|---|---|---|
| 核心问题 | 给智能体什么信息，怎么组织、裁剪、压缩和注入 | 让智能体在流程中承担什么角色，如何协作执行 | 怎样搭建环境、约束和反馈回路，让智能体长期稳定工作 |
| 主要对象 | 上下文、文档、检索、记忆、工具返回、消息历史 | 任务流、角色分工、工具调用、审批与恢复 | 运行环境、验证机制、可观测性、结构约束、记录系统、hooks |
| 关注重点 | 信息是否正确、最新、分层、可导航、token-efficient | 智能体是否能端到端推进任务 | 智能体输出是否可靠、可控、可维护 |
| 常见产物 | AGENTS.md、docs 索引、知识地图、检索策略、compaction、notes | agent workflow、任务拆解规则、审查链路、角色分工 | 可观测性接入、结构测试、lint、sandbox、反馈闭环、handoff artifacts、tool routing |
| 失败模式 | 信息过载、缺上下文、知识腐烂、context rot | 执行链断裂、职责不清、恢复困难 | 高吞吐但不可控，代码漂移，系统熵增 |

## 一个直观理解
- [[context-engineering]] 像“给智能体准备地图、便签和检索入口”。
- [[agentic-engineering]] 像“设计智能体在团队里怎么干活”。
- [[harness-engineering]] 像“把赛道、护栏、仪表盘和维修系统搭起来”。

## 在现有案例里的映射
- 地图式 `AGENTS.md`、版本化 docs、compaction、note-taking、just-in-time retrieval，属于 [[context-engineering]]。
- 让 [[codex]] 自己开 PR、响应反馈、修构建、合并变更，或让 planner / generator / evaluator 分工协作，属于 [[agentic-engineering]]。
- 把 UI、日志、指标、追踪、架构边界、lint、sandbox、approval、tool routing、hooks 和垃圾回收循环接入系统，属于 [[harness-engineering]]。
- LangChain 那句“If you're not the model, you're the harness”虽然有点猛，但很适合提醒团队：很多被零散讨论的 runtime 细节，其实都属于 harness 范畴。

## 实践建议
1. 不要争论术语，先判断团队当前缺的是 actor、context 还是 harness。
2. 如果智能体总是“理解错任务”或上下文越来越脏，先补 [[context-engineering]]。
3. 如果智能体不能稳定推进跨步骤工作，先补 [[agentic-engineering]]。
4. 如果智能体产能很高但系统越来越乱，优先建设 [[harness-engineering]]。
5. 长任务通常三者都要：context 负责高信号信息流，agentic 负责角色协作，harness 负责可靠运行。

## 结论
三者不是互斥概念，而是同一类智能体工程问题的三个观察角度。真正落地时，通常是 [[agentic-engineering]] 定义执行者，[[context-engineering]] 提供认知输入，[[harness-engineering]] 保证整个系统可靠运行。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
