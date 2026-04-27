# Context Engineering: Going Beyond Prompts To Push AI

**来源**: simple.ai newsletter — Dharmesh Shah (HubSpot/Shopify)
**日期**: 2026-04-26
**标签**: context-engineering, prompt-engineering, LLM, agent-design

---

## 核心论点

Context Engineering 是 Prompt Engineering 的进化版：
- **Prompt Engineering** = 优化"如何问"（how you ask）
- **Context Engineering** = 优化"AI 思考时可访问什么"（what the AI has access to when it thinks）

> "Prompting tells the model how to think, but context engineering gives the model the training and tools to get the job done."
> — Dharmesh Shah

---

## 关键概念

### 1. Context Window 是什么？
- 想象成一张大纸，传递给 LLM
- 限制以 token 计（约 ¾ 个英文单词）
- 计费、延迟、内存都与 token 数线性相关
- 关键限制：LLM 只知道训练数据和 context window 中提供的内容

### 2. 两年内的爆炸式增长
- 4K → 1M+ tokens
- 可放入整个代码库、完整商业计划、数月客服对话

### 3. AI "记忆"对话的机制
- 不是真正的记忆
- 后台将历史 prompt + 输出放入 context window
- 类比电影《记忆碎片》(Memento)：主角忘记一切，靠身上笔记回忆

### 4. RAG (Retrieval-Augmented Generation)
- 找到与用户 prompt 相关的文档集
- 将这些文档传入 context window
- 相当于"现场教学"LLM

### 5. Tool Calling 的巧妙设计
- LLM 不直接调用工具
- 核心 LLM 只接收输入、产生输出
- 应用层告诉 LLM 有哪些工具可用
- LLM 输出想调用的工具 → 应用层执行 → 结果放回 context window → 再传给 LLM
- 这是对 LLM "只能处理 context window" 这一限制的优雅 workaround

---

## Context Engineer 的实际工作

| 职责 | 说明 |
|------|------|
| **Curate** | 决定每个任务需要哪些文档、记忆、API |
| **Structure** | 按最优顺序排列：system messages → tools → retrieved data → user prompt |
| **Compress** | 摘要或分块，在 token 限制内保留关键信息 |
| **Evaluate** | 测量准确率，防范"context dilution"（无关信息干扰模型） |

---

## 为什么 Context Engineering 比 Prompt Engineering 更重要

| Prompt Engineering | Context Engineering |
|-------------------|---------------------|
| 学习提出好问题 | 像图书管理员决定读者能访问哪些书 |
| 优化句子 | 优化知识结构 |
| 2023 年 hype，薪资 $300k+ | 2024+ 的核心竞争力 |
| 人人都会了 | 需要信息架构、数据策略、UX 思维 |

**关键洞察**：成本与延迟与 context window 长度大致线性增长，这为 Context Engineer 留下了大量优化空间。

---

## 与 Claude Code 论文的关联

这篇 newsletter 与 arxiv 2604.14228 (Dive into Claude Code) 形成互补：

| 论文侧重 | 本文侧重 |
|----------|----------|
| 系统架构（权限、压缩管道、子代理） | 概念框架（context vs prompt） |
| 实现层面（五层压缩、CLAUDE.md 层次） | 思维层面（信息架构、知识策展） |
| 工程化落地 | 设计哲学 |

**共同主题**：两者都强调"给模型正确的上下文"比"给模型更好的指令"更重要。

---

## 对你项目的启示

1. **你的 Spring Boot Agent 平台需要 context 管理模块**：
   - 不是简单的 prompt template
   - 而是动态的 context 组装、压缩、检索系统

2. **RAG + Tool Calling 是核心**：
   - 论文中的 MCP / plugins / skills / hooks 四层扩展
   - 对应本文的"决定 AI 能访问什么"

3. **Context dilution 是真实风险**：
   - 论文中的五层压缩管道（budget/snip/microcompact/collapse/auto-compact）
   - 正是为了解决"无关信息干扰"问题

---

## 关键引用

> "The prompt engineering era taught us to talk to AI. The context engineering era is teaching us to think with AI."

> "Context engineering requires thinking about information architecture, data strategy, and user experience in ways prompt engineering never did."

> "The companies who master this will have a massive competitive advantage."
