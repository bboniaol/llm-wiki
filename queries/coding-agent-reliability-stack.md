---
title: Coding Agent Reliability Stack
created: 2026-04-14
updated: 2026-04-14
type: query
tags: [query-note, reliability, harness-engineering, workflow, best-practice, infrastructure]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# Coding Agent Reliability Stack

## 问题
如果你要把“coding agent 怎么稳定落地”压成一张方法地图，最小可用的 reliability stack 应该长什么样？

## 短答案
基于 [[harness-engineering]]、[[context-engineering]]、[[agent-reliability-patterns]]、[[long-running-agent-tasks]]、[[in-process-harness-vs-event-driven-harness]] 和 [[deterministic-backpressure-vs-durable-retries]]，一个实用的 coding agent reliability stack 可以分成六层：

1. 上下文层
2. 工具/权限层
3. 验证层
4. 状态与恢复层
5. 编排层
6. 组织治理层

不是每个团队一开始都要六层拉满，但出问题时基本都能映射回这六层中的某一层缺失或失衡。

## 六层结构

### 1. 上下文层
目标：让 agent 拿到最小但高信号的上下文，而不是一开局被垃圾信息灌满。

关键机制：
- [[context-engineering]]
- [[progressive-disclosure]]
- 短小高信号的 `CLAUDE.md` / `AGENTS.md`
- context firewall 式 [[multi-agent-delegation]]
- compaction / note-taking / just-in-time retrieval

如果这一层做不好，系统表现通常是：
- agent 看错任务
- tool 用错
- 很快 context rot
- 任务越做越飘

### 2. 工具 / 权限层
目标：让 agent 既有足够能力推进任务，又不至于乱动。

关键机制：
- [[agent-approval-patterns]]
- [[agent-sandboxing]]
- tool selection / MCP 控制
- rules / permissions / allowlists / hooks

如果这一层做不好，系统表现通常是：
- 不是能力不足，而是风险失控
- 或者反过来，什么都要人工点，吞吐量直接归零

### 3. 验证层
目标：让 agent 能看到高信号反馈，而不是靠“我觉得差不多了”。

关键机制：
- [[agent-feedback-loops]]
- [[evaluator-driven-qa]]
- [[deterministic-backpressure-vs-durable-retries]] 里的 deterministic backpressure
- tests / lint / contract / structured failure signals
- failFast / success 极简 / failure 展开

如果这一层做不好，系统表现通常是：
- agent 频繁虚假完工
- 大量 PASS 日志淹没真正失败点
- 模型稳定地误判结果

### 4. 状态与恢复层
目标：让任务可以接棒、续跑、恢复，而不是一断就从头开始。

关键机制：
- [[agent-memory-patterns]]
- [[repo-as-system-of-record]]
- progress files / feature lists / notes / git history
- [[long-running-agent-tasks]]
- durable state / resumability

如果这一层做不好，系统表现通常是：
- 每次新会话都像失忆
- 长任务恢复成本高
- 中断一次，前面大量工作白做

### 5. 编排层
目标：把单次 agent 能力提升成可持续运行的 agent system。

关键机制：
- [[in-process-harness-vs-event-driven-harness]]
- event-driven orchestration
- step-level retries / durable execution
- sub-agent invocation / task routing
- singleton concurrency / queueing / traces

如果这一层做不好，系统表现通常是：
- agent 在单轮里还行，但一到多步长链路就脆
- 后台任务难追踪、难恢复、易冲突

### 6. 组织治理层
目标：让 agent 不只是“能跑”，还要可审计、可协作、可规模化。

关键机制：
- [[agent-observability]]
- artifacts / traces / screenshots / logs
- audit / hooks / compliance logging
- service identity / shared controls / team rules
- [[cloud-agent-operations]]

如果这一层做不好，系统表现通常是：
- 小团队玩具能跑，大团队不敢用
- 事故后找不到证据
- 无法把 agent 从个人工具升级成团队系统

## 一个更实用的阅读顺序
如果你不是在搭完整平台，而是在救一个“已经不好用的 coding agent”，推荐按这个顺序排查：

1. 先看上下文层
   - 是不是 instruction budget 爆了
   - 是不是工具、规则、日志太吵
2. 再看验证层
   - 是不是结果信号太差，导致 agent 总在误判
3. 再看工具/权限层
   - 是不是能力不够或风险过高
4. 然后看状态与恢复层
   - 是不是每轮都在失忆或没法续跑
5. 最后看编排层和组织治理层
   - 当你已经需要后台长期运行、团队协作、审计合规时，再把系统往这两层抬

## 一条经验法则
- 小团队 / 本地交互式 coding agent：通常先把前 1-4 层做好
- 后台 agent / 组织级 agent 平台：6 层都会变重要

所以最常见的失败，不是“没上最高级架构”，而是：
- 该先补上下文和验证时，直接去上编排平台
- 或者已经在跑长链路后台 agent，却还停留在单会话思维

## 结论
- [[from-local-coding-agent-to-team-agent-platform]] 则从“时间顺序 / 演进路线”角度补上了同一套能力该如何逐层长出来。
coding agent reliability 不是一个技巧，而是一套分层系统。真正稳定的 agent，不是只靠更强模型，而是靠：
- 高信号上下文
- 受控工具与权限
- 清晰验证信号
- 可恢复状态
- 可靠编排
- 可审计治理

这六层一起，基本就是当前这套 wiki 里已经浮现出来的 reliability stack。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-writing-a-good-claude-md-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
