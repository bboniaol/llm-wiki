---
title: Anthropic
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, product, harness-engineering, agentic-engineering]
sources: [raw/articles/anthropic-claude-code-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md]
---

# Anthropic

## 它是什么
Anthropic 是 Claude、Claude Code、Claude Agent SDK 与 Claude Managed Agents 的发布方。就当前知识库中的资料看，Anthropic 对 harness engineering 的贡献不只是提供模型，而是在长时任务、跨 context window 接力、memory 工件、Auto mode、Agent SDK、多角色 harness 设计，以及 context engineering 方法论方面给出了更结构化的工程表达。

## 当前在库中的重要信号
- 通过 [[claude-code]] 产品页和文档，展示了一个多表面 coding agent 的产品化路线。
- 通过《Effective harnesses for long-running agents》这篇工程文章，把 long-running agents 的问题具体拆成 initializer agent、coding agent、feature list、progress file、git history、init.sh 等可落地工件。
- 通过《Harness design for long-running application development》把方法继续推进到 planner / generator / evaluator 三角色结构、Playwright MCP QA、sprint contract，以及“模型变强后可以删掉哪些旧支架”这种更成熟的 harness 迭代视角。
- 通过《Effective context engineering for AI agents》把 context engineering 从 prompt engineering 中分离出来，明确提出最小高信号上下文、just-in-time retrieval、compaction、structured note-taking 和 sub-agent architectures。
- 通过 Sentry 公开案例，补上了平台级 adoption 证据：Claude Managed Agents 被用于把 bug detection / RCA / coding agent / PR 交付串成闭环，而且由单个工程师在几周内完成集成。
- 通过 CircleCI 公开案例，补上了更贴近 Claude Code 本体的 adoption 证据：90% 工程团队在使用 Claude Code，且有团队基于 Claude Agent SDK 在几周内构建自治维护 agent 与 AI PR review 系统。
- 文章中还明确提到 Claude Code 团队与 code RL 团队参与了 long-horizon autonomous software engineering 的实践。

## 在知识库中的位置
Anthropic 目前更像是“长任务 + 上下文治理 + 应用开发 harness 方法论 + 托管 runtime 平台 + 开发者工作台 adoption”的重要来源，而不只是另一个模型公司。相较于 [[openai]] 当前在库里最强的是真实产品闭环案例，Anthropic 当前在库里最强的是把跨窗口接力、长链路应用开发、evaluator-driven QA、context engineering、managed runtime 平台化，以及 developer-facing coding adoption 讲得更工程化。

## 关联
- [[claude-code]] 是 Anthropic 当前在库里的核心 developer-facing 产品载体。
- [[claude-managed-agents]] 则是 Anthropic 在托管 agent runtime 方向上的平台信号。
- [[harness-engineering]]、[[context-engineering]]、[[long-running-agent-tasks]]、[[agent-memory-patterns]]、[[agent-feedback-loops]] 都从 Anthropic 的资料里得到重要补强。
- [[codex-vs-claude-code-vs-cursor]] 中，Anthropic 代表的是另一种更文档化、产品化、平台化的 agent engineering 路线。

## 来源
- [[anthropic-claude-code-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
