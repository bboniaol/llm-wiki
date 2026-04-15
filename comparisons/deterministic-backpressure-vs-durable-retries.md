---
title: Deterministic Backpressure vs Durable Retries
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, reliability, harness-engineering, workflow, infrastructure, best-practice]
sources: [raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# Deterministic Backpressure vs Durable Retries

## 为什么要区分
这两个词都在解决“agent 为什么会失败”，但解决的不是同一层问题：
- deterministic backpressure 更关注：如何让 agent 在当前执行轮里更容易看清楚结果、验证结果、不要被噪音淹没。
- durable retries 更关注：如果某一轮或某一步失败了，系统如何恢复、重试、继续，而不是整段流程从头来过。

一句话说：
- backpressure 偏“让 agent 不要看错”
- durable retries 偏“就算这次失败也能接着跑”

## 对比表
| 维度 | Deterministic Backpressure | Durable Retries |
|---|---|---|
| 代表线索 | [[humanlayer]] | [[inngest]] |
| 主战场 | 当前会话 / 当前验证回路 | 长流程 / 多 step 编排 |
| 主要问题 | 输出太吵、验证信号太弱、agent 提前宣布完成 | 某一步挂掉后整段流程重跑、状态丢失、恢复成本高 |
| 核心手段 | success 极简、failure 展开、failFast、输出整形、deterministic summarization | step-level persistence、independent retries、event routing、durable execution |
| 作用对象 | agent 对结果的“可读性”与“可判断性” | 系统对失败的“恢复性”与“连续性” |
| 如果缺失 | agent 容易被 PASS 日志、长输出、噪音误导 | agent loop 一旦中断，前面已完成工作可能白做 |
| 更像在优化 | 认知负担 | 执行恢复能力 |

## Deterministic Backpressure 在解决什么
- 不让海量成功日志、长测试输出、无关 shell 输出污染上下文。
- 把“结果是否通过”压成高度结构化、可快速判断的信号。
- 尽量让 agent 一次只面对最关键的失败，而不是同时处理五个错误。
- 本质上是在提高 [[agent-reliability-patterns]] 里的验证信号质量。

HumanLayer 这条线给出的关键经验是：
- success 要尽量短
- failure 再展开
- failFast
- 不要把摘要权交给模型临场决定

## Durable Retries 在解决什么
- 把 think / act / observe 拆成独立、可持久化的步骤。
- 某一步失败时，只重试这一步，不重跑前面已经成功的步骤。
- 让长任务从“脆弱长循环”变成“可恢复执行图”。
- 本质上是在提高 [[long-running-agent-tasks]] 的续跑能力和系统恢复性。

Inngest 这条线给出的关键经验是：
- 每次 LLM 调用和 tool 调用都可以是 step
- step 可以独立重试
- 结果和状态可以持久化
- orchestration / retries / traces 应由系统底座承担

## 两者不是替代关系
一个常见误解是：
- “有 durable retries 了，就不需要 backpressure”
或者
- “我把输出压短了，就不需要恢复机制”

都不对。

因为：
1. durable retries 不能替你解决“agent 看不懂输出”
   - 你可以很稳定地反复重试一个糟糕、噪音巨大的验证回路
2. deterministic backpressure 也不能替你解决“流程中断后怎么续跑”
   - 你可以让当前轮很清晰，但一旦进程死了，还是可能前功尽弃

## 一个实用搭配方式
成熟系统通常会这样叠：
1. 先做 deterministic backpressure
   - 保证每一步验证结果高信号、低噪音、易判断
2. 再做 durable retries
   - 保证这些高信号 step 在失败时可恢复、可重试、可追踪

所以更准确的关系是：
- backpressure 提高每一步的判断质量
- durable retries 提高整个流程的恢复能力

## 什么时候先做哪一个
优先做 deterministic backpressure：
- 你现在的主要问题是测试输出太长、日志太吵、agent 经常看错结果
- 你的失败更多来自“判断失真”而不是“流程中断”

优先做 durable retries：
- 你现在的主要问题是任务太长、后台执行经常挂、恢复成本太高
- 你的失败更多来自“流程脆弱”而不是“验证信号太差”

如果两边都痛：
- 一般先把 backpressure 做到及格
- 再把 retries 接起来

否则你只是在非常稳定地重试一堆低质量信号。

## 结论
deterministic backpressure 和 durable retries 分别回答两个不同问题：
- agent 如何更清楚地看到结果
- 系统如何在失败后继续前进

前者偏会话内验证质量，后者偏流程级恢复能力。两者一起上，才是更成熟的 [[harness-engineering]]。

## 来源
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
