---
title: Coding Agent Workflow Patterns
created: 2026-04-14
updated: 2026-04-24
type: concept
tags: [concept, workflow, coding-agent, orchestration, best-practice, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/claude-code-docs-common-workflows-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/cursor-docs-agent-overview-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md, raw/articles/ltbase-harness-engineering-2026-04-24.md]
---

# Coding Agent Workflow Patterns

## 定义
coding agent workflow patterns 指在真实软件工程里，把代码智能体纳入需求理解、任务拆解、实现、验证、审查、修复与合并流程时，反复证明有效的一组工作流模板。它关注的不是单个技巧，而是整条执行链如何稳定运转。

## 为什么需要模式化
当团队开始依赖 [[codex]]、[[claude-code]]、[[cursor]] 这类智能体时，最大问题往往不是“它会不会写代码”，而是“它应该按什么流程推进工作”。如果没有稳定 workflow，智能体能力再强，也容易在上下文切换、验证缺失、反馈断裂和审查返工中耗散。[[harness-engineering]] 的一部分价值，就是把这些 workflow 固化成能重复跑的模式。

## 常见模式
### 1. 任务拆解 → 局部实现 → 本地验证
适合中小变更。先把需求拆成有限范围，再让智能体完成单次实现并本地跑测试或 UI 验证。

### 2. 复现问题 → 收集证据 → 实施修复 → 回归验证
适合 bugfix。智能体先借助 [[agent-observability]] 与浏览器/日志信号复现问题，再进入 [[agent-feedback-loops]]。

### 3. 计划驱动型执行
适合复杂任务。先写执行计划，再按阶段推进，降低长链路任务中途跑偏的概率。它和 [[context-engineering]]、[[repo-as-system-of-record]] 天然耦合。Claude Code 的 Plan Mode 与 Cursor 的 Plan / Debug 取向，都是这类 workflow 的产品化入口。

### 4. PR 驱动闭环
让智能体围绕 PR 生命周期工作：实现、开 PR、响应 review、修复构建、再次验证、等待批准或合并。这是 [[agentic-engineering]] 在代码协作里的典型形态。CircleCI 的案例则把这件事推进到了“task in, validated PR out”的闭环形态。

### 5. 跨窗口接棒型工作流
Anthropic 的长任务文章把这一模式讲得很具体：initializer agent 先铺环境，后续 coding agent 每轮只做一个 feature 的增量推进，并在 session 结束时写入 progress、commit 到 git、保持环境干净可接班。

### 6. 浏览器回路驱动型工作流
Cursor 的 browser tools 说明，很多前端 / 全栈工作流已经不该停留在“写完代码再人工点点看”，而是让 agent 直接用浏览器读截图、查 console/network、做视觉修改，再把变更回写代码。这和 [[evaluator-driven-qa]]、[[agent-feedback-loops]] 会自然耦合。

### 7. 后台自动化工作流
Cursor automations 把 workflow 再往前推了一步：agent 不只是被人手动唤起，而是由 cron、GitHub 事件、Slack 消息、Webhook、Linear 变更自动触发，在云端执行并回写 PR、评论、通知和 artifacts。这里 workflow 已经变成持续运行的“后台工人系统”。

### 8. 跨职能 SDLC 工作流
Money Forward 的案例说明，coding agent workflow 不一定只服务工程师：
- QA 可以用 agent 从 Jira / Notion 生成 structured test cases，再由第二个 agent 翻成 Playwright scripts
- Product 可以直接读 production code 来补强 PRD 和 requirements
- Design 可以直接对 live frontend 和 analytics 数据做迭代
这意味着 workflow 模板开始从“编码闭环”扩展到“整个 SDLC 的协同闭环”。

