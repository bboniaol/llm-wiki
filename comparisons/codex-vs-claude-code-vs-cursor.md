---
title: Codex vs Claude Code vs Cursor
created: 2026-04-14
updated: 2026-04-25
type: comparison
tags: [comparison, coding-agent, tooling, workflow, best-practice, query-note]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-claude-code-2026-04-14.md, raw/articles/claude-code-docs-overview-2026-04-14.md, raw/articles/claude-code-auto-mode-2026-04-14.md, raw/articles/claude-code-docs-permission-modes-2026-04-14.md, raw/articles/claude-code-docs-memory-2026-04-14.md, raw/articles/claude-code-docs-sub-agents-2026-04-14.md, raw/articles/claude-code-docs-common-workflows-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/cursor-product-2026-04-14.md, raw/articles/cursor-docs-subagents-2026-04-14.md, raw/articles/cursor-docs-rules-2026-04-14.md, raw/articles/cursor-docs-mcp-2026-04-14.md, raw/articles/cursor-docs-terminal-2026-04-14.md, raw/articles/cursor-docs-agent-overview-2026-04-14.md, raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/akshay-pachaar-anatomy-of-agent-harness-2026-04-25.md]
---

# Codex vs Claude Code vs Cursor

## 比较前提
这一版已经不只是“产品页对产品页”，而是三类证据混合：
- [[codex]]：目前主要来自 [[openai]] 的真实工程案例
- [[claude-code]]：官方产品页 + 官方文档 + Auto mode + permission / memory / sub-agents / workflows + 长任务 harness 工程文章 + CircleCI adoption 案例
- [[cursor]]：官方产品页 + docs（subagents / rules / MCP / terminal / checkpoints / permissions / sandbox / browser / security / cloud agents / automations / enterprise controls）+ Money Forward 客户案例

所以这页现在能做的是“工程取向对比”，还不能做严格 benchmark 排行。

## 高层对比表
| 维度 | [[codex]] | [[claude-code]] | [[cursor]] |
|---|---|---|---|
| 当前证据强项 | 真实工程闭环案例 | 方法论文档最厚，且开始出现更贴近本体的 adoption 证据 | 本地 + 云端控制面最完整，并出现跨职能 adoption 案例 |
| 主要形态 | harness 内核心执行智能体 | 跨 terminal / IDE / desktop / browser 的 coding agent | 本地 agent IDE + cloud agents + automations 平台 |
| 记忆体系信号 | 案例里强调 repo 作为记录系统 | `CLAUDE.md` + auto memory + progress artifacts | rules + AGENTS.md + indexing + checkpoints + automation memories |
| 多 agent / delegation | 案例有 agent-to-agent review 信号 | sub-agents、Agent SDK、foreground/background、persistent memory | subagents、orchestrator、verification pattern、parallel cloud agents |
| 长任务能力 | 案例显示可持续数小时执行 | Auto mode + initializer/coding agent 接棒设计 + common workflows | background subagents、queued messages、checkpoints、cloud automations |
| 控制面信号 | 案例强调 harness、验证、审查 | permission modes 层级非常细 | permissions.json、sandbox.json、MCP approval、browser origin allowlist、enterprise safety controls、audit logs |
| 公开 adoption 信号 | 强案例但主要是 OpenAI 自身 | CircleCI 已给出较强工程团队 adoption；Sentry 给出 managed runtime 平台案例 | 已出现 Money Forward 这类跨 engineering / QA / product / design 案例 |

## 阶段性观察
### 1. Codex：目前最强的是“真实工程闭环证据”
当前库里关于 [[codex]] 最值钱的仍是 [[openai-harness-engineering-2026-04-14]] 这类案例：它不是只讲功能，而是展示了如何在真实产品开发里跑实现、验证、review、修复、合并闭环。这让 Codex 在“案例硬度”上目前最强。

### 2. Claude Code：现在从“方法论最厚”开始走向“公开 adoption 更可信”
[[claude-code]] 不再只是多表面产品。它同时具备：
- 明确 permission modes
- `CLAUDE.md` + auto memory 的双层记忆
- sub-agents 与 Agent SDK
- common workflows 文档
- Anthropic 提供的跨窗口长任务 harness 方法
- CircleCI 这类更贴近 Claude Code 本体的 adoption 证据

这使它在 [[long-running-agent-tasks]]、[[agent-memory-patterns]]、[[agent-approval-patterns]]、[[multi-agent-delegation]] 这些维度上仍然是“方法论最成体系”的一方，而且公开案例层也开始变硬。

### 3. Cursor：现在最像“本地 IDE + 云端代理平台 + 企业控制面 + 跨职能 adoption”的组合体
[[cursor]] 的 docs 之前已经显示它强调 plan、debug、subagents、rules、MCP、terminal sandbox、checkpoints；补上 Money Forward 案例后，轮廓更完整了：
- 本地：permissions.json、sandbox.json、browser tools、debug/plan、checkpoints、queue
- 云端：cloud agents、automations、computer use、PR artifacts、CI 修复
- 组织层：team-owned automations、service account、enterprise safety controls、audit logs、hooks、DLP 集成
- 业务层：开始扩到 QA、product、design，而不只是工程师个人提效

