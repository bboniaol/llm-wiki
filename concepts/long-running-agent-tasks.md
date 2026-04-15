---
title: Long-running Agent Tasks
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, workflow, reliability, automation, orchestration, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md]
---

# Long-running Agent Tasks

## 定义
long-running agent tasks 指需要智能体持续执行较长时间、跨多个反馈周期甚至跨多个 context window 才能完成的任务，例如复杂 bug 修复、大范围重构、回归验证、文档清理和多轮审查响应。它们的难点不在单步能力，而在于如何在长时间跨度中保持目标一致、上下文稳定和恢复能力。

## 为什么它重要
[[openai]] 的文章提到，单次 [[codex]] 运行在单个任务上持续工作超过六小时并不罕见。Anthropic 之前那篇文章把问题拆成“跨 session 接棒”；应用开发那篇又往前推到“如何扩 spec、如何做独立 QA、如何动态简化 harness”。LangChain 这篇文章则从 primitive 角度补上了长任务为什么会难：agent 要在 context rot、tool output 膨胀、状态持久化、继续执行逻辑和自我验证之间持续平衡。也就是说，长任务本质上既是跨 session 连续性问题，也是上下文管理与执行循环设计问题。

## 核心挑战
- 上下文漂移：任务进行太久，最初意图和中间决策容易丢失。
- 状态丢失：重启、失败、超时后无法从中间状态恢复。
- 反馈延迟：验证结果来得太慢，导致错误放大。
- 人机切换成本：需要人工介入时，接手成本很高。
- 虚假完工：后续 agent 看到已有进展后，过早宣布“项目完成”。
- 模糊需求直接开工：如果只有一句 prompt，agent 很容易低估范围，最后做出“看起来像成品、但功能深度不够”的应用。
- context rot：随着窗口变长，推理质量和任务完成能力会逐步退化。

## 这些文章给出的关键做法
- 旧版 Anthropic harness：用 initializer agent 只负责首轮环境搭建，后续 coding agent 每次只做增量进展，并把环境收尾到“可继续接班”的干净状态。
- 新版 Anthropic harness：在长任务前再加一个 planner，把 1-4 句需求扩成完整产品 spec，减少 generator 一上来就低配实现的概率。
- 用 evaluator 和 generator 分离执行与评判：generator 负责构建，evaluator 负责用 Playwright MCP、测试标准和评分准则做独立 QA。
- 使用 `claude-progress.txt`、git history、feature_list.json、`init.sh` 或文件化 contract 这些工件承载状态与协作边界。
- LangChain 这篇文章补了另外几类 primitive：compaction、tool-output offloading、filesystem + git、planning + self-verification、以及 Ralph Loop 这类 continuation pattern，都是让 agent 在接近“想退出/想收工”时还能继续往前走的 harness 逻辑。
- HumanLayer 的 advanced context engineering 则把这件事 workflow 化：长任务不该等到快爆窗才处理，而要通过 frequent intentional compaction 和 sub-agents 持续把主线程维持在更高质量的上下文区间。
- 它的 backpressure 文章又补了一层执行细节：长任务里的测试/验证输出不能无脑灌回上下文，成功日志应极短，失败时再展开，否则很容易把 agent 赶出 smart zone。
- [[inngest]] 这篇文章则从执行底座补强了长任务恢复性：如果每次 think/tool 调用都是独立 step，那么第 5 轮死掉时，不必重跑前 4 轮；这把 durable execution 直接变成了长任务 harness 的一部分。

## 设计原则
- 用计划、决策日志和阶段性产物承载任务状态，别把一切寄托在会话上下文里。
- 把长任务拆成多个可验证阶段，每一段都能独立通过 [[agent-feedback-loops]] 检查。
- 对关键中间状态做持久化，依赖 [[repo-as-system-of-record]] 保存计划与进度。
- 为长任务准备恢复机制：失败可重试、中断可续跑、必要时可升级人工处理。
- 把 agent loop 拆成可重试的 step，比把整个会话写成一个不可恢复的 monolith 更稳。
- 让每次 session 都先“重新上岗”而不是立即编码。
- 不把 harness 结构当常量；模型能力变强后，应该重新判断哪些分段、重置和 QA 环节仍然值得保留。
- 把 continuation、compaction、offloading 这种“继续跑下去”的逻辑视为一等公民，而不是边角补丁。
- 对验证输出做 deterministic 压缩，别把长任务的上下文预算浪费在海量 PASS 日志上。

## 与相近概念的关系
- [[long-running-agent-tasks]] 是 [[coding-agent-workflow-patterns]] 在长链路场景下的强化版本。
- 它依赖 [[context-engineering]] 维持上下文新鲜度，也依赖 [[agent-observability]] 和 [[agent-feedback-loops]] 提供纠偏。
- [[agent-reliability-patterns]] 关注长期稳定性问题，而长任务是最容易暴露这些问题的场景。
- [[multi-agent-delegation]] 在这里不是“并行炫技”，而是 planner / builder / evaluator 这种职责分离。
- 这些文章也让 [[harness-engineering]] 更具体：harness 的很大一部分价值，就是为跨窗口接力和长链路应用开发提供结构化支架。

## 常见误区
- 把长任务当成放大版短任务处理，不做阶段化设计。
- 任务一旦中断，就只能从头开始。
- 只有最终结果，没有中间里程碑与状态记录。
- 让 agent 一开始就试图 one-shot 全项目，结果在半路耗尽上下文并留下脏状态。
- 以为 evaluator 永远都必须存在，忽略它的成本收益其实会随着模型能力边界变化。
- 以为长任务失败只是模型不够强，忽略 continuation、compaction、offloading、durable state 这些 harness 设计问题。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[humanlayer-advanced-context-engineering-2026-04-14]]
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
