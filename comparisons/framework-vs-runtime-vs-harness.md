---
title: Framework vs Runtime vs Harness
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, harness-engineering, agentic-engineering, infrastructure, best-practice, workflow]
sources: [raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# Framework vs Runtime vs Harness

## 为什么要区分
这三个词在 agent 圈里经常混着说，结果就是：有人以为“有个框架”就等于“有了可运行 agent”，有人把 runtime 当成 harness 本身，也有人把所有系统层问题都扔进 framework。LangChain / Deep Agents 这条线已经提供了一个很好的拆法；Inngest 这篇文章又从 workflow infra 角度补了一刀：framework 提供积木，runtime 提供执行底座，而 harness 还可能进一步吃进 durable orchestration、event routing 与 step-level observability 这类系统能力。

## 对比表
| 维度 | Framework | Runtime | Harness |
|---|---|---|---|
| 核心作用 | 提供构建模块和开发接口 | 提供执行、持久化、中断、流式等运行机制 | 把模型、工具、环境、约束、反馈组织成可工作的系统 |
| 关注重点 | 可组合性、开发体验、抽象 API | 生命周期、状态恢复、并发、执行控制 | 任务完成率、可靠性、安全性、长期运行效果 |
| 典型内容 | prompts API、tool wrappers、model adapters、graph DSL | durable execution、streaming、interrupt、memory store、step orchestration | filesystem、sandbox、browser、skills、permissions、verification loops、subagents、hooks、event routing、concurrency control |
| 回答的问题 | “怎么搭这个系统？” | “这个系统怎么跑起来并持续运行？” | “怎么让模型在真实任务里稳定交付结果？” |
| 失败模式 | 积木很多但拼不成可用 agent | 能跑但不会干活，或跑不稳 | 任务能跑一阵，但不可靠、不安全、不可维护 |

## 一个直观理解
- Framework 像零件箱。
- Runtime 像发动机和底盘。
- Harness 像整辆能上路、带护栏和仪表盘的车。

## 用 LangChain 这条线来映射
- [[langchain]] 更像 framework / 生态层：提供构建 agent 的核心 building blocks。
- LangGraph runtime（在当前库里主要通过 [[deepagents]] 间接出现）更像 runtime 层：负责 durable execution、interrupt、streaming、memory store 这些运行机制。
- [[inngest]] 这篇文章进一步说明：当 durable execution、event routing、step retries 和 traces 被直接用来承载 agent loop 时，runtime 与 harness 的边界会贴得更近，但依然不能混为一谈。
- [[deepagents]] 更接近 harness implementation：它把 planning、filesystem、subagents、permissions、human-in-the-loop、sandbox execution 等组合成一套默认可用的 agent harness。

## Harness 为什么不等于 Runtime
很多人会把“runtime 很强”误当成“harness 就完整了”，但这两者不是一回事：
- runtime 可以提供中断、持久化、流式执行
- 但 harness 还要决定：
  - 给模型什么工具
  - 在什么文件系统里工作
  - 有没有 sandbox
  - 怎么 compaction / offload
  - 怎么验证结果
  - 什么动作要 approval
  - 多 agent 如何协作

换句话说，runtime 偏“怎么运行”，harness 偏“让运行结果有用”；而 Inngest 这条线提醒我们，某些 runtime / workflow infra 能力一旦直接承载 agent loop，本身就会变成 harness 的骨架。

## Framework 为什么也不等于 Harness
framework 更像“可选零件仓库”。它当然可以帮助你搭 harness，但不会自动帮你解决这些问题：
- 任务怎么分解
- 上下文怎么管理
- 权限怎么约束
- 结果怎么验证
- 长任务怎么续跑
- 多 agent 怎么协同

所以同一个 framework 上，能长出很弱的 harness，也能长出很强的 harness。

## 一个实用判断法
- 如果你在讨论 API、抽象接口、集成方式，大概率在说 framework。
- 如果你在讨论 durable execution、interrupt、streaming、state persistence，大概率在说 runtime。
- 如果你在讨论 event routing、step retries、step traces、singleton concurrency 如何让 agent loop 稳定落地，往往已经踩到 harness 与 runtime 的交界处。
- 如果你在讨论 sandbox、filesystem、verification、skills、approval、subagents、feedback loops，大概率在说 harness。

## 为什么这页对你这套知识库重要
你这套库已经有三条不同类型的证据：
- [[openai]]：真实产品 harness 案例
- Anthropic：长任务 / context / evaluator-driven QA 方法论
- [[langchain]] / [[deepagents]]：framework / runtime / harness 的抽象与实现映射
- [[inngest]]：从 workflow infrastructure 角度证明 harness 可能比“agent runtime”更靠近系统编排层

把三层拆开之后，后面再看任何产品或框架，就不容易被 marketing 词带跑了。

## 常见误区
- 以为“有框架”就自动等于“有 agent 平台”。
- 把 runtime 能力吹成任务可靠性本身。
- 把 harness 的设计问题全部甩给模型能力。
- 讨论 agent 系统时不区分构建层、运行层、系统支架层，最后争论半天其实不在同一层。

## 结论
framework、runtime、harness 是三层不同抽象：framework 提供构建积木，runtime 提供执行机制，harness 负责把模型真正变成能工作的 agent 系统。真正成熟的 agent engineering，不是只会选模型或选框架，而是能在这三层上分别做对设计。

## 来源
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
