---
title: Evaluator-driven QA
created: 2026-04-14
updated: 2026-04-16
type: concept
tags: [concept, reliability, testing, workflow, best-practice, harness-engineering]
sources: [raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md, raw/articles/coderabbit-docs-overview-2026-04-16.md, raw/articles/meticulous-product-overview-2026-04-16.md, raw/articles/braintrust-score-production-traces-2026-04-16.md, raw/articles/langfuse-evaluation-overview-2026-04-16.md, raw/articles/phoenix-evaluation-overview-2026-04-16.md]
---

# Evaluator-driven QA

## 定义
evaluator-driven QA 指把“生成/实现”和“验收/评估”拆给不同 agent 或不同角色来完成的一种质量保障模式。核心不是多一个 reviewer，而是明确承认：生成 agent 往往不擅长严格评估自己，尤其在主观质量、复杂交互和边界条件上容易偏乐观。

## 为什么值得单独成页
Anthropic 的应用开发文章把这个模式讲得很实：当 generator 自评不可靠时，让独立 evaluator 基于 Playwright MCP、评分 rubric、sprint contract 和硬阈值做验收，能显著提升输出质量。这里的关键不只是“多一个测试环节”，而是把 QA 从附属检查提升成 harness 的主结构。

## 核心结构
- generator：负责生成实现、推进功能、响应反馈。
- evaluator：负责独立跑 UI、API、数据库和行为验证，并输出可执行反馈。
- contract / rubric：把“什么算 done”与“按什么标准打分”提前写清楚。
- feedback loop：evaluator 的发现必须直接进入下一轮 generator 修复，而不是停留在报告里。
- 在更轻量的实践里，这个 evaluator 不一定是完整 QA agent，也可能只是像 Karan 所说那样的 `LLM as Judge` / critic-in-loop，用来在最终输出前做一层结构化批判与校验。

## 设计原则
- 评估者必须与执行者职责分离，避免“自己给自己打分”。
- 评价标准要尽量结构化、机器可读、可复用。
- evaluator 的输出要足够具体，能直接转成下一轮修复任务。
- evaluator 也需要校准： few-shot、反例、日志复盘都很重要。
- 不是所有任务都要 evaluator；当模型已经能稳定 solo 完成时，evaluator 可能变成额外成本。

## 适用场景
- UI / UX 质量很重要，且“好不好”不能只靠单元测试判断。
- 功能很多、交互复杂，容易出现“看起来像成品但一用就坏”。
- 任务长、回归成本高，需要专门角色持续守住完成标准。
- 团队想把 [[agent-feedback-loops]] 做成更稳定的结构，而不是临时补丁。
- 团队希望把 evaluator 外化成常驻组件：要么像 CodeRabbit 一样挂在 PR review 入口，要么像 Meticulous 一样挂在 browser regression 入口，形成 workflow-native checker。

## 新增判断：evaluator 正在从角色扩展成平台/检查层
Anthropic 这条线展示的是 harness 内的 evaluator 角色；而 2026-04-16 新补的 CodeRabbit、Meticulous、Braintrust、Langfuse、Phoenix 等资料则说明，evaluator 正在外化成常驻平台能力：有的盯 PR，有的盯浏览器回归，有的盯生产 traces。这让 [[evaluator-driven-qa]] 不再只是“多 agent 分工”，而是一个可以落在多种工程入口的质量结构。更完整的横向归纳见 [[from-offline-benchmark-to-online-evals]]。

## 与相近概念的关系
- [[evaluator-driven-qa]] 是 [[agent-feedback-loops]] 的强化版本，把反馈源组织成专门角色。
- 它是 [[agent-reliability-patterns]] 的一种具体实现，用角色互校降低误判。
- 在 [[multi-agent-delegation]] 中，它通常表现为 generator → evaluator → generator 的闭环。
- 它依赖 [[agent-observability]]、浏览器工具、测试工具和 contract 工件来提供证据。
- [[evaluator-driven-qa-vs-human-in-the-loop-review]] 对比了它与人工关键节点审查各自更适合守住哪类风险。
- 在 [[harness-engineering]] 里，它是解决“自评失真”的一类支架，而不是额外装饰。

## 常见误区
- 把 evaluator 当普通 reviewer，用一句“看起来不错”就放过。
- evaluator 只给结论，不给具体失败证据和修复线索。
- 以为 evaluator 越重越好，忽略它的成本收益边界。
- 只在最终阶段做 QA，不把反馈接回生成环。

## 来源
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[karan-x-post-2043618895328932340-2026-04-15]]
