---
title: "Sub-Agents vs Agent Teams: The Architecture Decision That Changes Everything"
author: Suryansh Tiwari
source_url: https://x.com/Suryanshti777/status/2047694444787577236
captured_at: 2026-04-25
---

# Sub-Agents vs Agent Teams

## 核心观点

大多数人在任务变复杂时第一反应是"用多 Agent 系统"，这通常是错的。

真正该问的不是"要不要多个 Agent"，而是"这个任务实际上需要什么协调方式"。

## Sub-Agents：并行隔离

- 独立的上下文实例，类似"委派"
- 每个 sub-agent 有：角色定义、有限工具集、完全隔离的上下文、单一明确任务
- 完成后只返回最终输出，不包含推理过程
- **约束**：不能互相通信、不能 spawn 新 agent、所有信息流回 parent
- **本质**：compression，把混乱探索变成干净信号

## Agent Teams：协作通信

- 为协作设计，agent 间保持上下文、实时通信、自适应
- 结构：lead agent（分配+综合）+ teammates（执行）+ shared task layer（追踪进度和依赖）
- **本质**：coordination，frontend agent 可以信号 backend 变化

## 核心差异

| | Sub-Agents | Agent Teams |
|---|---|---|
| 焦点 | 执行 | 协作 |
| 状态 | 无状态 | 持久 |
| 交互 | 一次性 | 持续 |
| 控制 | Parent 控制 | 点对点 |
| 上下文 | 隔离 | 共享 |

## 常见错误

按角色拆分（planner / developer / tester）会导致每次交接都丢失上下文。

更好的方式是**基于上下文边界拆分**：如果两个任务共享深层上下文，放在同一个 agent 里；只有当上下文能干净分离时才拆分。

## 5 个关键模式

1. Prompt chaining — 顺序步骤
2. Routing — 任务路由到正确 agent
3. Parallelization — 独立任务并行
4. Orchestrator–worker — 一个 agent 委派
5. Evaluator–optimizer — 生成+精炼

## 何时不用多 Agent 系统

- 任务简单时
- Agent 间高度依赖时
- 协调开销过高时

## 最终原则

围绕**上下文边界**设计，而不是角色。从简单开始，只在需要时增加复杂度。
