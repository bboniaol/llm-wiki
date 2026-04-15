---
title: Approval vs Sandbox vs Observability
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, workflow, security, observability, reliability, best-practice]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md]
---

# Approval vs Sandbox vs Observability

## 为什么要对比
这三者都属于智能体系统的“控制面”，但解决的是不同问题。很多团队一说“安全控制”就混成一团，结果最后要么全靠人工审批，要么只做隔离，要么只有监控图没有执行约束。把三者拆开，才能知道系统到底缺哪块。

## 对比表
| 维度 | [[agent-approval-patterns]] | [[agent-sandboxing]] | [[agent-observability]] |
|---|---|---|---|
| 核心问题 | 哪些动作需要人工确认 | 智能体能在什么边界内执行 | 我们如何看到智能体做了什么、哪里出了问题 |
| 主要作用 | 控制决策权 | 控制执行边界 | 控制可见性与诊断能力 |
| 典型机制 | 批准闸门、风险分级、人工介入点 | worktree、隔离环境、最小权限、受限工具 | 日志、指标、追踪、DOM 快照、执行记录 |
| 主要收益 | 降低高风险错误外溢 | 限制破坏范围 | 提高可诊断性、可审计性和纠偏效率 |
| 失败模式 | 全量审批导致吞吐崩塌 | 过度隔离导致无法完成真实任务 | 有监控没闭环，智能体和人都不会用 |

## 一个直观理解
- [[agent-approval-patterns]] 像闸机：决定谁什么时候能过去。
- [[agent-sandboxing]] 像围栏：决定即使过去了，能跑多远。
- [[agent-observability]] 像仪表盘和黑匣子：决定出了事能不能看明白。

## 工程建议
1. 不要只上审批，不做隔离和可观测性，那只是人工堵洪水。
2. 不要只上 sandbox，不做 observability，否则问题会被关进黑箱。
3. 不要只有 observability，没有 approval 与 sandbox，否则你只是在高清观看事故发生。
4. 最稳的方式是三者组合：批准控制高风险决策，沙箱限制执行范围，可观测性支撑诊断和反馈。

## 与更大框架的关系
- 三者一起构成 [[harness-engineering]] 的控制面核心。
- 它们共同支撑 [[coding-agent-workflow-patterns]] 的稳定执行。
- 其中 approval 更偏治理，sandbox 更偏隔离，observability 更偏证据与诊断。

## 结论
approval、sandbox、observability 不是替代关系，而是互补关系。一个成熟的智能体工程系统，应该同时回答三个问题：谁批准、在哪执行、如何看见。

## 来源
- [[openai-harness-engineering-2026-04-14]]
