# MemGPT: Towards LLMs as Operating Systems

## 基本信息
- **论文**: MemGPT: Towards LLMs as Operating Systems
- **作者**: Charles Packer, Sarah Wooders, Kevin Lin, Vivian Fang, Shishir G. Patil, Ion Stoica, Joseph E. Gonzalez (UC Berkeley)
- **发布时间**: 2023-10 (arXiv), 2024-02 (修订)
- **arXiv**: https://arxiv.org/abs/2310.08560
- **代码**: https://research.memgpt.ai
- **标签**: #agent #memory #os #virtual-context-management #memory-hierarchy #function-calling

---

## 一句话总结

MemGPT 通过**虚拟上下文管理**（借鉴 OS 虚拟内存分页机制），让固定上下文窗口的 LLM 能够自主地在"主存"（上下文）和"磁盘"（外部存储）之间分页数据，从而提供**无限上下文的幻觉**，支持超长文档分析和跨会话记忆。

---

## 核心架构

```
┌─────────────────────────────────────────┐
│           User / Application            │
├─────────────────────────────────────────┤
│      MemGPT OS Layer (Controller)       │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐   │
│  │ Main    │ │ Virtual │ │ External│   │
│  │ Context │ │ Context │ │ Storage │   │
│  │ (RAM)   │ │ Manager │ │ (Disk)  │   │
│  └─────────┘ └─────────┘ └─────────┘   │
├─────────────────────────────────────────┤
│      LLM (Fixed Context Window)         │
│         GPT-4 / Claude / etc.           │
└─────────────────────────────────────────┘
```

---

## 核心机制

### 1. 虚拟上下文管理 (Virtual Context Management)
- **灵感来源**: OS 虚拟内存分页（Paging）
- **核心思想**: 在固定大小的物理内存（上下文窗口）上，提供无限虚拟内存的抽象
- **实现方式**: LLM 通过 function calling 自主读写外部存储

### 2. 内存层级 (Memory Hierarchy)

| 层级 | 类比 OS | 功能 | 访问速度 |
|-----|--------|------|---------|
| **Main Context** | RAM | 当前任务所需的即时上下文 | 极快（直接输入） |
| **Working Context** | 工作集 | 当前会话的临时数据 | 快（function call） |
| **Recall Storage** | 磁盘 | 历史对话、长期记忆 | 慢（检索+加载） |

### 3. Function Calls as System Calls
- LLM 输出 function call 来管理自身状态：
  - `page_in(data_id)`: 从外部存储加载数据到上下文
  - `page_out(data_id)`: 将上下文数据写入外部存储
  - `replace_context(new_context)`: 替换上下文内容
  - `yield_control()`: 将控制权交还给用户
- **类比**: 这些 function calls 相当于 OS 的 system calls

### 4. 中断机制 (Interrupts)
- 用户输入 = 中断信号
- MemGPT 控制器处理中断，决定：
  - 是否将用户输入放入上下文
  - 是否需要先 page in 相关记忆
  - 何时 yield 控制权返回用户

---

## 评估场景

### 场景 1: 超长文档分析
- **挑战**: 文档长度远超 LLM 上下文窗口
- **MemGPT 方案**: 
  - 将文档分块存储在外部
  - LLM 按需 page in 相关段落
  - 支持跨段落推理和引用

### 场景 2: 多会话聊天
- **挑战**: 长期对话中保持人设、记忆、上下文一致性
- **MemGPT 方案**:
  - 核心记忆（人设、用户偏好）常驻主上下文
  - 历史对话存储在 recall storage
  - 需要时检索相关历史
  - 支持"反思"和"进化"

---

## 与相关工作的关系

| 工作 | 关系 |
|-----|------|
| **AIOS (LLM OS)** | MemGPT 是 AIOS 的"内存管理子系统"具体实现 |
| **Scaffolded LLM** | MemGPT 是 Millidge 理论中"内存层级"的工程实践 |
| **Letta** | MemGPT 的后续产品化，扩展了 sleep-time compute |
| **传统 OS 虚拟内存** | 直接借鉴分页、工作集、中断等概念 |

---

## 原文摘录

> "We propose virtual context management, a technique drawing inspiration from hierarchical memory systems in traditional operating systems which provide the illusion of an extended virtual memory via paging between physical memory and disk."

> "Using function calls, LLM agents can read and write to external data sources, modify their own context, and choose when to return responses to the user."

> "We treat context windows as a constrained memory resource, and design a memory hierarchy for LLMs analogous to memory tiers used in traditional OSes."

---

## 关联概念

- [[agent-memory]] — Letta 的博客：Agent Memory 设计指南
- [[llm-os]] — AIOS: LLM Agent Operating System
- [[scaffolded-llms-natural-language-computers]] — 内存层级理论框架
- [[agent-harness]] — Agent 基础设施
- [[virtual-memory]] — 操作系统虚拟内存

---

## 评价与影响

- **开创性**: 最早将 OS 虚拟内存概念系统性地应用于 LLM 上下文管理
- **工程验证**: 在文档分析和多会话聊天两个场景验证有效
- **产品化路径**: MemGPT → Letta，从研究到商业产品的成功转化
- **与 Harness Engineering 的关系**: MemGPT 是 Harness 中"内存管理模块"的标杆实现
