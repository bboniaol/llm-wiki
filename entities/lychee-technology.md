---
title: Lychee Technology
created: 2026-04-24
updated: 2026-04-24
type: entity
tags: [company, product, harness-engineering, agentic-engineering]
sources: [raw/articles/ltbase-harness-engineering-2026-04-24.md]
---

# Lychee Technology

## 是什么
Lychee Technology（荔枝科技）是一家发布 Harness Engineering 技术博客的公司，其工程博客 blog.ltbase.dev 发表了关于 agent harness 的系统性文章，包括 7 层 harness stack 和 4 个生产陷阱等框架。该公司同时开发了 Forma（AI-ready data storage）等产品。

## 与 harness engineering 的关系
Lychee Technology 的工程博客是 harness engineering 知识库中一个**独立的方法论来源**。与 OpenAI、Anthropic、LangChain 等组织的方法论不同，Lychee 的文章提供了一个更结构化的**分层框架**（7 层 stack + 4 设计原则 + 4 生产陷阱），适合作为工程落地的参考架构。

## 关键贡献
- **7-Layer Harness Stack**：把 harness 拆成 Cognition、Tools、Contracts & Interfaces、Orchestration、Memory & State、Evaluation & Observation、Constraints & Recovery 七个明确层次。
- **4 设计原则**：Constrain don't instruct / Externalize state / Make every step verifiable / Fail locally not globally。
- **4 生产陷阱**：Context Anxiety / Self-Grading Illusion / Illusion of Correctness / Memory Consolidation Cycle。
- **Minimum Viable Harness**：从 Layer 7（Constraints & Recovery）开始倒着建，而不是从 prompt 开始。

## 与其他实体的关系
- [[openai]]、[[anthropic]]、[[langchain]] — 其他发布 harness engineering 方法论的组织。
- [[harness-engineering]] — 总概念页，Lychee 的文章是该页的重要来源之一。
- [[agent-reliability-patterns]] — Lychee 的 4 个生产陷阱可直接归入可靠性模式。
- [[coding-agent-workflow-patterns]] — Lychee 的完整 agent run 示例补充了 workflow 模板。

## 来源
- [[ltbase-harness-engineering-2026-04-24]]
