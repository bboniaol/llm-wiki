---
title: OpenAI
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [company, product, harness-engineering, agentic-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md]
---

# OpenAI

## 它是什么
OpenAI 是这篇文章的发布方，也是文中所述 Codex 内部实验的组织者。文章展示了 OpenAI 如何在真实产品开发中，把工程团队的主要工作从“手写代码”转移到“设计环境、约束与反馈回路”，并以此验证 [[harness-engineering]] 在真实团队中的可行性。

## 在本文中的关键信号
- 2025 年 8 月下旬，OpenAI 团队从空仓库启动一个由智能体主导生成的项目。
- 五个月内，代码库增长到约一百万行，约 1,500 个 Pull Request 被打开并合并。
- 文章强调“人类掌舵，智能体执行”，说明组织职责并未消失，而是迁移到了任务定义、环境设计与验收控制。

## 组织层面的工程取向
- 将代码仓库视为智能体可访问的唯一高保真知识边界。
- 将文档、计划、评测、可观测性与 lint 规则一起纳入版本控制，作为系统能力的一部分。
- 通过约束、结构测试和持续清理机制，降低智能体高速产出带来的架构漂移与熵增。

## 关联
- OpenAI 通过 [[codex]] 推动文章中的智能体软件工程实验。
- 这篇文章是 [[harness-engineering]] 的典型案例，不是泛泛谈模型能力，而是强调系统设计。
- 其知识管理方式与 [[agent-readable-repositories]] 高度相关。

## 来源
- [[openai-harness-engineering-2026-04-14]]
