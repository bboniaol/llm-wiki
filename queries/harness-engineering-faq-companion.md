---
title: Harness Engineering FAQ — 从理论到生产的 9 个关键决策
created: 2026-04-24
updated: 2026-04-24
type: query
tags: [query-note, harness-engineering, best-practice, reliability, workflow, anti-pattern]
sources: [raw/articles/ltbase-harness-engineering-faq-2026-04-24.md, raw/articles/ltbase-harness-engineering-2026-04-24.md]
---

# Harness Engineering FAQ — 从理论到生产的 9 个关键决策

## 问题
[[lychee-technology]] 的 companion FAQ 回答了 9 个从实验 agent 过渡到生产系统时的核心工程决策。这些问题不是 prompt 技巧，而是系统设计问题。本文档把 9 个回答 + 5 个反模式 + 实现优先级收敛成一张可直接参考的判断地图。

## 9 个关键决策

### Q1: 为什么用了 RAG，搜索工具还会造成上下文溢出？
**核心区别**: RAG chunks 是预处理、清洗、大小受限的；原始 web search 返回的是无结构、无边界、带 HTML 标签和重复片段的原始材料。

**生产教训**: 很多推理层会**静默截断**溢出的上下文，而不是报错。模型在不知情的情况下基于残缺信息推理。

**修复**: Tool 层必须做三件事 — ranking（BM25/embedding）、deduplication、hard token budget。
> **Rule of thumb**: Never pass raw tool output directly to the model.

**与现有知识的关联**: 与 [[harness-engineering]] 中 Tool 层的"Token Budget Truncation"直接对应；也与 [[context-engineering]] 中"渐进披露"原则兼容。

---

### Q2: 为什么用确定性验证节点，而不是 LLM-based prompt check？
**核心区别**: 让 LLM "确保输出是合法 JSON" 是一个 hope — 它是概率性的、慢的、会幻觉的。Pydantic/jq 这类代码验证器要么通过要么失败，附带结构化错误追踪，没有歧义。

**修复**: Harness 必须在每个 LLM 输出传播前拦截它，跑过相关验证器，失败时把 exact error 回传给模型做 localized retry。模型永远不应该看到自己 malformed output 的下游后果。
> **Rule of thumb**: If a check can be deterministic, it must not be delegated to an LLM.

**与现有知识的关联**: 与 [[agent-reliability-patterns]] 中"验证闭环"和 [[evaluator-driven-qa]] 中"执行验证而非文本判断"完全一致。

---

### Q3: LLM 能严格遵循生成的 DAG 吗？
**答案**: 不能，也不应该。

LLM 的工作止于生成计划（DAG 或 JSON workflow）。Harness 内的专用执行引擎读取 DAG 并运行它。模型不控制执行流。

**三个好处**:
- **Security**: 引擎处理 credential 注入，模型永远看不到 OAuth/API key
- **Determinism**: 计划锁定后执行顺序不会漂移
- **Observability**: 每步独立可日志、可检查、可重试

**关键警告**: DAG 必须被视为 untrusted input — 模型可能生成语法合法但逻辑不安全的计划。
> **Rule of thumb**: The model proposes. The harness disposes.

**与现有知识的关联**: 与 [[coding-agent-workflow-patterns]] 中"计划驱动型执行"和 [[harness-engineering]] 中 Orchestration 层的职责完全一致。

---

### Q4: 怎么判断一个生成的计划是否"好"？
三个 production-readiness 属性：

| 属性 | 含义 | 反例 |
|------|------|------|
| **Granularity** | 步骤代表稳定的高层工作单元 | "调用内部 API v2.3 的 /fetch 端点" |
| **Separation of Concerns** | 状态持久化、重试、错误处理不属于计划 | 计划里写"如果失败就重试 3 次" |
| **Observability** | 每步独立可追踪、可重试 | 一步崩了必须从头跑才能 debug |

> **Rule of thumb**: A good plan is one you can debug step-by-step under production conditions.

