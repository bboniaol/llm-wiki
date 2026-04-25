# Scaffolded LLMs as natural language computers

## 基本信息
- **作者**: Beren Millidge
- **发布时间**: 2023-04-11
- **来源**: https://www.beren.io/2023-04-11-Scaffolded-LLMs-natural-language-computers/
- **标签**: #agent #harness #von-neumann #scaffolded-llm #natural-language-computer #NLOP

---

## 一句话总结

将围绕 LLM 的“脚手架”系统（scaffolded LLMs）视为一种**自然语言通用计算机**，其核心是：LLM=CPU、上下文=RAM、向量库=磁盘、插件=驱动，而单个 LLM 调用则是一个“自然语言操作（NLOP）”。

---

## 核心论点

1. **我们重新发明了冯·诺依曼架构**
   - Generative Agent 的架构（LLM + 提示模板 + 记忆读写）与冯·诺依曼架构惊人相似。
   - 这不是巧合——冯·诺依曼架构是设计计算机的“自然抽象”。

2. **自然语言计算机的组成映射**

| 数字计算机 | 自然语言计算机 (Scaffolded LLM) |
|-----------|------------------------------|
| CPU       | LLM（NLPU：自然语言处理单元） |
| RAM       | Prompt / 上下文窗口         |
| 磁盘/内存 | 向量数据库 / 长期记忆         |
| 内存控制器| 向量检索启发式 / 记忆控制器   |
| 驱动/外设 | Plugins / API 工具            |
| 程序/指令 | 提示模板 + ReAct / 反思等协议 |

3. **性能度量：NLOP**
   - **NLOP** (Natural Language OPeration)：约 100 token 的生成视为一次 NLOP。
   - GPT-4 ≈ 1 NLOP/s；GPT-3.5-turbo ≈ 10 NLOPs/s。
   - 上下文长度 = RAM：GPT-4 8K ≈ Commodore 64 时代（1980s 早期）。

4. **执行模型 = 数据流架构**
   - 不同于 CPU 的串行执行，LLM 调用天然可并行。
   - 自然执行模型是**展开的 DAG**（有向无环图），受程序内在串行性约束，但不受硬件限制。

5. **同态性（Homoiconicity）**
   - 数字计算机：指令和数据都是 bits，无本质区别。
   - 自然语言计算机：prompt 中指令与语义内容无原则区分；但已开始形成惯例（如 system prompt = 保护内存区）。

---

## 关键洞察

### 编程语言层面
- 当前处于**汇编语言阶段**：CoT、Selection-Inference、Reflection、Self-correction 是 `mov`、`leq`、`goto`。
- LangChain 等是**最原始的编译器**，还没达到 C 语言的抽象层级。
- 抽象有开销，当前 NLOP 太慢，无法有效使用高级抽象；但未来会。

### 理论空白
- 数字计算机有图灵、哥德尔、λ 演算等先验理论。
- **自然语言计算机几乎没有等价的形式理论**：
  - NLOP 的边界未定义
  - 没有 NAND 门等价的最小自然语言电路
  - 没有真值表来规范底层行为

### 内存层级
- 当前只有两级：上下文（Cache/RAM）和向量库（磁盘）。
- 未来会出现更多层级：LLM 内部密集/稀疏注意力、LLM 子调用做相关性排序等。

### 基础模型 = 认知硬件
- 基础模型更像**硬件**而非软件：
  - 黑盒、难以调试、无版本控制
  - 昂贵、迭代慢（训练失败 = 数月等待）
  - 高通用性、可移植性（理论上）
- 经济地位类比：OpenAI ≈ Intel（芯片制造商），高固定成本 + 商品化销售。

### 与数字计算机的根本差异
| 特性 | 数字 CPU | NLPU (LLM) |
|-----|---------|------------|
| 确定性 | 高 | 低（甚至 zero-temp 也非确定） |
| 可靠性 | 极高 | 低（质量波动大） |
| 规格明确 | 是 | 否（underspecified，如摘要的一对多映射） |
| 指令集 | 固定 | 开放/不断增长 |
| 速度 | 10^9 FLOPs/s | ~1 NLOP/s |
| 灵活性 | 低 | 极高（任意自然语言任务） |

- **CISC vs RISC 辩论的再现**：复杂提示（CISC）vs 大量简单提示链（RISC）。

---

## 原文摘录

> "What we have essentially done here is reinvented the von-Neumann architecture and, what is more, we have reinvented the general purpose computer."

> "Like a digital computer, it is fully general, but what it operates on is not bits, but text. We have a natural language computer which operates on units of natural language text to produce other, more processed, natural language texts."

> "The natural execution model of our NL computer is instead an expanding DAG of parallel NLOPs, constrained by the inherent seriality of the program they are running, but not by the 'hardware'. In effect, we have reinvented the dataflow architecture."

> "We will likely need similar 'semantic' error correcting codes for LLM outputs to be able to stitch together extended sequences of NLOPs in a highly coherent and consistent way."

---

## 关联概念

- [[von-neumann-architecture]] — 冯·诺依曼架构
- [[generative-agent]] — Park et al. 的 Generative Agent 论文
- [[react-agent]] — ReAct 推理-行动循环
- [[chain-of-thought]] — 思维链
- [[llm-os]] — LLM Agent Operating System (AIOS)
- [[agent-harness]] — Agent Harness 基础设施
- [[dataflow-architecture]] — 数据流架构
- [[homoiconicity]] — 同态性

---

## 评价与影响

- **开创性**：最早系统地将 scaffolded LLM 与计算机架构做完整类比的文章之一。
- **预见性**：提出的 NLOP、NLPU、自然语言编程语言等概念在 2024-2025 年得到广泛呼应。
- **局限性**：写于 GPT-4 早期，对速度/成本的悲观预测部分已被改善（如推理优化、MoE、推理时间扩展）。
- **与 Harness Engineering 的关系**：Scaffold = Harness 的“硬件抽象层”视角——harness 是围绕 LLM 这个“CPU”构建的完整计算机系统。
