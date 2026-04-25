---
title: Agent 架构思维导图与学习导航
created: 2026-04-25
updated: 2026-04-25
type: query
tags: [query-note, harness-engineering, agentic-engineering, system-map, study-plan]
sources: [queries/harness-engineering-system-map.md, queries/harness-engineering-7-day-study-plan.md, concepts/scaffolded-llms-natural-language-computers.md, concepts/agent-harness.md, concepts/llm-os.md, concepts/agent-memory.md, concepts/memgpt.md, comparisons/multi-agent-frameworks.md]
---

# Agent 架构思维导图与学习导航

## 问题

当前知识库已有 84 页，涵盖 harness engineering、agent 基础设施、记忆、评测、平台化等大量概念。用户感到"太多太乱"，需要一张**完整的思维导图 + 一步一步的学习路径**，把概念按层次串起来，并给出可执行的学习计划。

## 短答案

Agent 架构可以从两个互补视角理解：
1. **计算机架构视角**（理论层）：LLM = CPU，Harness = 操作系统，Agent = 应用程序
2. **工程系统视角**（实践层）：从概念边界 → 事实底座 → 上下文记忆 → 执行控制 → 工作流纠偏 → 稳定性评测 → 平台组织 → 前沿演化

本文把这两个视角合成一张**十层思维导图**，并给出**7 天渐进学习路径**。

---

## 十层思维导图（总览）

```text
Agent 架构全景
│
├─ 理论根基层（计算机架构类比）
│  ├─ [[scaffolded-llms-natural-language-computers]] — LLM = NLPU，Scaffold = 冯·诺依曼架构
│  ├─ [[agent-harness]] — Harness = 将无状态 LLM 转化为自治 Agent 的基础设施
│  └─ [[llm-os]] — AIOS = LLM 的操作系统内核（调度/上下文/内存/工具/访问控制）
│
├─ 1. 概念边界层
│  ├─ [[harness-engineering]] — 系统支架工程
│  ├─ [[framework-vs-runtime-vs-harness]] — 构建层 vs 执行层 vs 支架层
│  └─ [[harness-vs-context-vs-agentic-engineering]] — 三种常被混用的视角
│
├─ 2. 事实底座层
│  ├─ [[repo-as-system-of-record]] — 仓库作为事实母体
│  ├─ [[agent-readable-repositories]] — Agent 可导航的仓库
│  └─ [[doc-gardening-agents]] — 文档持续修剪
│
├─ 3. 上下文与记忆层
│  ├─ [[context-engineering]] — 上下文组织与注入
│  ├─ [[progressive-disclosure]] — 按需暴露
│  ├─ [[agent-memory-patterns]] — 四层记忆模型
│  ├─ [[context-constitution]] — 上下文治理原则
│  ├─ [[long-running-agent-tasks]] — 跨会话接棒
│  ├─ [[agent-memory]] — Letta 记忆设计（Message/Core/Recall/Archival）
│  └─ [[memgpt]] — MemGPT 虚拟上下文管理（OS 内存分页）
│
├─ 4. 执行边界与控制面层
│  ├─ [[agent-sandboxing]] — 隔离环境
│  ├─ [[agent-approval-patterns]] — 审批策略
│  ├─ [[agent-observability]] — 可观测性
│  └─ [[approval-vs-sandbox-vs-observability]] — 三者职责对比
│
├─ 5. 工作流与纠偏闭环层
│  ├─ [[coding-agent-workflow-patterns]] — 任务拆解→实现→验证→PR
│  ├─ [[agent-feedback-loops]] — 测试/日志/审查信号修正
│  ├─ [[evaluator-driven-qa]] — 生成与验收角色拆分
│  ├─ [[multi-agent-delegation]] — 多 Agent 协作
│  └─ [[deterministic-backpressure-vs-durable-retries]] — 信号质量 vs 恢复能力
│
├─ 6. 稳定性与评测层
│  ├─ [[agent-reliability-patterns]] — 约束/验证/隔离/回滚
│  ├─ [[coding-agent-evals]] — 真实任务评测
│  ├─ [[coding-agent-reliability-stack]] — 六层可靠性方法图
│  ├─ [[minimum-viable-agent-harness-checklist]] — 最小落地清单
│  └─ [[how-to-read-agent-harness-benchmarks]] — Benchmark 阅读指南
│
├─ 7. 多 Agent 编排层
│  ├─ [[multi-agent-frameworks]] — AutoGen/CrewAI/Swarm/LangGraph 对比
│  └─ [[multi-agent-delegation]] — 委派模式与协作策略
│
├─ 8. 平台化与组织层
│  ├─ [[cloud-agent-operations]] — 云端后台执行
│  ├─ [[from-local-coding-agent-to-team-agent-platform]] — 六阶段演进
│  ├─ [[coding-agent-org-design-patterns]] — 组织职责地图
│  ├─ [[coding-agent-governance-checklist]] — 上线前检查
│  ├─ [[coding-agent-maturity-model]] — 五级成熟度
│  ├─ [[managed-harness-vs-open-harness]] — 托管 vs 开放路线
│  └─ [[three-platform-archetypes-for-coding-agents]] — 三条平台路线
│
└─ 9. 前沿演化层
   ├─ [[natural-language-agent-harnesses]] — Harness 外化为自然语言工件
   ├─ [[intelligent-harness-runtime]] — 共享语义运行时
   ├─ [[extreme-harness-engineering]] — 极端编排：Symphony/dark factory
   ├─ [[symphony]] — Issue → Autonomous Implementation Run
   ├─ [[entangled-software]] — 软件与组织双向塑形
   └─ [[meta-harness]] — Harness 自动优化（Stanford IRIS Lab）
```