**与现有知识的关联**: 与 [[coding-agent-workflow-patterns]] 中"设计原则"和 [[agent-observability]] 直接相关。

---

### Q5: 状态应该存在文件还是数据库里？
**答案**: 本地开发用文件可以；生产环境必须外置。

在 K8s / serverless 环境中，下一次请求不一定落在同一个实例上。一个容器写的 `state.json` 对另一个容器不可见。

**推荐分层存储**:
- **Redis** — 快速、易失的执行状态（当前 DAG 节点、进行中子任务）
- **PostgreSQL** — 持久、可查询的恢复状态（审计日志、已完成任务历史、可恢复会话）

> **Rule of thumb**: Use fast storage for execution state, durable storage for recovery state.

**与现有知识的关联**: 与 [[agent-memory-patterns]] 中 Working Memory vs Persistent State 的分层完全一致；也与 [[long-running-agent-tasks]] 中跨 session 恢复需求对应。

---

### Q6: 工具逻辑是固定的，为什么还要验证工具输出？
**答案**: 因为工具的环境不是固定的。

两个持续出现的生产故障模式：
- **API Drift**: 外部 API 格式变化对人类不可见但破坏下游解析器。 `"status": "active"` 可能静默变成 `"status": 1`
- **Data Defects**: 爬虫和第三方 API 返回不完整或畸形数据 — 缺失字段、嵌入 HTML、null 值出现在数字位置

**修复**: 边界验证 — 在入口处拒绝不符合 schema 的数据，记录失败，触发重试或 fallback。长期还要引入 schema versioning。
> **Rule of thumb**: Every external boundary is a failure surface. Validate before trusting.

**与现有知识的关联**: 与 [[harness-engineering]] 中 Contracts & Interfaces 层的"schema drift"问题和 [[agent-reliability-patterns]] 中"约束前置"原则一致。

---

### Q7: Sprint Contract 谈判是怎么工作的？
Sprint Contract 是一个对抗性规划协议，在**任何执行开始前**在 Generator 和 Evaluator 两个独立角色之间运行。

**流程**:
1. **Propose** — Generator 输出结构化计划 + 明确成功标准
2. **Critique** — Evaluator 识别缺失边界情况、模糊断言、不可测试条件，拒绝计划
3. **Revise** — Generator 提交更新计划解决缺口
4. **Sign-off** — 标准可验证且完整后，合同锁定，执行开始

**两条不可协商规则**:
- Evaluator 必须**执行，不能只是读** — 必须运行代码、用浏览器自动化验证接口、模拟交互
- Evaluator 必须在 **clean context** 上运行 — 不能看到 Generator 的推理链

> **Rule of thumb**: Verification must be independent—or it isn't verification.

**与现有知识的关联**: 与 [[evaluator-driven-qa]] 完全兼容，但把"独立评估"的要求表达得更严格（clean context + 执行验证）。

---

### Q8: 资源有限时，应该按什么顺序实现 stack？
**原则**: 不要第一天就建完整 stack。优先韧性，后智能。

**Day 1 — Minimum Viable Harness**:
| 组件 | 解决什么问题 |
|------|-------------|
| `state.json` | 任务进度在 context window 外跟踪 |
| Retry wrapper | 每个 tool call 的 try/catch + 指数退避 |
| Schema validator | 畸形 LLM 输出在传播前被拒绝 |
| Tool output truncation | 每个 payload 的硬 token 预算 |

这四个组件预防了最常见、最昂贵的故障模式：静默截断、未捕获异常、损坏输出、丢失状态。

**然后按这个顺序迭代**:
1. Constraints & Recovery — 让失败安全且幂等
2. Memory & State — 让进度跨 session 持久化
3. Tool Middleware — 防止原始 payload 导致上下文崩溃
4. Contracts & Interfaces — 消除组件间 schema drift
5. Orchestration — 通过 DAG 或状态机强制执行流
6. Cognition & Evaluation — 提升推理质量和输出正确性

> **Rule of thumb**: First make it fail safely. Then make it smarter.

