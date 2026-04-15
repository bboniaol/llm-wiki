---
title: Repo as System of Record
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, workflow, documentation, planning, context-engineering, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md]
---

# Repo as System of Record

## 定义
repo as system of record 指把代码仓库本身作为智能体时代最核心的事实来源，要求关键规则、文档、计划、架构、技术债、质量标准和决策痕迹都以本地、版本化、可链接的形式沉淀在仓库里，而不是散落在聊天、表格或人脑中。

## 在 OpenAI 案例中的体现
[[openai]] 在文章里明确强调：对智能体来说，看不到的东西就等于不存在。因此，他们没有把知识长期留在外部文档系统，而是把 `AGENTS.md`、`docs/`、执行计划、质量规则和技术债记录都放进仓库，让 [[codex]] 能直接检索、导航和修改。

## 为什么这是控制层而不只是文档层
当仓库成为 system of record 后，很多控制机制才有稳定落点：
- 审批规则可以版本化
- 计划和验收标准可以追踪
- 结构约束和 lint 可以自动执行
- 决策历史可以被未来智能体复用

这使 [[context-engineering]]、[[agentic-engineering]] 和 [[harness-engineering]] 不再依赖“谁还记得当初怎么约定的”。

## 设计原则
- 把高价值知识往仓库里收，而不是留在外部即时沟通里。
- 用索引、交叉链接和分层文档做渐进式披露。
- 把规则尽量写成可验证、可执行、可审查的工件。
- 把计划、技术债和架构决策视为一等资产，而不是临时便签。

## 与相近概念的关系
- [[repo-as-system-of-record]] 是 [[agent-readable-repositories]] 的进一步强化说法，强调“仓库是事实边界”。
- 它直接支撑 [[context-engineering]]，因为上下文必须有稳定来源。
- 它也支撑 [[agent-approval-patterns]]，因为批准规则和决策需要落地留痕。
- 在 [[harness-engineering]] 里，它承担的是知识与控制信息的持久化底座。

## 常见误区
- 只把代码放仓库，规则和计划仍然散落在外部。
- 文档虽在仓库里，但无人维护、无索引、无校验，最后一样腐烂。
- 把仓库当归档区，而不是运行中的控制与认知底座。

## 来源
- [[openai-harness-engineering-2026-04-14]]
