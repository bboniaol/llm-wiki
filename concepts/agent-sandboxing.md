---
title: Agent Sandboxing
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, security, reliability, infrastructure, workflow, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/cursor-docs-terminal-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md]
---

# Agent Sandboxing

## 定义
agent sandboxing 指通过隔离的运行环境、受限权限、可回收资源和受控工具接口，让智能体在可观测、可审计、可销毁的边界内执行任务。核心目标是降低错误、越权和污染主环境的风险。

## 为什么它是控制层核心能力
高吞吐智能体如果直接在主环境、主账号、主数据上工作，出错代价会非常高。基于 [[openai]] 的案例，一个关键思路是让智能体在隔离工作树、临时运行实例和受控工具链中工作，这样即使执行失误，损害范围也被限制住。Cursor 的文档则把这个思路补成了相当细的产品配置层：不仅 terminal 默认受限，browser 也有单独 origin 控制和会话隔离，cloud agents 还运行在云端隔离 VM 里。LangChain 这篇文章则把 sandbox 讲成 harness 核心 primitive 之一：它不只是安全壳，更是 agent 执行、观察和验证工作的基本运行面。

## 典型能力
- 隔离工作目录、临时 worktree、一次性环境
- 受限网络、受限凭证、最小权限账户
- 可丢弃的日志、指标和运行实例
- 对文件、进程、浏览器、部署等高风险接口设置边界
- 用配置文件把沙箱策略版本化，而不只是塞在 GUI 开关里

## 从这些文档补出的细节
- terminal 默认在 restricted sandbox 中运行，阻止未授权文件访问和网络活动。
- `sandbox.json` 允许区分 per-user 与 per-workspace 两层配置，并显式定义 network policy、additional paths、protected paths 与缓存策略。
- 企业 / team admin 策略会叠在本地配置之上，而且本地配置不能削弱这些上层控制。
- browser tools 也有单独的 approval、allow/block list、browser context 与 enterprise origin allowlist。
- cloud agents 运行在独立云 VM 中，这是另一层“运行面隔离”，适合把长任务和后台自动化从本地机器剥离出去。
- LangChain 文章强调，sandbox 不只是为了“别把本机炸了”，还要给 agent 一个带浏览器、测试工具、语言运行时和日志观察能力的默认环境，让它能安全 act + observe + verify。
- enterprise 文档把 sandboxing 视为 deterministic security controls 的一部分，而不是体验选项。

## 设计原则
- 默认最小权限，而不是默认全开再靠自觉。
- 让沙箱里的执行足够真实，能复现问题；同时又与主环境隔离。
- 沙箱状态要可观测，方便进入 [[agent-observability]] 和 [[agent-feedback-loops]]。
- 对需要升级权限的动作，和 [[agent-approval-patterns]] 结合处理。
- 配置优先级和保护路径要明确，否则所谓沙箱只是心理安慰。
- 本地沙箱与云端隔离 VM 是互补关系：一个偏交互安全，一个偏后台执行安全。

## 与相近概念的关系
- [[agent-sandboxing]] 提供执行隔离边界。
- [[agent-approval-patterns]] 决定何时允许越过边界做更高风险动作。
- [[approval-vs-sandbox-vs-observability]] 适合用来快速区分三者分别解决什么问题。
- [[harness-engineering]] 把沙箱、反馈回路、约束和工具接入组装成完整系统。
- [[agentic-engineering]] 关注智能体在流程中的角色，而 sandboxing 保证这个 actor 不会乱跑。
- [[evaluator-driven-qa]] 之类高自动化工作流如果没有 sandbox，很容易把验证代理变成新的风险入口。
- [[cloud-agent-operations]] 把 sandboxing 从单机会话延伸到了后台运行面。

## 常见误区
- 以为只要有 Docker 就算 sandboxing 完成。
- 沙箱过于隔离，导致智能体无法获得真实调试信号。
- 没有权限升级路径，一旦需要真实操作只能人工全接管。
- 把 allowlist 当安全证明，忽略它只是 best-effort 的效率配置。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[cursor-docs-terminal-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
- [[cursor-docs-enterprise-llm-safety-controls-2026-04-14]]
- [[cursor-docs-cloud-agent-overview-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
