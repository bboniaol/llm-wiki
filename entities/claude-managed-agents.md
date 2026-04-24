---
title: "Claude Managed Agents"
created: 2026-04-24
updated: 2026-04-24
type: entity
tags: [product, agent, harness, managed-infrastructure, anthropic]
sources: [raw/articles/lance-martin-claude-managed-agents-2026-04-09.md]
---

# Claude Managed Agents

Anthropic 推出的托管式 agent 平台，提供预构建、可配置的 agent harness + 托管基础设施。

## 核心定位

> "A pre-built, configurable agent harness that runs in managed infrastructure."

不是让用户自己搭建 harness，而是把 harness + 基础设施一起托管，让开发者专注于定义 agent 模板（tools, skills, files/repos 等）。

## 设计动机：两个根本挑战

### 1. Harness 假设会过时

基于 Messages API 的 agent 需要 harness 来路由 tool calls、管理上下文。但 harness 编码了对 Claude "不能做什么"的假设——随着 Claude 能力指数级增长，这些假设会**过时并 bottleneck 模型性能**。

> "Harnesses need to be continually updated to keep pace with Claude."

### 2. 任务时间 horizon 在指数级增长

Claude 在 METR benchmark 上已超过 **10 个人类小时**的工作量。未来 Claude 可能运行数天、数周甚至数月——这对基础设施提出安全、弹性、可扩展的要求。

## 架构设计：三体分离

不设计特定 harness，而是将系统解耦为三个独立接口：

| 组件 | 角色 | 说明 |
|------|------|------|
| **Brain** | Claude + harness | 持续演进，不做强假设 |
| **Hands** | Sandboxes + tools | 执行动作，可独立失败/替换 |
| **Session** | 事件日志 | 状态记录，可独立失败/替换 |

每个组件之间做最少假设，可以独立失败或被替换。

## 核心概念

| 概念 | 定义 | 类比 |
|------|------|------|
| **Agent** | 版本化配置：model, system prompt, tools, skills, MCP servers | 身份/人格 |
| **Environment** | 沙箱模板：runtime, networking, package config | 工作环境 |
| **Session** | 一次有状态执行：用 Agent + Environment 运行，挂载资源，凭证存 vault | 一次任务 |

关系：一个 Agent 可以有多个 Session。

## 使用模式

| 模式 | 描述 | 示例 |
|------|------|------|
| **Event-triggered** | 服务触发，无人介入 | 系统 flag bug → agent 写 patch 开 PR |
| **Scheduled** | 定时执行 | 每日简报（X/GitHub 活动、agent 团队进展） |
| **Fire-and-forget** | 人类触发，异步交付 | Slack/Teams 指派任务 → 返回 spreadsheet/slides/app |
| **Long-horizon** | 长周期任务 | fork auto-research repo，让 agent 持续探索 |

## 接入方式

| 方式 | 面向 | 支持语言 |
|------|------|----------|
| **SDKs** | 代码集成，驱动 Session | Python, TypeScript, Java, Go, Ruby, PHP |
| **CLI** | 终端操作，管理所有资源 | 所有 API 资源作为子命令 |
| **Skills** | Claude Code 内快速上手 | `/claude-api managed-agents-onboarding` |

典型工作流：CLI 做 setup，SDK 做 runtime，Agent 模板存 YAML 在 git 里。

## 官方资源

- [Claude blog](https://www.anthropic.com/news/claude-managed-agents) — 使用模式和客户案例
- [Engineering blog](https://www.anthropic.com/engineering/claude-managed-agents) — 设计过程（与 @eyaltoledano, @gsheasby, @sasharush 合著）
- [Docs](https://docs.anthropic.com/en/docs/claude-managed-agents/overview) — 快速开始、CLI 和 SDK 概览

## 与相关概念的关系

- [[harness-engineering]] — Claude Managed Agents 是"托管 harness"的实例，验证了 harness 不会消失而是变薄/被托管
- [[framework-vs-runtime-vs-harness]] — 属于"托管 harness + 基础设施"层，不是 framework 也不是纯 runtime
- [[claude-code]] — 通过 skills 机制集成 onboarding
- [[anthropic]] — 公司实体页
- [[lance-martin]] — 主要推动者

## 关键洞察

1. **Agent scaling = infrastructure challenge** — 不是 harness 设计问题，是基础设施问题
2. **Harness 需要持续更新** — 模型能力增长会让旧 harness 成为 bottleneck
3. **三体分离 = 可靠性 + 安全 + 灵活** — brain/hands/session 独立演进
4. **Agent 作为新核心原语** — 从 Messages API 的原语升级为可配置、可复用的 Agent 模板
