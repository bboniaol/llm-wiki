---
title: Harness Engineering System Map
created: 2026-04-15
updated: 2026-04-25
type: query
tags: [query-note, harness-engineering, system-map, best-practice]
sources: [queries/agent-architecture-system-map.md]
---

# Harness Engineering System Map

> **注意**：本文档是 **Agent 架构十层地图的工程子集**，聚焦 harness engineering 的八层实践体系。
> 
> 如需完整视角（含理论根基层、多 Agent 编排层），请阅读 [[agent-architecture-system-map]]。

---

## 一句话总结

Harness engineering 不是"给模型加几个工具"，而是把 **context、state、verification、control、workflow、runtime、governance** 串成一个能长期工作的系统。

---

## 八层结构（精简版）

```text
Harness Engineering
├─ 1. 概念边界
│  ├─ [[framework-vs-runtime-vs-harness]]
│  ├─ [[harness-vs-context-vs-agentic-engineering]]
│  └─ [[harness-engineering]]
│
├─ 2. 事实底座
│  ├─ [[repo-as-system-of-record]]
│  ├─ [[agent-readable-repositories]]
│  └─ [[doc-gardening-agents]]
│
├─ 3. 上下文与记忆
│  ├─ [[context-engineering]]
│  ├─ [[progressive-disclosure]]
│  ├─ [[agent-memory-patterns]]
│  ├─ [[context-constitution]]
│  └─ [[long-running-agent-tasks]]
│
├─ 4. 执行边界与控制面
│  ├─ [[agent-sandboxing]]
│  ├─ [[agent-approval-patterns]]
│  ├─ [[agent-observability]]
│  └─ [[approval-vs-sandbox-vs-observability]]
│
├─ 5. 工作流与纠偏闭环
│  ├─ [[coding-agent-workflow-patterns]]
│  ├─ [[agent-feedback-loops]]
│  ├─ [[evaluator-driven-qa]]
│  ├─ [[multi-agent-delegation]]
│  └─ [[deterministic-backpressure-vs-durable-retries]]
│
├─ 6. 稳定性与评测
│  ├─ [[agent-reliability-patterns]]
│  ├─ [[coding-agent-evals]]
│  ├─ [[coding-agent-reliability-stack]]
│  ├─ [[minimum-viable-agent-harness-checklist]]
│  └─ [[how-to-read-agent-harness-benchmarks]]
│
├─ 7. 平台化与组织化
│  ├─ [[cloud-agent-operations]]
│  ├─ [[from-local-coding-agent-to-team-agent-platform]]
│  ├─ [[coding-agent-org-design-patterns]]
│  ├─ [[coding-agent-governance-checklist]]
│  ├─ [[coding-agent-maturity-model]]
│  ├─ [[managed-harness-vs-open-harness]]
│  └─ [[three-platform-archetypes-for-coding-agents]]
│
└─ 8. 前沿演化
   ├─ [[natural-language-agent-harnesses]]
   ├─ [[intelligent-harness-runtime]]
   ├─ [[extreme-harness-engineering]]
   ├─ [[symphony]]
   └─ [[entangled-software]]
```

---

## 每层一句话

| 层 | 核心问题 | 关键页面 |
|---|---------|---------|
| 1. 概念边界 | "你到底在谈哪一层？" | [[framework-vs-runtime-vs-harness]] |
| 2. 事实底座 | "Agent 依据什么活着？" | [[repo-as-system-of-record]] |
| 3. 上下文与记忆 | "别把窗口当垃圾堆" | [[context-engineering]] |
| 4. 执行边界 | "有能力不等于有边界" | [[agent-sandboxing]] |
| 5. 工作流纠偏 | "从一次回答变成可持续推进" | [[coding-agent-workflow-patterns]] |
| 6. 稳定性评测 | "系统强不强，不能靠感觉" | [[agent-reliability-patterns]] |
| 7. 平台组织 | "从个人外挂变成团队系统" | [[cloud-agent-operations]] |
| 8. 前沿演化 | "接下来往哪长" | [[natural-language-agent-harnesses]] |

---

## 学习顺序

**快速路径**（已有 [[agent-architecture-system-map]] 时）：
1. 直接读 [[agent-architecture-system-map]] 的 Day 1-7 完整路线
2. 本文作为"工程层速查表"，需要快速定位某层时翻查

**单独使用本文时**：
1. 先读 [[harness-engineering]] 总定义
2. 按 1→8 层顺序，每层选 1-2 个核心页面深入
3. 最后读 [[coding-agent-reliability-stack]] 和 [[minimum-viable-agent-harness-checklist]] 做总结

---

## 关联页面

- [[agent-architecture-system-map]] — 完整十层地图（含理论根基 + 多 Agent 编排）
- [[harness-engineering-7-day-study-plan]] — 按天执行的详细学习路线
- [[harness-engineering]] — Harness engineering 总定义页

## 来源

- [[queries/agent-architecture-system-map.md]]
