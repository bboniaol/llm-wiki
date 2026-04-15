---
title: Cursor
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [product, coding-agent, tooling, workflow, context-engineering]
sources: [raw/articles/cursor-product-2026-04-14.md, raw/articles/cursor-docs-subagents-2026-04-14.md, raw/articles/cursor-docs-rules-2026-04-14.md, raw/articles/cursor-docs-mcp-2026-04-14.md, raw/articles/cursor-docs-terminal-2026-04-14.md, raw/articles/cursor-docs-agent-overview-2026-04-14.md, raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md]
---

# Cursor

## 它是什么
Cursor 是一款以 AI coding 为核心的 agent IDE / coding product。当前抓取到的官方 product、docs 和客户案例显示，它把计划、调试、terminal、subagents、rules、skills、MCP、checkpoints、browser tools、安全控制面，以及 cloud agents / automations 整合进一个面向软件开发的 agent 工作台。

## 当前可确认的能力
- 支持 agent 模式，可独立完成复杂 coding task。
- 支持 plan / debug / terminal 等模式。
- 支持 subagents，并可 foreground / background 运行。
- 支持 codebase indexing、自定义 embedding、team rules、skills、plugins、MCP。
- terminal 默认 sandboxed，可配置 network policy、protected paths、shared build cache、workspace/per-user sandbox.json。
- 支持 permissions.json，为 terminal 和 MCP auto-run 设 allowlist，并遵循 team admin > file > IDE 的优先级。
- 支持 browser tools，可读 console logs、network traffic、screenshots，并带 origin allowlist、session persistence 与 enterprise 控制。
- 支持 checkpoints，可在 agent session 中回滚到历史快照；支持 queued messages 让会话像持续任务队列一样推进。
- 支持 cloud agents，在云端隔离 VM 中并行跑任务、开分支、推 PR、修 CI、附带 artifacts。
- 支持 automations，通过 schedule、GitHub、Slack、Webhook、Linear 触发后台 agent。

## 从文档和案例看出的工程特征
- Cursor 非常强调 [[context-engineering]]：rules、AGENTS.md、indexing、mentions、skills 都在服务“给 agent 正确上下文”。
- 它也明显强调 [[multi-agent-delegation]]：subagents 有独立上下文、并行执行、verification/orchestrator pattern。
- 在控制层上，Cursor 把 [[agent-sandboxing]]、[[agent-approval-patterns]]、MCP tool approval、permissions.json allowlist、browser origin allowlist 等做成了较明确的产品设置。
- checkpoints 和 queued messages 则让它在 [[long-running-agent-tasks]] 与迭代式 workflow 中更像一个持续会话系统，而不只是一次性补全器。
- browser tools 说明它不仅想管“写代码”，还想把 UI 验证、可视化调试和设计回写也纳入 agent workflow。
- cloud agents / automations 又把它从“本地 IDE agent”推到“后台 agent 平台”：能并行、异步、事件触发、团队计费、服务账号执行。
- enterprise 文档说明它不是只做个人效率，而是在往组织级安全、审计、合规与 DLP 接入扩展。
- Money Forward 案例则提供了目前库里最硬的公开 adoption 证据：Cursor 不只是工程师工具，而是开始扩展到 QA、product、design 的 cross-functional SDLC 平台。
- security 文档对 allowlist 的态度很克制：它是效率机制，不是安全证明，这点比很多产品文案诚实。

## 当前已知边界
现在这页主要还是基于官方产品、文档与客户案例，因此可以确认产品设计方向和一个较强 adoption 案例；但还不足以严谨判断它在所有真实大型仓库、复杂 review 闭环和长期可靠性上一定比 [[claude-code]] / [[codex]] 更强。后续仍需要更多案例、评测和实战补证。

## 关联
- [[money-forward]] 是当前库里关于 Cursor 最硬的一条公开案例证据。
- [[codex-vs-claude-code-vs-cursor]] 用它作为 coding agent 工具比较对象之一。
- [[context-engineering]]、[[multi-agent-delegation]]、[[agent-sandboxing]]、[[coding-agent-workflow-patterns]] 都和 Cursor 的官方设计强相关。
- [[cloud-agent-operations]] 是理解 Cursor 从本地代理扩展到后台平台代理的重要入口。
- [[agent-memory-patterns]] 与 [[repo-as-system-of-record]] 也是后续继续分析它的重要入口。
- [[evaluator-driven-qa]] 和 browser tools / debug flow / checkpoints 结合后，是分析 Cursor UI 工程能力的下一条线索。

## 来源
- [[cursor-product-2026-04-14]]
- [[cursor-docs-subagents-2026-04-14]]
- [[cursor-docs-rules-2026-04-14]]
- [[cursor-docs-mcp-2026-04-14]]
- [[cursor-docs-terminal-2026-04-14]]
- [[cursor-docs-agent-overview-2026-04-14]]
- [[cursor-docs-reference-permissions-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-cloud-agent-overview-2026-04-14]]
- [[cursor-docs-cloud-agent-automations-2026-04-14]]
- [[cursor-docs-cloud-agent-capabilities-2026-04-14]]
- [[cursor-docs-enterprise-llm-safety-controls-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
- [[cursor-money-forward-case-study-2026-04-14]]
