# Agent Harness: Critical Infrastructure for AI Agents

## 基本信息
- **作者**: Roberto Dias Duarte
- **发布时间**: 2024
- **来源**: https://www.robertodiasduarte.com.br/en/agent-harness-infraestrutura-critica-para-agentes-de-ia/
- **标签**: #agent #harness #infrastructure #orchestration #memory #tools

---

## 一句话总结

Agent Harness 是将**无状态 LLM 转化为自治 Agent** 的关键基础设施，负责编排、上下文管理、工具调用、记忆读写和错误处理，是 Agent 系统的"操作系统内核"。

---

## 核心论点

1. **LLM 本身不是 Agent**
   - 原始 LLM 是无状态的、被动的、单轮响应的。
   - 要让它成为 Agent，需要一个 **Harness（ harness = 马具/挽具）** 来驾驭它。

2. **Harness 的核心职责**

| 模块 | 功能 |
|-----|------|
| **编排 (Orchestration)** | 管理 Agent 的执行循环、决策流程、状态机 |
| **上下文管理** | 维护对话历史、系统提示、任务上下文 |
| **工具管理** | 注册、发现、调用外部工具/API |
| **记忆管理** | 短期记忆（上下文）+ 长期记忆（向量存储） |
| **错误处理** | 重试、降级、异常恢复、日志记录 |
| **安全与权限** | 访问控制、沙箱、审计 |

3. **Harness 作为"操作系统"**
   - 类比：LLM = CPU，Harness = OS Kernel
   - 没有 OS，CPU 只是硅片；没有 Harness，LLM 只是文本生成器。
   - Harness 提供进程管理（Agent 实例）、内存管理（上下文/记忆）、I/O（工具/环境交互）。

---

## 关键洞察

### 为什么 Harness 是"关键基础设施"
- **可靠性**：生产级 Agent 不能依赖裸 LLM 的随机性。
- **可观测性**：需要追踪 Agent 的每一步决策、工具调用、记忆读写。
- **可扩展性**：支持多 Agent 协作、分布式执行。
- **安全性**：防止工具滥用、提示注入、无限循环。

### Harness 与 Scaffolded LLM 的关系
- **Scaffolded LLM**（Millidge 2023）= 理论框架：LLM 是 NLPU，需要脚手架。
- **Agent Harness** = 工程实现：具体的 harness 代码/系统来实现这个脚手架。
- 二者是**理论与实践**的对应。

### Harness 的层次结构
```
┌─────────────────────────────────────┐
│  Agent Application (业务逻辑)        │
├─────────────────────────────────────┤
│  Agent Harness (编排/记忆/工具/错误)  │
├─────────────────────────────────────┤
│  LLM Provider (OpenAI/Anthropic/...)│
├─────────────────────────────────────┤
│  Foundation Model (GPT-4/Claude/...)  │
└─────────────────────────────────────┘
```

---

## 原文摘录

> "Agent Harness is the infrastructure that transforms a stateless LLM into an autonomous agent, managing orchestration, context, tools, memory, error handling."

> "Without a harness, an LLM is just a text generator. With a harness, it becomes a computational agent capable of autonomous decision-making."

---

## 关联概念

- [[scaffolded-llms-natural-language-computers]] — Beren Millidge 的理论框架
- [[llm-os]] — LLM Agent Operating System (AIOS)
- [[agent-architecture]] — Agent 架构设计模式
- [[multi-agent-orchestration]] — 多 Agent 编排
- [[agent-memory]] — Agent 记忆系统设计
- [[agent-tool-use]] — Agent 工具调用机制

---

## 评价与影响

- **工程导向**：相比 Millidge 的理论文章，本文更侧重工程实现和基础设施视角。
- **术语普及**：推动了 "Agent Harness" 作为一个独立概念被讨论，不再只是 "Agent Framework" 的别名。
- **与 Harness Engineering 的关系**：直接对应用户关注的 harness engineering 方向——如何构建生产级的 Agent 基础设施。
