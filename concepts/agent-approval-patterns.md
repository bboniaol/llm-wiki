---
title: Agent Approval Patterns
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, workflow, reliability, security, orchestration, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md]
---

# Agent Approval Patterns

## 定义
agent approval patterns 指在人机协作系统里，为智能体定义“哪些动作可以自动执行，哪些动作必须等待人工确认，确认发生在什么粒度和什么节点”的一套控制策略。它解决的核心问题不是让智能体更聪明，而是让自动化边界更安全、更可控。

## 为什么重要
随着 [[codex]]、Claude Code、[[cursor]]、[[deepagents]] 这类智能体系统开始参与真实工程流程，完全放权和完全手动都很差：前者容易失控，后者会把吞吐量打回原形。合适的 approval pattern 能在风险控制和执行效率之间找到平衡，这也是 [[agentic-engineering]] 和 [[harness-engineering]] 落地时绕不开的一层控制面。

## 从 Anthropic 文章得到的新信号
Anthropic 对 long-running agents 的处理说明，approval 不是只针对“危险命令”的开关，而是要和 session 目标设计一起工作：
- 初始化阶段和增量执行阶段可以使用不同 prompt / 不同职责。
- 每轮 coding agent 不应随意重写 feature list，而应只在验证通过后改状态。
- “结束 session 前把环境清理到可接班状态”本身就是一种隐含批准边界：不允许把半成品、脏状态直接甩给下一轮。

## 从 Cursor / Deep Agents 文档得到的新信号
- `permissions.json` 把 terminalAllowlist 和 mcpAllowlist 做成了全局配置文件，并且明确了 team admin > file > IDE 的优先级。
- browser tools 默认也要求 approval，并提供独立的 origin allowlist / block list。
- security 文档明确说 allowlist 不是安全保证，说明 approval 的本质是控制效率与风险，而不是替代安全边界。
- Deep Agents 直接把 human-in-the-loop 做成 runtime capability：可以声明哪些敏感工具操作需要人工确认，并依赖 LangGraph interrupt 能力中断执行等待批准。
- 配置文件或运行时规则只有在自动执行能力存在时才真正有意义，说明“批准模式”和“执行模式”天然是绑定设计的。

## 常见批准模式
- 任务级批准：先批准目标，后续低风险动作自动推进。
- 步骤级批准：关键节点需要人工确认，例如合并、部署、删库、发外部消息。
- 工具级批准：某些工具默认自动，某些工具始终人工守门。
- 风险分级批准：根据影响范围、环境、权限、成本和外部副作用决定是否需要人工介入。
- 状态变更批准：像 feature list、测试状态、完成标记这类“代表系统事实”的字段，必须满足更严格条件才能更新。
- 来源级批准：像 Cursor browser origin allowlist 这种，控制 agent 能去哪些站点、哪些外部系统。

## 设计原则
- 把高风险动作和低风险动作分开，不要一刀切。
- 优先让批准发生在“决策点”而不是“每一步点击点”。
- 批准规则要可解释、可枚举、可落到工具与 workflow 上。
- 把批准结果回写到系统中，让后续智能体知道边界和先例。
- 对跨 session 任务，要控制“什么算完成”，避免 agent 提前宣布胜利。
- 让审批配置可以版本化、可审计，而不是只存在于本地 UI 开关里。

## 与相近概念的关系
- [[agent-approval-patterns]] 负责定义控制闸门。
- [[agent-sandboxing]] 负责限制智能体在未批准前能触达的环境范围。
- [[approval-vs-sandbox-vs-observability]] 从控制面角度对比了批准、隔离与可观测性的职责边界。
- [[repo-as-system-of-record]] 负责把规则、决策和审计痕迹沉淀下来。
- [[agent-feedback-loops]] 可以利用批准结果，决定下一轮执行是继续、回滚还是升级人工处理。
- [[evaluator-driven-qa]] 这类高自动化 workflow 也要受 approval 约束，尤其当 evaluator 能调用浏览器和外部工具时。

## 常见误区
- 所有动作都要求批准，最后把智能体变成半自动表演工具。
- 风险高低没有分级，导致低风险动作也堆积等待。
- 批准只存在于聊天里，没有进入系统记录，后续无法复用和审计。
- 只盯“危险命令”，却不管 agent 是否在错误时机把 feature 标成 done。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[cursor-docs-reference-permissions-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
