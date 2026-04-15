---
title: Claude Code
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [product, coding-agent, tooling, workflow, agentic-engineering]
sources: [raw/articles/anthropic-claude-code-2026-04-14.md, raw/articles/claude-code-docs-overview-2026-04-14.md, raw/articles/claude-code-auto-mode-2026-04-14.md, raw/articles/claude-code-docs-permission-modes-2026-04-14.md, raw/articles/claude-code-docs-memory-2026-04-14.md, raw/articles/claude-code-docs-sub-agents-2026-04-14.md, raw/articles/claude-code-docs-common-workflows-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md]
---

# Claude Code

## 它是什么
Claude Code 是 Anthropic 推出的 agentic coding tool。根据官方产品页、文档、工程文章和公开客户案例，它不仅是一个聊天式编码助手，而是一个能读取代码库、编辑文件、运行命令、接入开发工具并跨多个工作表面运行的 coding agent，同时也是 Anthropic 长时任务 harness 与应用生成 harness 的重要执行体之一。

## 当前可确认的能力
- 直接读取代码库、编辑文件、运行命令。
- 可在 terminal、VS Code、JetBrains、desktop、browser 中使用。
- CLI 支持第三方 provider。
- 支持 MCP、instructions、skills、hooks、sub-agents、Agent SDK。
- 可创建 commit、branch、PR，并在 CI 中接入 GitHub Actions / GitLab CI/CD。
- desktop 形态支持并行会话、视觉 diff、预览 server、定时任务和 cloud sessions。

## 从深文档、工程文章和案例看出的工程特征
- permission modes 非常细：default、acceptEdits、plan、auto、dontAsk、bypassPermissions，不只是“要不要弹确认框”。这让 [[agent-approval-patterns]] 在 Claude Code 里有了明确产品化表达。
- memory 机制明确拆成 `CLAUDE.md` 与 auto memory，两者一起承载长期规则和经验，这对 [[agent-memory-patterns]] 很关键。
- sub-agents 支持独立上下文、独立权限、工具限制、模型选择、foreground/background、persistent memory，明显强化了 [[multi-agent-delegation]] 能力。
- common workflows 文档把理解代码库、找代码、debug、plan mode、tests、PR、parallel worktrees 等工作流做成了显式套路，说明它不是只提供模型，而是在提供一整套可复用开发流程。
- Anthropic 的上一版长任务文章表明，Claude Agent SDK / Claude Code 生态强调 initializer agent、coding agent、feature list、progress file、git history、init.sh 这类“跨窗口接棒工件”。
- 最新应用开发文章进一步显示，Claude Agent SDK 可以承载 planner / generator / evaluator 三角色 harness：规划者扩 spec，构建者生成应用，评估者用 Playwright MCP 和评分标准做独立 QA；而且 harness 结构会随模型能力变化而被主动简化。
- CircleCI 案例则首次补上了较硬的公开 adoption 证据：90% 工程团队在用 Claude Code，且有团队基于 Claude Code / Agent SDK 在几周内构建 AI PR review 系统与自治维护 agent。

## 当前已知边界
基于现有资料，能确认的是产品能力面、官方工程方向，以及至少一条较强的公开 adoption 案例；但还不能仅凭这些材料就断言它在所有真实大仓库、复杂 bugfix 或成本表现上一定优于 [[codex]] 或 [[cursor]]。这类判断仍需更多案例和 eval 支撑。

## 关联
- [[anthropic]] 是 Claude Code 的发布方，也是长任务 harness 方法论的重要来源。
- [[codex-vs-claude-code-vs-cursor]] 把它作为 coding agent 工具比较对象之一。
- [[agentic-engineering]]、[[coding-agent-workflow-patterns]]、[[long-running-agent-tasks]] 是理解 Claude Code 的关键入口。
- [[agent-memory-patterns]]、[[agent-approval-patterns]]、[[multi-agent-delegation]]、[[agent-feedback-loops]] 在其资料中都有明确映射。
- [[circleci]] 是当前库里关于 Claude Code adoption 最强的一条公开案例证据。

## 来源
- [[anthropic-claude-code-2026-04-14]]
- [[claude-code-docs-overview-2026-04-14]]
- [[claude-code-auto-mode-2026-04-14]]
- [[claude-code-docs-permission-modes-2026-04-14]]
- [[claude-code-docs-memory-2026-04-14]]
- [[claude-code-docs-sub-agents-2026-04-14]]
- [[claude-code-docs-common-workflows-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