**与现有知识的关联**: 与 [[minimum-viable-agent-harness-checklist]] 结论一致，但把实现顺序表达得更具体（6 步迭代序列）。

---

### Q9: Agent 有数百个工具时，怎么处理动态工具选择？
**问题**: 把所有工具描述注入上下文会耗尽 token budget。

**解法**: 把工具选择当作独立子问题，由专用 sub-agent 在主 agent 运行前处理。

**5 步流程**:
1. **Lightweight tool map** — 给主 agent 注入紧凑的能力摘要（类别 + 关键短语），不是完整工具描述
2. **Extract intent & generate plan** — 主 agent 产出计划，包含显式工具需求（"我需要一个能查询 Postgres 的工具"）
3. **Tool Selector sub-agent** — 专用 sub-agent 在 clean context 上识别真正需要的工具
   - 工具数 > 1000: 两阶段（Coarse filter via RAG/embedding → Precise selection via LLM reasoning）
   - 工具数 ~几百: 直接 LLM reasoning，跳过粗筛
4. **Register selected tools** — 选中工具注入主 agent 上下文，执行继续
5. **Cache tool set within session** — 多步任务中避免每轮重新选择

**两个已知限制**:
- 计划质量: 轻量工具地图让 agent 能表达具体需求而非模糊需求
- 延迟: 每次工具选择至少增加一个 LLM round-trip，但 session caching + 良好范围的粗筛可以把成本控制住

> **Rule of thumb**: Accurate tool selection is a prerequisite for task completion. Use RAG to scale, LLM reasoning to select accurately, and caching to keep multi-step tasks fast.

**与现有知识的关联**: 与 [[multi-agent-delegation]] 中"用 sub-agent 建立 context firewall"和 [[harness-engineering]] 中 Cognition 层的"localized task brief"原则一致。

---

## 5 个常见反模式

如果系统做了以下任何一件事，它还没有 production-ready：

1. **Passing raw tool output directly to the model**
   - 修复: Tool Middleware 层必须做 ranking + dedup + truncation

2. **Letting the LLM control its own execution flow**
   - 修复: 模型只生成计划，专用执行引擎运行 DAG

3. **Using prompt checks instead of validators for correctness**
   - 修复: 能用 Pydantic/jq 的校验绝不用 LLM

4. **Storing critical state only in the context window**
   - 修复: Redis + PostgreSQL 分层外置状态

5. **Encoding retry and recovery logic inside the plan itself**
   - 修复: 重试和恢复是 harness 职责，不是计划内容

---

## 总判断

这 9 个问答的核心收敛点：

| 主题 | 核心原则 |
|------|---------|
| Tool 输出 | 永远预处理，永远不要 raw feed |
| 验证 | 能用代码就不用 LLM |
| 执行控制 | 模型提议，harness 处置 |
| 计划质量 | 可独立 debug 的粒度 + 关注点分离 |
| 状态 | 文件用于开发，Redis/PostgreSQL 用于生产 |
| 边界 | 每个外部接口都是故障面 |
| 评估 | 独立执行 + clean context |
| 优先级 | 先让失败安全，再让系统聪明 |
| 工具选择 | RAG 粗筛 + LLM 细选 + session 缓存 |

**一句话**: Harness Engineering 不是让模型更聪明，而是让环境更 rigid。

## 关联页面
- [[harness-engineering]] — 总概念页，包含 7 层 stack 和 4 设计原则
- [[agent-reliability-patterns]] — 4 个生产陷阱及修复
- [[coding-agent-workflow-patterns]] — 完整 agent run 示例
- [[minimum-viable-agent-harness-checklist]] — Day 1 起步清单
- [[evaluator-driven-qa]] — Generator/Evaluator 分离模式
- [[multi-agent-delegation]] — Sub-agent 分工模式
- [[agent-memory-patterns]] — 状态分层存储
- [[lychee-technology]] — 来源实体

## 来源
- [[ltbase-harness-engineering-faq-2026-04-24|ltbase-harness-engineering-faq]]
- [[ltbase-harness-engineering-2026-04-24|ltbase-harness-engineering]]
