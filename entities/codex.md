---
title: Codex
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [product, coding-agent, tooling, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/latent-space-extreme-harness-engineering-2026-04-15.md, raw/articles/openai-symphony-spec-2026-04-15.md]
---

# Codex

## 它是什么
Codex 是 OpenAI 在文中使用的核心 coding agent。它不只是写应用代码，还参与测试、CI、文档、评审回复、发布工具、可观测性验证与仓库维护脚本的生成与修改。

## 在本文中的角色
- 从空仓库生成初始架构、CI、包管理设置和初始 `AGENTS.md`。
- 通过标准开发工具（如 gh、本地脚本、仓库内技能）自行收集上下文，而不是依赖人类复制粘贴。
- 可以在本地驱动应用、读取 DOM/截图、查询日志与指标、复现问题并验证修复。
- 在足够完备的环境下，能够端到端完成“重现 bug → 修复 → 验证 → 开 PR → 响应反馈 → 合并”。

## 对工程实践的启发
文章里的重点不是“Codex 很强”，而是 [[openai]] 为它构建了配套的 [[harness-engineering]] 系统：可执行文档、可查询可观测性、结构化约束、自动审查与清理循环。脱离这些支撑结构，文中的自主水平不能简单泛化。

Latent.Space 的后续文章则把这条线再往前推了一步：在 Frontier / Symphony 语境里，Codex 不再只是终端里的 coding assistant，而是被接进 work orchestration service、review agents、skills、observability stacks 和 PR lifecycle automation 之后的一组执行节点。

## 关联
- [[openai]] 用 Codex 作为主要执行智能体来验证新的软件交付模式。
- [[harness-engineering]] 描述的是让 Codex 稳定工作的整套环境与反馈回路。
- [[agent-readable-repositories]] 是 Codex 能长期保持上下文与行为一致性的关键前提。
- [[symphony]] 则说明 Codex 还可以进一步被编排成 issue-driven autonomous runs，而不是只作为单机会话工具。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[latent-space-extreme-harness-engineering-2026-04-15]]
- [[openai-symphony-spec-2026-04-15]]
