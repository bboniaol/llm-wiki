---
title: Doc-gardening Agents
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, automation, documentation, workflow, best-practice, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md]
---

# Doc-gardening Agents

## 定义
doc-gardening agents 指专门负责扫描、修剪、更新和修复文档系统的智能体。它们不直接面向终端用户交付功能，而是持续维护知识库、规范、索引、交叉链接与过期内容，防止文档成为腐烂的装饰品。

## 为什么它重要
在智能体系统里，文档不只是给人读的说明书，而是 [[context-engineering]] 和 [[repo-as-system-of-record]] 的基础设施。如果文档很快过期，主执行智能体拿到的上下文就会变脏，整个 [[harness-engineering]] 的可靠性会一起下降。

## 在 OpenAI 案例里的映射
文章明确提到有一个定期运行的“doc-gardening”智能体，用来扫描那些已经不再反映真实代码行为的文档，并主动发起修复 PR。这说明文档维护不再是可有可无的补充劳动，而是被纳入工程系统本身。

## 典型职责
- 检查索引是否完整、交叉链接是否断裂
- 发现与当前代码行为不一致的说明文档
- 更新质量评分、规范引用和计划状态
- 清理陈旧规则、重复文档和失效入口

## 设计原则
- 文档治理要周期性、自动化，而不是只在出事故后补救。
- 修剪 agent 最好基于明确规则工作，而不是自由发挥改写一切。
- 文档修复也应走 review 和验证流程，避免“自动造谣”。
- 把 doc gardening 视为技术债管理的一部分。

## 与相近概念的关系
- [[doc-gardening-agents]] 是 [[agent-readable-repositories]] 的维护者。
- 它们依赖 [[repo-as-system-of-record]] 提供稳定的落点。
- 也会进入 [[coding-agent-workflow-patterns]]，以 PR 形式交付修复。
- 在大规模智能体系统里，它是控制熵增的重要手段，和 [[agent-feedback-loops]] 一样属于长期稳定性组件。

## 常见误区
- 以为文档过期只是阅读体验问题，其实会直接伤害智能体执行质量。
- 让文档 agent 无约束地改写规范，导致噪音上升。
- 只关注代码垃圾回收，不关注文档垃圾回收。

## 来源
- [[openai-harness-engineering-2026-04-14]]
