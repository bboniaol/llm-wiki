---
title: Akshay Pachaar
created: 2026-04-25
updated: 2026-04-25
type: entity
tags: [person, harness-engineering, agentic-engineering]
sources: [raw/articles/akshay-pachaar-anatomy-of-agent-harness-2026-04-25.md]
---

# Akshay Pachaar

## 简介
AI/ML 领域的内容创作者与教育者，活跃于 X/Twitter，以长文形式系统梳理 AI agent 工程话题。其 2026 年 4 月发布的《The Anatomy of an Agent Harness》是目前知识库中最完整的 harness 组件地图之一。

## 核心贡献

### 《The Anatomy of an Agent Harness》（2026-04-25）
这篇长文把生产级 agent harness 拆成 **12 个组件 + 7 个架构选择**，并横向对比了 Anthropic、OpenAI、LangChain、CrewAI、AutoGen 等平台的实现细节。

**12 个组件：**
1. Orchestration Loop（TAO/ReAct 循环）
2. Tool System（schema、验证、沙箱执行）
3. Memory System（多时间尺度：short-term / long-term / project files）
4. Context Management（compaction、masking、JIT retrieval、subagent delegation）
5. Prompt Assembly（分层：system prompt → tools → memory → history → user msg）
6. Output Parsing（native tool calling vs structured output）
7. State Persistence / Checkpointing（LangGraph reducers、OpenAI sessions、Claude Code git commits）
8. Error Handling & Recovery（四种错误类型：transient / LLM-recoverable / user-fixable / unexpected）
9. Guardrails & Safety（input/output/tool 三层 + tripwire）
10. Verification & Feedback（rules-based / visual / LLM-as-judge）
11. Subagent Delegation（Fork / Teammate / Worktree / agents-as-tools / handoffs）
12. Lifecycle Management（Initializer → Coding Agent 接力）

**7 个架构选择：**
1. Single-agent vs. multi-agent（Anthropic/OpenAI 都建议先最大化单 agent）
2. ReAct vs. plan-and-execute（LLMCompiler 3.6x 加速）
3. Context window management（5 种生产策略）
4. Verification loop design（computational vs inferential）
5. Permission and safety architecture（permissive vs restrictive）
6. Tool scoping strategy（Vercel 移除 80% 工具后成功率↑）
7. Harness thickness（Anthropic 赌 thin harness + model improvement）

**关键证据引用：**
- LangChain TerminalBench：只换 harness（同模型同权重）排名从 30 外跳到第 5
- LLM 自优化 harness：76.4% pass rate 超过人工设计系统
- Vivek Trivedy 公式："If you're not the model, you're the harness"
- Beren Millidge 的 OS 类比：裸 LLM = 无 OS 的 CPU，harness = 操作系统

## 与知识库的关系
- 该文是当前知识库中最完整的 harness 组件地图，与 [[harness-engineering]] 概念页直接互补
- 对 [[coding-agent-workflow-patterns]] 贡献了通用的 7-step TAO cycle 骨架
- 对 [[agent-memory-patterns]] 补充了 Claude Code 三层记忆模型和 OpenAI 四类持久策略
- 对 [[codex-vs-claude-code-vs-cursor]] 补充了详细的平台实现对比表
- 文中引用的 TerminalBench 证据与 [[wolfbench]] 形成 benchmark 层面的呼应。TerminalBench 2.0（arXiv:2601.11868）是 89 个真实终端任务的 benchmark，frontier models/agents 得分 < 65%。Stanford Meta-Harness（GitHub: stanford-iris-lab/meta-harness-tbench2-artifact）通过 automated harness evolution 在该 benchmark 上达到 76.4%，验证了 "harness 可自动优化" 的命题。

## 来源
- [[akshay-pachaar-anatomy-of-agent-harness-2026-04-25]]