### 9. 诊断到 PR 的闭环工作流
Sentry 和 CircleCI 两条案例共同说明，一类非常强的 workflow 正在成型：
- 先由系统或 agent 检测失败 / 问题
- 提供日志、telemetry、trace 或 build context
- 再交给 coding agent 规划修复
- 最后产出已经过验证的 PR
这比“智能体帮你写代码”更接近真正的闭环软件维护工作流。

### 10. 分层 harness 驱动的完整 agent run（Lychee 示例）
[[lychee-technology]] 的文章提供了一个贯穿全部 7 层 harness 的完整执行示例，展示了各层如何在实际运行中配合：

**场景**: "Compare pricing between Competitor A and Competitor B."

| 步骤 | Harness 层 | 动作 | 关键决策 |
|------|-----------|------|---------|
| 1 | Orchestration & State | Planner LLM 分解为 DAG，两个并行分支 | `state.json` 标记 "Fetch A" = `IN_PROGRESS` |
| 2 | Tools | Web search 返回 50 条结果 | BM25 ranking + dedup → 只返回 top 3000 tokens |
| 3 | Contracts | 验证 tool 输出 schema | 不符合则拒绝，不进入模型 |
| 4 | Evaluation | LLM 生成 pricing JSON | Rule-based check 发现缺少 `currency` 字段 |
| 5 | Recovery | 拦截错误，不回传用户 | 把 exact error trace 给 LLM 做 localized retry |
| 6 | State Update | 修正数据通过验证 | `state.json` 标记 A = `COMPLETED`，继续 B |
| 7 | Hard Failure | B 的搜索返回空（网站 down） | 检测空 payload，触发 fallback query |
| 8 | Fallback Succeeds | 替代查询返回有效结果 | Contract + Evaluation 双验证通过后，才写 `COMPLETED` |

这个示例的核心教训：
- **状态写回是条件性的** — 不是"做了就记"，而是"验证通过才记"
- **失败是局部的** — Competitor B 的失败不影响 A 的已完成状态
- **每层都有明确职责** — 没有哪一层在替另一层"顺便做"

## 设计原则
- 优先让 workflow 可验证，而不是只求快。
- 把每一步需要的上下文、工具和反馈源提前准备好。
- 把复杂任务切成智能体能稳住的粒度。
- 在 workflow 中嵌入批准、隔离和回滚边界。
- 对长链路工作流，显式设计“每轮开场动作”和“每轮收尾动作”。
- 如果产品支持 checkpoints / queue / background agents，就把它们当 workflow 原语，而不是边角便利功能。
- 后台 automation 一定要设计 trigger、identity、tool scope、evidence output，不然迟早越权或失控。

## 与相近概念的关系
- [[coding-agent-workflow-patterns]] 是实践层模板。
- [[agentic-engineering]] 更偏系统设计视角，定义 actor 和职责边界。
- [[agent-feedback-loops]] 与 [[agent-observability]] 为 workflow 提供纠偏与证据。
- [[agent-approval-patterns]] 和 [[agent-sandboxing]] 决定 workflow 中哪些动作可自动推进。
- [[evaluator-driven-qa]] 是其中一种适合复杂 UI / 多轮构建的强化工作流。
- [[cloud-agent-operations]] 则是把 workflow 从本地交互式执行，扩展成后台并行、事件驱动、组织级运行。

## 常见误区
- 让智能体直接端到端做完整功能，却不给中间验证节点。
- 只关注实现，不把 review、修复和回归纳入 workflow。
- 每次都临时编流程，导致团队无法复用经验。
- 长任务没有统一开场/收尾规范，导致下一轮 agent 接手时要重新猜现场。
- 把 automation 当普通 prompt 存档，不把它视为长期运行的系统资产。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[claude-code-docs-common-workflows-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[cursor-docs-agent-overview-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
- [[cursor-docs-cloud-agent-automations-2026-04-14]]
- [[cursor-docs-cloud-agent-capabilities-2026-04-14]]
- [[cursor-money-forward-case-study-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
- [[ltbase-harness-engineering-2026-04-24|ltbase-harness-engineering]]
