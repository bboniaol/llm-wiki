---
title: Meta-Harness
created: 2026-04-25
updated: 2026-04-25
type: entity
tags: [product, framework, benchmark, evaluation, harness-engineering, agentic-engineering, open-source]
sources: [raw/papers/meta-harness-paper-2026-03-30.md, raw/articles/stanford-meta-harness-tbench2-2026-04-25.md, raw/papers/terminal-bench-2.0-paper-2026-01-17.md]
---

# Meta-Harness

## 简介
Stanford IRIS Lab 提出的 **outer-loop harness 优化系统**，核心命题：harness（决定模型看到什么、存储什么、检索什么的代码）可以像超参数一样被自动搜索和优化，而不是永远依赖人工设计。这是首个在三个不同领域（文本分类、数学推理、agentic coding）都验证有效的 harness 自动优化框架。

## 核心团队
- Yoonho Lee, Roshen Nair, Qizheng Zhang, Kangwook Lee, Omar Khattab, Chelsea Finn
- 机构：Stanford IRIS Lab
- 论文：arXiv:2603.28052（2026-03-30 提交）

## 核心创新

### 为什么现有文本优化器不适合 harness 优化
现有方法（TTT-Discover、OpenEvolve）的问题：
- **无记忆**：不保留历史尝试记录
- **仅标量反馈**：只看分数，不看执行轨迹
- **模板限制**：把反馈压缩成短摘要

Meta-Harness 的解法：给 proposer **完整的文件系统访问权限**：
- 所有候选 harness 的源代码
- 执行轨迹（每次评估最多 1000 万 token 诊断信息）
- 分数和性能指标
- proposer 用 `grep` 和 `cat` 自由读取

### 外层循环架构
1. **初始化种群**：从强基线开始（如 Terminus-KIRA、ACE）
2. **Proposer 提议**：agent 基于文件系统历史提出新 harness 变体
3. **评估**：在搜索集上运行候选 harness
4. **选择**：基于 Pareto 前沿（准确率 vs 上下文成本）
5. **迭代**：proposer 从所有历史尝试中学习

### 关键设计：最小必要结构
Meta-Harness 故意对外层循环施加最小结构：
- proposer 获得原始文件系统访问，而非预处理摘要
- 保留完整经验历史
- 允许 proposer 检查任何需要的信息
- 这就是它优于结构繁重的 OpenEvolve/TTT-Discover 的原因

## 三大实验领域结果

### 1. 在线文本分类
- **结果**：比 ACE（SOTA 上下文管理）高 **7.7 分**，上下文 token 少 **4 倍**
- **速度**：仅 **4 次评估** 就达到竞争对手 60 次评估的最终性能
- **消融实验**：
  - 完整接口（分数+轨迹）：50.0 中位数准确率
  - 仅分数：34.6
  - 分数+摘要：34.9
  - **结论**：完整执行轨迹访问是最重要的组件

### 2. 检索增强数学推理
- **200 道 IMO 级别题目**（IMO-AnswerBench、IMO-ProofBench、ArXivMath）
- **5 个 held-out 模型**：GPT-OSS-20B、GPT-5.4-nano、GPT-5.4-mini、Gemini-3.1-Flash-Lite、Gemini-3-Flash
- **结果**：5 个模型平均提升 **4.7 分**
- **方法**：在 BM25 上的代码空间操作，无需额外 dense encoder

### 3. Agentic Coding（TerminalBench-2）
- **Claude Opus 4.6**：**76.4%** 通过率
  - 超越 Terminus-KIRA（74.7%）
  - 在所有 Opus 4.6 agent 中排名 **#2**（ForgeCode 81.8% 但无法从公开代码复现）
- **Claude Haiku 4.5**：**37.6%** 通过率
  - 在所有 Haiku 4.5 agent 中排名 **#1**
  - 比第二名（Goose，35.5%）高 2.1 分

## 发现的 TerminalBench-2 Harness：环境引导（Environment Bootstrapping）

### 核心 trick
agent 循环开始前，harness 运行复合 shell 命令收集 sandbox 环境快照并注入初始 prompt。

**快照包含：**
- 工作目录
- /app 目录列表（大目录截断到 20 项）
- 可用编程语言及版本（Python、GCC、G++、Node、Java、Rust、Go）
- 已安装包管理器（pip、apt-get）
- 可用内存

**效果**：消除 agent 通常花在发现可用工具和文件的 2-4 轮探索，让模型立即开始有效工作。

**实现细节：**
- 引导命令有 15 秒超时保护
- 静默失败（不破坏异常环境中的 agent）
- 在 Terminus-KIRA 基础上增加约 80 行代码
- 继承 Terminus-KIRA 的原生 tool calling、30KB 输出上限、多视角完成检查清单

### 搜索过程叙事
论文记录了有趣的搜索日志叙事弧：
1. 早期候选因过度激进的环境假设而失败
2. proposer 形成对失败的明确诊断
3. 转向更安全的设计模式（带超时+静默失败的环境引导）
4. 最终 harness 既鲁棒又可泛化

## 与现有知识的关联
- [[harness-engineering]] — Meta-Harness 直接验证 "harness 可以自动优化" 的命题
- [[coding-agent-evals]] — 提供 harness 层可优化性的首个系统级实证
- [[wolfbench]] / [[terminal-bench]] — TerminalBench-2 是核心评测平台
- [[terminus-kira]] — 基线 harness，Meta-Harness 在其上增加环境引导
- [[akshay-pachaar]] — 文中引用的 "LLM 自优化 harness 76.4%" 的具体所指
- [[natural-language-agent-harnesses]] — NLAH 把 harness 外化成自然语言对象；Meta-Harness 把 harness 外化成可搜索的代码对象
- [[agent-memory-patterns]] — 环境引导本质上是一种"预加载记忆"策略

## 通用化验证
### OOD 文本分类
- 在 **9 个未见数据集** 上评估
- Meta-Harness 平均准确率 **73.1%**
- 超越 ACE（70.2%）和所有 few-shot 基线
- 在 6/9 数据集上表现最佳
- 说明发现的 harness 捕获的是通用有效策略，而非过拟合

## 局限与边界
- ForgeCode（81.8%）仍高于 Meta-Harness，但无法从公开代码复现
- TerminalBench-2 的 harness 是 benchmark 特化的（虽然能力通用）
- 搜索过程需要计算资源（每次评估运行完整 benchmark）
- "More details coming soon" — 论文已发表但 artifact 可能还有更新

## 来源
- [[meta-harness-paper-2026-03-30]]
- [[stanford-meta-harness-tbench2-2026-04-25]]
- [[terminal-bench-2.0-paper-2026-01-17]]