---

## 两个互补视角的关系

| 视角 | 核心隐喻 | 解决什么问题 | 代表页面 |
|-----|---------|-----------|---------|
| **计算机架构视角** | LLM = CPU，Harness = OS | "Agent 系统本质上是什么" | [[scaffolded-llms-natural-language-computers]], [[agent-harness]], [[llm-os]] |
| **工程系统视角** | 八层系统建设 | "怎么一步步建出生产级 Agent" | [[harness-engineering-system-map]] 的 8 层 |

**关系**：计算机架构视角告诉你"为什么这样设计"，工程系统视角告诉你"怎么落地"。二者互补，缺一不可。

---

## 7 天渐进学习路径（修订版）

基于已有的 [[harness-engineering-7-day-study-plan]]，结合本次新增的理论根基层和多 Agent 编排层，修订如下：

### Day 1（工作日 / 2h）— 先建立"Agent 是什么"的总框架
**阅读**：
1. [[scaffolded-llms-natural-language-computers]] — 理解 LLM = NLPU 的核心隐喻
2. [[agent-harness]] — 理解 Harness 的本质职责
3. [[harness-engineering]] — 理解工程视角的总定义

**输出**：写一段自己的定义，包含：LLM 是 CPU，Harness 是 OS，Agent 是 App。

**检查问题**：为什么"给 LLM 加几个工具"不等于已经有了 Harness？

---

### Day 2（工作日 / 2h）— 概念边界与事实底座
**阅读**：
1. [[framework-vs-runtime-vs-harness]]
2. [[harness-vs-context-vs-agentic-engineering]]
3. [[repo-as-system-of-record]]
4. [[agent-readable-repositories]]

**输出**：一张三列表：什么属于 framework、什么属于 runtime、什么属于 harness。

**检查问题**：如果一个产品只强调"模型强+工具多+有 runtime"，但不讲 verification、approval、state，它 harness 成熟吗？

---

### Day 3（工作日 / 2h）— 上下文与记忆（理论+工程）
**阅读**：
1. [[context-engineering]]
2. [[agent-memory-patterns]]
3. [[agent-memory]] — Letta 四层记忆
4. [[memgpt]] — OS 虚拟内存视角

**输出**：对比 Millidge 的"内存层级理论"与 Letta 的"四层记忆工程实现"，写 3 个对应关系。

**检查问题**：为什么"加一个 memory plugin"通常不等于解决了 agent memory？

---

### Day 4（工作日 / 2h）— 执行控制与工作流
**阅读**：
1. [[agent-sandboxing]]
2. [[agent-approval-patterns]]
3. [[coding-agent-workflow-patterns]]
4. [[agent-feedback-loops]]

**输出**：一个最小控制面模板：自动放行 / 必须审批 / 必须保留证据。

