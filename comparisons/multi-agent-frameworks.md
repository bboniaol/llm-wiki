# 多 Agent 编排框架比较

## 基本信息
- **主题**: AutoGen vs CrewAI vs OpenAI Swarm vs LangChain Agents
- **来源**: 多篇技术博客、论文、官方文档综合
- **标签**: #multi-agent #orchestration #autogen #crewai #swarm #langchain #comparison

---

## 一句话总结

多 Agent 编排框架的核心差异在于**协作模型**：AutoGen 强调对话式迭代推理，CrewAI 强调角色化任务流，OpenAI Swarm 强调极简轻量，LangChain 强调模块化可组合——选择取决于场景复杂度、团队规模和可控性需求。

---

## 框架概览

| 框架 | 作者/维护方 | 核心哲学 | 最佳场景 |
|-----|-----------|---------|---------|
| **AutoGen** | Microsoft Research | 对话即计算：Agent 通过多轮对话协作解决问题 | 复杂推理、代码生成、需要迭代调试的任务 |
| **CrewAI** | João Moura (社区) | 角色扮演：预定义角色 + 任务 + 团队 | 业务流程自动化、角色明确的团队协作 |
| **OpenAI Swarm** | OpenAI | 极简轻量：轻量级多 Agent 编排 | 简单多 Agent 路由、快速原型 |
| **LangChain/LangGraph** | LangChain Inc. | 模块化：可组合的 Agent 构建块 | 需要高度定制、与现有工具链集成 |

---

## 详细对比

### AutoGen (Microsoft)

**核心抽象**
- **ConversableAgent**: 可对话的 Agent 基类
- **UserProxyAgent**: 代表用户的 Agent，可执行代码
- **AssistantAgent**: LLM 驱动的助手 Agent
- **GroupChat**: 多 Agent 群聊管理

**协作模型**
```
UserProxy → Assistant → (代码执行/工具调用) → Assistant → ...
         ↑___________________________________________↓
```
- **对话驱动**: Agent 通过自然语言对话协作
- **人机协作**: 用户可随时介入
- **代码执行**: Assistant 生成代码，UserProxy 执行

**优势**
- 强大的代码生成和执行能力
- 灵活的人机协作模式
- 适合复杂推理任务（数学、编程）

**劣势**
- 学习曲线陡峭
- 对话流程难以精确控制
- 调试复杂

---

### CrewAI

**核心抽象**
- **Agent**: 有角色、目标、背景故事的 Agent
- **Task**: 具体任务，可分配给 Agent
- **Crew**: Agent + Task 的组合，按流程执行
- **Process**: 执行模式（sequential, hierarchical）

**协作模型**
```
Researcher Agent → Writer Agent → Reviewer Agent
     ↓                  ↓              ↓
   [Task 1]         [Task 2]       [Task 3]
```
- **角色化**: 每个 Agent 有明确的角色和职责
- **任务流**: 预定义的任务序列或层级
- **工具共享**: Agent 可共享工具

**优势**
- 直观的角色-任务映射
- 适合业务流程建模
- 社区活跃，模板丰富

**劣势**
- 灵活性不如 AutoGen
- 复杂动态协作支持有限
- 对非结构化任务支持较弱

---

### OpenAI Swarm

**核心抽象**
- **Agent**: 极简定义（instructions + functions）
- **Handoff**: Agent 之间的交接机制
- **Result**: 执行结果

**协作模型**
```
Router Agent → (handoff) → Specialist Agent A
           → (handoff) → Specialist Agent B
```
- **轻量级**: 核心代码仅约 100 行
- **显式路由**: Agent 主动决定交接给谁
- **函数调用驱动**: 通过 function calling 切换 Agent

**优势**
- 极简，易理解
- 与 OpenAI API 深度集成
- 适合简单路由场景

**劣势**
- 功能极简，复杂场景需自行扩展
- 无内置记忆管理
- 生态较小

---

### LangChain / LangGraph

**核心抽象**
- **Chain**: 可组合的 LLM 调用序列
- **Agent**: ReAct、Plan-and-Execute 等模式
- **LangGraph**: 基于图的状态机编排
- **Tool**: 外部工具封装

**协作模型**
```
[Node: Agent A] → [Node: Tool Call] → [Node: Agent B]
      ↓                                    ↓
   [Edge: condition] ← [State] → [Edge: condition]
```
- **图编排**: 基于有向图的状态流转
- **状态共享**: 节点间共享状态
- **条件路由**: 边可带条件判断

**优势**
- 极度灵活，可定制任何流程
- 生态最丰富（工具、集成、模板）
- LangGraph 适合复杂状态机

**劣势**
- 概念多，学习成本高
- 需要较多胶水代码
- 容易过度工程化

---

## 选择决策树

```
需要多 Agent 协作？
  ├─ 否 → 单 Agent 即可，用 LangChain 或裸 LLM
  └─ 是 → 协作复杂度？
       ├─ 简单路由 → OpenAI Swarm
       ├─ 角色化流程 → CrewAI
       ├─ 对话式迭代 → AutoGen
       └─ 复杂状态机/高度定制 → LangGraph
```

---

## 与 Harness Engineering 的关系

- **多 Agent 编排 = Harness 的"进程调度"层**
- 各框架对应不同的调度策略：
  - AutoGen = 协作式调度（对话协商）
  - CrewAI = 批处理调度（预定义流水线）
  - Swarm = 事件驱动调度（handoff）
  - LangGraph = 状态机调度（图遍历）
- **生产建议**: 将编排框架作为 Harness 的一个可插拔模块

---

## 关联概念

- [[agent-harness]] — Agent 基础设施
- [[llm-os]] — AIOS: Agent 操作系统（含调度器）
- [[agent-memory]] — Agent 记忆设计
- [[agent-tool-use]] — 工具调用机制
- [[autogen]] — AutoGen 详细文档
- [[crewai]] — CrewAI 详细文档
- [[langgraph]] — LangGraph 详细文档

---

## 评价

- **2024-2025 趋势**: 框架收敛，从"百花齐放"走向"场景适配"
- **关键洞察**: 没有"最好"的框架，只有"最适合"的框架
- **未来方向**: 标准化 Agent 协议（如 A2A、ANP），框架间互操作
