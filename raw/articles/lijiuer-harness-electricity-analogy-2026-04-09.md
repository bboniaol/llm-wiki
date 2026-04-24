---
title: 为什么2026年有人对Harnesses的理解还在1800年
source_url: https://x.com/li9292/status/2042138247208513693
author: 李韭二 (@li9292)
captured: 2026-04-24
method: browser extraction
---

# 为什么2026年有人对Harnesses的理解还在1800年

**作者**: 李韭二 (@li9292)
**发布时间**: 2026-04-09
**互动数据**: 10 replies, 67 reposts, 312 likes, 509 bookmarks, 38.5K views

## 核心论点

大多数人在讨论 agent harness 时，无意识地继承了 1800 年的心智模型：把 LLM 当作一匹需要被控制的马。

Harness 词源来自法语，意为马匹的甲胄和控制装备。19 世纪，harness 就是套在马身上的皮带和金属件，用来引导一匹有力但不受控的动物。

但在作者看来，**LLM 不是马。LLM 是电。**

- 当你把 LLM 当马看，你会去造马鞍、造缰绳。
- 当你把 LLM 当电看，你会去造变压器、造输电网、造电器。

两种心智模型导向完全不同的工程决策。

## 一、明确的产业信号

- **2026 年 2 月**，OpenAI 发布 Harness Engineering 技术博文——3 名工程师通过 Codex 用 5 个月生产了约 100 万行代码，零行由人类手写。重点不是模型多强，而是模型周围那套系统。
- **同月**，Martin Fowler 发表了 harness engineering 文章——软件工程领域最具影响力的作者入场。
- **2026 年 3 月**，arxiv 上出现专门将 harness 形式化为学术概念的论文。

> harness 不是附属品。harness 才是产品。

## 二、Agent Framework VS Agent Harness

**Agent Framework（框架）≠ Agent Harness（驾驭系统）**

| 维度 | Agent Framework | Agent Harness |
|------|----------------|---------------|
| 本质 | 设计时工具 | 完整运行时系统 |
| 包含 | 选模型、prompt 模板、tool schema | 编排循环、工具执行、上下文管理、状态持久化、错误处理、验证循环、安全执行、生命周期管理 |
| 例子 | LangChain, CrewAI | Claude Code, Codex, Manus |
| 类比 | 蓝图 | 能自己跑的车 |

LangChain 的 Vivek Trivedy 的表述最精确：
> "If you're not the model, you're the harness."

Harrison Chase 提出了三层分类：
> Framework（配置）→ Runtime（运行时）→ Harness（驾驭）

## 三、Agent Harness ≠ Harness Engineering

- **Agent Harness** 是产物——一个生产级的 harness 包含 11 个组件。
- **Harness Engineering** 是学科。

围绕 LLM 模型的工程形成三个同心圆：
1. **Prompt Engineering**（提示词工程）——最内层：设计模型收到的指令
2. **Context Engineering**（上下文工程）——中间层：管理模型看到什么、什么时候看到
3. **Harness Engineering**（驾驭工程）——最外层：包含前两层，加上工具编排、状态持久化、错误恢复、验证循环、安全执行和生命周期管理

> 这是电器和电气工程的区别——一个是产物，一个是制造产物的学科。

## 四、3 个流行比喻及其问题

### 1. Scaffold（脚手架）
建筑脚手架是临时基础设施，一旦建筑盖好就拆掉。这个比喻暗示 harness 是过渡性的，随着模型增强终将消失。

**反例**: Anthropic 确实定期从 Claude Code 的 harness 中删除某些步骤，因为更新的模型内化了这些能力。Manus 四次重建了整个 agent framework，每次都在移除复杂度。但移除的是复杂度，不是 harness 本身。

> 作者判断: harness 会变薄，但永远不会被拆掉。

### 2. Wrapper（封装层）
Anthropic 的早期文档将 harness 定义为 "the complete software infrastructure wrapping the LLM"。Wrapping——封装——暗示薄薄一层，重要性远不如里面被包裹的东西（套壳）。

**反例**: Vercel 从他们的数据 agent d0 中移除了 80% 的工具定义，成功率从 80% 提升到 100%，速度快了 3.5 倍。如果 harness 只是一层包装，那移除 80% 的工具应该让性能变差，而不是变好。

> 封装层这个比喻低估了 harness 的工程权重。