**检查问题**：为什么"我已经做了审批"不能替代 sandbox 和 observability？

---

### Day 5（工作日 / 2h）— 评测、可靠性与多 Agent 编排
**阅读**：
1. [[evaluator-driven-qa]]
2. [[agent-reliability-patterns]]
3. [[multi-agent-frameworks]] — 四框架对比
4. [[multi-agent-delegation]]

**输出**：一张表：什么场景用 AutoGen、什么用 CrewAI、什么用 Swarm、什么用 LangGraph。

**检查问题**：多 Agent 编排中，"协作式调度"（AutoGen）和"批处理调度"（CrewAI）各适合什么任务类型？

---

### Day 6（周末 / 4-5h）— 平台化与系统地图
**阅读**：
1. [[coding-agent-reliability-stack]]
2. [[minimum-viable-agent-harness-checklist]]
3. [[from-local-coding-agent-to-team-agent-platform]]
4. [[coding-agent-maturity-model]]
5. [[managed-harness-vs-open-harness]]
6. [[harness-engineering-system-map]] — 总地图复习

**输出**：一张自己的三列表：最小 harness 能力 / 团队级平台才需要的 / 警惕的 lock-in 问题。

**检查问题**：如果你现在要做 Spring Boot 微服务 Agent 平台，最不该过早投入的是哪一层？

---

### Day 7（周末 / 4-6h）— 前沿演化与总复习
**阅读**：
1. [[natural-language-agent-harnesses]]
2. [[intelligent-harness-runtime]]
3. [[extreme-harness-engineering]]
4. [[meta-harness]] — Harness 自动优化
5. [[llm-os]] — AIOS 系统层视角
6. 本文（总复习）

**输出**：一页总结："我现在如何理解 Agent 架构，以及它未来会往哪长"

至少回答：
1. Agent 架构的核心对象是什么？
2. Memory / Context / Workflow / Governance / Orchestration 各守什么职责？
3. 今天最值得学的结构是什么？什么太前沿不该直接照抄？
4. 如果要落地，会从哪一层开始？

**检查问题**：你会不会直接照着 Symphony / dark factory 路线做？如果不会，你会抽走哪些结构，保留哪些原则？

---

## 一周后的达标标准

能稳定回答：
1. **理论层**：LLM = CPU，Harness = OS，Agent = App 的完整映射是什么？
2. **工程层**：harness / framework / runtime / context / agentic engineering 的边界？
3. **记忆层**：Millidge 的内存层级 vs Letta 的四层记忆 vs MemGPT 的虚拟上下文，三者关系？
4. **控制层**：sandbox / approval / observability 各守什么职责？
5. **编排层**：AutoGen / CrewAI / Swarm / LangGraph 各适合什么场景？
6. **平台层**：managed / open / platform workbench 三条路线分别适合什么阶段？
7. **前沿层**：NLAH、IHR、Meta-Harness、AIOS 各代表什么演化方向？

---

## 怎么用这张地图读新材料

以后看到任何 Agent 产品、论文、文章，按这 4 步扫：

1. **它在补哪一层？**（理论/概念/底座/上下文/控制/工作流/评测/编排/平台/前沿）
2. **它解决的是哪个缺口？**（context / state / control / verification / orchestration / governance）
3. **它让系统更稳，还是让 demo 更顺？**
4. **它是局部技巧，还是能进入平台和组织层的长期结构？**

---

## 关联页面

- [[harness-engineering-system-map]] — 八层工程系统地图（更详细的工程视角）
- [[harness-engineering-7-day-study-plan]] — 原版 7 天学习路线
- [[scaffolded-llms-natural-language-computers]] — 理论根基
- [[agent-harness]] — Harness 基础设施定义
- [[llm-os]] — LLM 操作系统
- [[multi-agent-frameworks]] — 多 Agent 编排框架对比

## 来源

- [[queries/harness-engineering-system-map]]
- [[queries/harness-engineering-7-day-study-plan]]
- [[concepts/scaffolded-llms-natural-language-computers]]
- [[concepts/agent-harness]]
- [[concepts/llm-os]]
- [[concepts/agent-memory]]
- [[concepts/memgpt]]
- [[comparisons/multi-agent-frameworks]]
