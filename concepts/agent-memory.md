# Agent Memory: How to Build Agents that Learn and Remember

## 基本信息
- **来源**: Letta (原 MemGPT) 官方博客
- **发布时间**: 2024-2025
- **链接**: https://www.letta.com/blog/agent-memory
- **标签**: #agent #memory #context-engineering #letta #memgpt #stateful-agents

---

## 一句话总结

Agent Memory 的本质是**上下文工程（Context Engineering）**——决定哪些 token 进入上下文窗口、如何组织、如何在外部存储与上下文之间流转，从而让无状态 LLM 变成有状态、能学习的 Agent。

---

## 核心论点

### 1. 从 Stateless 到 Stateful
- 传统 LLM：每次交互孤立，无记忆继承
- Stateful Agent：能跨会话学习、适应、进化
- **记忆 = 上下文窗口中的内容**

### 2. Agent Memory 的四种类型

| 类型 | 功能 | 位置 | 持久化 |
|-----|------|------|--------|
| **Message Buffer** | 最近对话消息 | 上下文窗口 | 临时 |
| **Core Memory** | 结构化记忆块（用户偏好、人设、任务目标） | 上下文窗口（pinned） | 自动 |
| **Recall Memory** | 完整对话历史，可搜索检索 | 外部存储 | 自动落盘 |
| **Archival Memory** | 显式知识库（向量/图数据库） | 外部存储 | 需配置 |

### 3. 关键技术

#### Message Eviction & Summarization
- **Eviction**: 上下文满时智能淘汰（建议只淘汰 70%，保持连续性）
- **Recursive Summarization**: 被逐出的消息与已有摘要合并，老消息影响递减

#### Memory Blocks
- 结构化、可编辑的上下文单元
- 组成：label + description + value + character limit
- Agent 可通过工具自主更新自己的记忆块
- 支持"睡眠代理"（sleep-time agents）异步优化记忆

#### External Storage & Retrieval
- **Vector DB**: 嵌入+向量检索
- **Graph DB**: 关系遍历，处理连接信息
- **关键区分**: RAG 是工具，不是记忆本身

---

## 工程系统案例

### MemGPT: OS 视角的内存管理
- 将上下文窗口视为**受限内存资源**
- 实现 OS 风格的**内存层级**：
  - Core Memory = RAM（快速，在上下文内）
  - Archival/Recall = Disk（外部存储）
- LLM 通过 function call 自主管理内存分页（page in/out）
- 提供"无限上下文"的幻觉

### Sleep-Time Compute: 异步记忆优化
- **非阻塞**: 记忆管理与对话解耦，不拖慢响应
- **主动精炼**: 空闲期重组、压缩、提升记忆质量
- 对比 MemGPT 的惰性增量更新，质量更高

---

## 人类记忆 vs Agent 记忆

| 人类记忆 | Agent 记忆 |
|---------|-----------|
| 神经生物学基础 | 纯文本输入输出 |
| 自动编码 | 需显式上下文工程 |
| 情感标记 | 无情感，纯 token |

**核心原则**: 不要硬编码人类记忆结构，而应设计有效的上下文管理系统。

---

## 原文摘录

> "Agent memory is what and how your agent remembers information over time."

> "Designing an agent's memory is essentially context engineering: determining which tokens enter the context window and how they're organized."

> "The future of agent memory lies not in any single technique but in the thoughtful combination of multiple approaches: careful eviction and summarization, intelligent management of memory blocks, and sophisticated systems for storing and retrieving external context."

> "RAG is a tool for agent memory, it is not 'memory' in of itself."

---

## 关联概念

- [[memgpt]] — MemGPT 论文：LLM as OS
- [[llm-os]] — AIOS: LLM Agent Operating System
- [[context-engineering]] — 上下文工程
- [[scaffolded-llms-natural-language-computers]] — 内存层级理论
- [[agent-harness]] — Agent 基础设施
- [[rag]] — Retrieval-Augmented Generation

---

## 评价与影响

- **实践导向**: 从 MemGPT 研究到 Letta 产品，理论到工程的完整路径
- **术语清晰**: 明确区分了 Message Buffer / Core / Recall / Archival 四层记忆
- **关键洞察**: 记忆 = 上下文工程，RAG ≠ 记忆
- **与 Harness Engineering 的关系**: 记忆管理是 Harness 的核心模块之一（见 [[agent-harness]]）