### 3. Engine vs Car（引擎与汽车）
Evangelos Pappas 提出：模型是引擎，harness 是车。行业花了太多时间争论引擎规格，却没人在造一辆能上路的车。

**局限**: 这个类比承认 harness 不是附属品，但它的局限在于品类的单一性。LLM 驱动的 agent 跨越的是完全不同的品类：编程助手、客服对话、医疗诊断。这更像是电力接上不同的电器，而不是引擎装进不同的车。

## 五、值得认真对待的比喻：操作系统

在所有现有比喻中，最精确的来自 Beren Millidge 2023 年的文章：
> 一个裸 LLM 就是一块没有操作系统的 CPU。harness 就是让它可用的 OS。

这个类比在微观层面是准确的。如果你在设计一个 harness 的内部架构，OS 比喻是最直接可操作的参考模型。

但 OS 解释的是一台计算机内部如何运作，而不是计算机产业如何运作。OS 比喻和电力比喻不是替代关系，而是互补：一个解释微观架构，一个解释宏观产业。

## 六、从 1800 年到 1900 年：电力革命

十年前，吴恩达 2016 年发推："AI is the new electricity!"
2017 年他在 Stanford GSB 展开：「就像电力在 100 年前改变了几乎所有行业，今天我很难想到一个行业不会在未来几年被 AI 改变。」

### 为什么是电力，不是蒸汽机？
蒸汽机是能源转换的临时产物，最终被电力取代。某种意义上，蒸汽机才是真正的 scaffold。

而电力有三个关键特征：
1. **通用性** — 驱动完全不同类型的设备
2. **远程传输** — 通过电网从生产地到使用地
3. **标准化接口** — 不管怎么发电，最终转化为标准电压输出

LLM 具备类似的特征。当然，类比不是等式。LLM 的输出具有非确定性，而电力是完全可预测的。这些差异意味着 harness engineering 面临的挑战比电气工程更复杂。但在产业结构的层面，电力的分层逻辑仍然是目前最有解释力的类比。

### 完整的产业分层对应

最关键的一层：**电器**。灯泡、冰箱、计算机、核磁共振仪，每一种都是一套完整的工程系统，将标准化的电力转化为特定场景的价值。

而**电气工程**——制造这些电器的学科——对应的正是 **Harness Engineering**。

## 结语：插上电就行了吗？

如果电力类比成立，历史还给了我们一个警告。

Dr. Philippa Hardman 指出，工厂只有在围绕电力重新设计之后才变得更高效，而简单地把蒸汽引擎换成电动马达是不够的。

今天的企业正在犯同样的错误：
- McKinsey 2025 年报告显示，不到 10% 的企业 AI 应用能走过试点阶段。
- MIT 的研究发现，95% 的生成式 AI 项目没有产生可量化的财务影响。

企业以为「插上电就行」。但就像 100 年前的工厂一样，你必须围绕新的能源形态重新设计整套系统。这正是 harness engineering 要做的事。

---

## 引用来源
1. OpenAI, "Harness engineering: leveraging Codex in an agent-first world" (2026.2.11)
2. Martin Fowler, "Harness engineering for coding agent users"
3. CNBC, "Meta acquires intelligent agent firm Manus" (2025.12.30)
4. "Natural-Language Agent Harnesses," arxiv 2603.25723 (2026.3.26)
5. Nghi D. Q. Bui, "Building Effective AI Coding Agents for the Terminal," arxiv 2603.05344
6. LangChain, "Agent Frameworks, Runtimes, and Harnesses"
7. Daily Dose of DS (Avi), "The Anatomy of an Agent Harness" (2026.4.7)
8. Anthropic, "Building Effective Agents" (2024.12)
9. Manus, "Context Engineering for AI Agents: Lessons from Building Manus"
10. Vercel, "We removed 80% of our agent's tools"
11. Evangelos Pappas, "The Agent Harness Is the Architecture"
12. Beren Millidge, "Scaffolded LLMs as natural language computers" (2023.4.11)
13. Andrew Ng, Twitter (2016.5.26)
14. Stanford GSB, "Andrew Ng: Why AI Is the New Electricity" (2017)
15. Dr. Philippa Hardman, "AI: the New Electricity?"
16. McKinsey QuantumBlack, "Seizing the agentic AI advantage" (2025.6)
17. MIT NANDA, "The Gen AI Divide: State of AI in Business 2025"
