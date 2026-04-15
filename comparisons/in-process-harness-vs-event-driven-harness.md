---
title: In-process Harness vs Event-driven Harness
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, harness-engineering, infrastructure, workflow, reliability, best-practice]
sources: [raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# In-process Harness vs Event-driven Harness

## 为什么要区分
现在知识库里已经出现了两种明显不同的 harness 落地风格：
- 一类更像 [[humanlayer]] 代表的 in-process / local-session harness：重点放在 agentfile、上下文治理、sub-agents、hooks 和 back-pressure 上。
- 另一类更像 [[inngest]] 代表的 event-driven / durable orchestrated harness：重点放在 step orchestration、durable execution、event routing、retries 与 concurrency control 上。

两者都属于 [[harness-engineering]]，但关注的主战场不同。前者更像“把单次 agent 会话调教好”，后者更像“把 agent loop 放进可恢复、可编排、可观察的系统底座里”。

## 对比表
| 维度 | In-process Harness | Event-driven Harness |
|---|---|---|
| 典型代表 | [[humanlayer]] 式实践 | [[inngest]] 式编排 |
| 主要工作面 | 当前会话、当前仓库、当前上下文窗口 | 多 step 执行流、事件路由、后台任务、长期运行 |
| 关键杠杆 | `CLAUDE.md` / `AGENTS.md`、[[progressive-disclosure]]、sub-agents、hooks、back-pressure | durable execution、step retries、event routing、step traces、singleton concurrency |
| 最先解决的问题 | 上下文污染、instruction budget、工具暴露过多、验证输出过吵 | 长流程中断恢复、任务碰撞、后台执行稳定性、可追踪性 |
| 子代理实现重点 | context firewall，压缩结果回流父线程 | `step.invoke()` 等独立函数运行，子代理自带 retries 与 observability |
| 失败模式 | 模型能跑但越来越笨，上下文越来越脏 | 系统能调度但 agent 本身上下文/工具设计很差，仍然做不好任务 |
| 更像在优化 | agent session 质量 | agent system 可恢复性与编排能力 |

## In-process Harness 什么时候更强
- 你首先遇到的问题是：agent 总是看错上下文、拿错工具、被长输出淹没。
- 任务主要发生在本地交互式 coding session 中。
- 你要优先解决 instruction budget、context rot、agentfile 设计、工具暴露和验证噪音。
- 这时 [[humanlayer]] 这条线通常杠杆更高：先把当前 agent 会话调干净，比先上复杂编排更值。

## Event-driven Harness 什么时候更强
- 你首先遇到的问题是：任务很长、容易中断、需要后台运行、需要重试恢复和并发治理。
- 你想把 think → act → observe loop 拆成 durable steps，而不是一个长函数或长会话。
- 你需要 step-level traces、job queue、event routing、singleton concurrency 这类系统能力。
- 这时 [[inngest]] 这条线更强：问题已经不是“会不会用 agent”，而是“能不能把 agent 系统化托管起来”。

## 两者不是二选一
最成熟的系统往往会把两者叠起来：
1. 用 in-process harness 把 agent 本身调顺
   - 高信号 agentfile
   - [[progressive-disclosure]]
   - context firewall 式 sub-agents
   - deterministic back-pressure
2. 再用 event-driven harness 把 agent loop 托管起来
   - step-level retries
   - durable execution
   - event routing
   - 并发与恢复控制

也就是说，前者决定“agent 会不会在单次任务里发飘”，后者决定“这个 agent 系统能不能长期稳定跑”。

## 一个实用判断法
- 如果你现在最痛的是上下文、工具、记忆和噪音，先补 in-process harness。
- 如果你现在最痛的是恢复、编排、重试、追踪和后台运行，先补 event-driven harness。
- 如果两边都痛，通常先把前者补到及格线，再把后者接上；不然只是把一个糟糕 agent 放进更贵的编排系统里。

## 结论
in-process harness 和 event-driven harness 都不是“谁替代谁”，而是 agent engineering 的两个层次：
- 前者更接近 [[context-engineering]] 和会话内控制
- 后者更接近 workflow infrastructure 和 durable orchestration

真正成熟的 harness，通常不是只会其中一边，而是知道什么时候该优化会话，什么时候该升级编排底座。

## 来源
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