所以 Cursor 现在在库里的轮廓已经不只是“IDE 内 agent 系统化”，而是“agent operating surface + SDLC adoption”做得最全的一方。

## 如果按工程关注点来选观察角度
- 关注"真实软件工程闭环案例" → 先看 [[codex]]
- 关注"跨窗口长任务接棒与长期自主推进 + developer-facing adoption" → 先看 [[claude-code]]
- 关注"从本地交互式 agent 一路延伸到云端后台代理、组织控制与跨职能 adoption" → 先看 [[cursor]]

## Akshay Pachaar 的平台实现对比补充
Akshay 的长文把三家的 harness 实现细节做了很好的横向梳理，值得补充到对比表中：

| 维度 | [[codex]] | [[claude-code]] | [[cursor]] |
|---|---|---|---|
| **Harness 架构** | Codex Core + App Server + client surfaces（三层共享同一 harness） | Claude Agent SDK（`query()` 函数，async iterator 流式消息） | 本地 IDE agent + cloud agents + automations |
| **Runtime 哲学** | "code-first"：workflow 逻辑用原生 Python 表达 | "dumb loop"：所有智能在模型，harness 只管 turns | 本地交互式 + 云端后台并行 |
| **循环模式** | Runner class（async/sync/streamed） | Gather-Act-Verify | Plan/Debug + subagents + checkpoints |
| **Tool 体系** | function tools + hosted tools + MCP | 6 类：file ops、search、execution、web、code intel、subagents | subagents、rules、MCP、terminal、browser |
| **记忆实现** | application memory / SDK sessions / Conversations API / `previous_response_id` | 三层：lightweight index + topic files + raw transcripts | rules + AGENTS.md + checkpoints + automation memories |
| **状态持久** | 四种互斥策略 | git commits + progress files | checkpoints + queue |
| **错误处理** | 三层 guardrails（input/output/tool）+ tripwire | 在 tool handler 内捕获，返回 error result 保持循环 | permissions + sandbox + enterprise controls |
| **验证机制** | 依赖外部测试/审查 | rules-based + visual + LLM-as-judge 三种 | browser tools + debug + CI 集成 |
| **子代理** | agents-as-tools + handoffs | Fork / Teammate / Worktree 三种执行模型 | subagents + orchestrator + parallel cloud agents |
| **Context 管理** | priority stack（server system msg > tools > dev instructions > user instructions） | compaction + observation masking + JIT retrieval + subagent delegation | lazy loading + indexing + tool output truncation |

关键洞察：
- **Codex 的 "all surfaces share the same harness"** 解释了为什么 "Codex models feel better on Codex surfaces than a generic chat window" — harness 与模型是 co-evolved 的
- **Claude Code 的 "dumb loop"** 是最极简的 harness 哲学，与 Anthropic "thin harness + model improvement" 的赌注一致
- **Cursor 的 hybrid 模式**（本地 + 云端）是目前覆盖场景最广的，但也意味着 harness 复杂度最高

## 目前还不能下的结论
基于当前证据，还不能严谨下这些判断：
- 三者谁在真实大仓库上的成功率最高
- 谁的 bugfix 质量或 review 质量最好
- 谁的长任务成本/速度比最优
- 谁的 MCP / sandbox / approval 在复杂企业环境中最好用

这些结论仍需要：更多官方深文档、公开案例、第三方评测，以及你自己的实战记录。

## 下一步补证建议
1. 为 [[claude-code]] 再补第二条 adoption / customer story，避免只靠 CircleCI 单一案例
2. 为 [[cursor]] 继续补第二、第三个公开案例，避免只靠单一 customer story
3. 未来再引入第三方 eval 或你自己的实战观察，把这页升级成“证据驱动对比 V9”

## 关联
- [[coding-agent-evals]] 决定未来怎么系统比较它们。
- [[long-running-agent-tasks]] 是区分三者真实价值的重要场景。
- [[multi-agent-delegation]] 是理解 Cursor 与 Claude Code 差异化的关键入口之一。
- [[agent-approval-patterns]]、[[agent-sandboxing]]、[[agent-memory-patterns]]、[[evaluator-driven-qa]]、[[cloud-agent-operations]] 是后续继续拆控制面和验证层的关键线索。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-claude-code-2026-04-14]]
- [[claude-code-docs-overview-2026-04-14]]
- [[claude-code-auto-mode-2026-04-14]]
- [[claude-code-docs-permission-modes-2026-04-14]]
- [[claude-code-docs-memory-2026-04-14]]
- [[claude-code-docs-sub-agents-2026-04-14]]
- [[claude-code-docs-common-workflows-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
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
- [[akshay-pachaar-anatomy-of-agent-harness-2026-04-25|akshay-pachaar-anatomy-of-agent-harness]]
