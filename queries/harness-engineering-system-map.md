---
title: Harness Engineering System Map
created: 2026-04-15
updated: 2026-04-15
type: query
tags: [query-note, harness-engineering, context-engineering, reliability, workflow, best-practice]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md, raw/articles/latent-space-extreme-harness-engineering-2026-04-15.md, raw/articles/openai-symphony-spec-2026-04-15.md]
---

# Harness Engineering System Map

## 问题
如果不按“零散文章 + 单点概念”来学，而是要把当前知识库里的 harness engineering 组件串成一张可学习、可导航、可持续扩展的思维导图，最稳的结构应该长什么样？

## 短答案
可以把 [[harness-engineering]] 理解成一套八层系统，而不是单一技巧：

1. 边界层：先分清 [[framework-vs-runtime-vs-harness]] 与 [[harness-vs-context-vs-agentic-engineering]]
2. 事实底座层：让 [[repo-as-system-of-record]] 与 [[agent-readable-repositories]] 成为稳定上下文母体
3. 上下文与记忆层：用 [[context-engineering]]、[[progressive-disclosure]]、[[agent-memory-patterns]] 管 token、状态和 continuity
4. 执行与控制层：用 [[agent-sandboxing]]、[[agent-approval-patterns]]、[[pluggable-agent-backends]] 管边界和执行面
5. 工作流与纠偏层：用 [[coding-agent-workflow-patterns]]、[[agent-feedback-loops]]、[[evaluator-driven-qa]]、[[multi-agent-delegation]] 建闭环
6. 稳定性与评测层：用 [[agent-reliability-patterns]]、[[coding-agent-evals]]、[[how-to-read-agent-harness-benchmarks]] 判断系统是否真的有效
7. 平台与组织层：用 [[cloud-agent-operations]]、[[coding-agent-org-design-patterns]]、[[coding-agent-governance-checklist]]、[[coding-agent-maturity-model]] 理解如何从个人工具长成团队系统
8. 前沿演化层：用 [[natural-language-agent-harnesses]]、[[intelligent-harness-runtime]]、[[extreme-harness-engineering]]、[[entangled-software]] 看这套系统接下来会往哪里长

一句更直白的人话：
Harness engineering 不是“给模型加几个工具”，而是把 context、state、verification、control、workflow、runtime、governance 和 org design 串成一个能长期工作的系统。

## 一张可学习的思维导图

```text
Harness Engineering
├─ 1. 概念边界
│  ├─ [[framework-vs-runtime-vs-harness]]
│  ├─ [[harness-vs-context-vs-agentic-engineering]]
│  ├─ [[harness-engineering]]
│  └─ [[agentic-engineering]]
│
├─ 2. 事实底座 / 工作环境
│  ├─ [[repo-as-system-of-record]]
│  ├─ [[agent-readable-repositories]]
│  ├─ [[doc-gardening-agents]]
│  └─ [[pluggable-agent-backends]]
│
├─ 3. 上下文与记忆
│  ├─ [[context-engineering]]
│  ├─ [[progressive-disclosure]]
│  ├─ [[context-constitution]]
│  ├─ [[agent-memory-patterns]]
│  └─ [[long-running-agent-tasks]]
│
├─ 4. 执行边界与控制面
│  ├─ [[agent-sandboxing]]
│  ├─ [[agent-approval-patterns]]
│  ├─ [[agent-observability]]
│  └─ [[approval-vs-sandbox-vs-observability]]
│
├─ 5. 工作流与纠偏闭环
│  ├─ [[coding-agent-workflow-patterns]]
│  ├─ [[agent-feedback-loops]]
│  ├─ [[evaluator-driven-qa]]
│  ├─ [[evaluator-driven-qa-vs-human-in-the-loop-review]]
│  ├─ [[multi-agent-delegation]]
│  └─ [[deterministic-backpressure-vs-durable-retries]]
│
├─ 6. 稳定性 / 评测 / 判断框架
│  ├─ [[agent-reliability-patterns]]
│  ├─ [[coding-agent-evals]]
│  ├─ [[coding-agent-reliability-stack]]
│  ├─ [[minimum-viable-agent-harness-checklist]]
│  └─ [[how-to-read-agent-harness-benchmarks]]
│
├─ 7. 平台化与组织化
│  ├─ [[cloud-agent-operations]]
│  ├─ [[from-local-coding-agent-to-team-agent-platform]]
│  ├─ [[coding-agent-org-design-patterns]]
│  ├─ [[coding-agent-governance-checklist]]
│  ├─ [[coding-agent-maturity-model]]
│  ├─ [[managed-harness-vs-open-harness]]
│  └─ [[three-platform-archetypes-for-coding-agents]]
│
└─ 8. 前沿研究与未来形态
   ├─ [[natural-language-agent-harnesses]]
   ├─ [[intelligent-harness-runtime]]
   ├─ [[what-nlah-rq2-rq3-actually-show]]
   ├─ [[extreme-harness-engineering]]
   ├─ [[symphony]]
   └─ [[entangled-software]]
```

## 八层结构怎么互相咬合

### 1. 概念边界层：先别把词用乱
第一层先解决“你到底在谈哪一层”的问题。

- [[framework-vs-runtime-vs-harness]] 负责区分构建积木、执行底座、系统支架
- [[harness-vs-context-vs-agentic-engineering]] 负责区分 actor、context、harness 三种视角
- [[harness-engineering]] 是总页，告诉你 harness 关注的是让系统长期稳定交付
- [[agentic-engineering]] 则把视角抬到“组织如何围绕 agent 重写流程”

如果这一层不清楚，后面所有讨论都会混成一锅：把 framework 说成平台、把 runtime 说成可靠性、把 context 当成 harness 全部。

### 2. 事实底座层：agent 先得活在一个可读世界里
agent 不是靠“脑补”完成复杂任务，而是靠稳定事实边界。

- [[repo-as-system-of-record]]：规则、计划、决策、状态最好落在 repo 里
- [[agent-readable-repositories]]：仓库要对 agent 可导航、可检索、可验证
- [[doc-gardening-agents]]：文档不是写完就算，要持续修剪防熵增
- [[pluggable-agent-backends]]：执行面与状态层要能替换，别把系统写死在一种 backend 上

这一层解决的是“agent 到底依据什么活着”。

### 3. 上下文与记忆层：别把窗口当垃圾堆
这一层是当前知识库里最容易被误解、但杠杆非常高的一层。

- [[context-engineering]] 管“给什么、怎么给、何时给”
- [[progressive-disclosure]] 管按需暴露，不把所有规则一次性塞满
- [[context-constitution]] 把 context governance 上升成原则系统
- [[agent-memory-patterns]] 负责把会话记忆、工件记忆、规则记忆分层
- [[long-running-agent-tasks]] 解决跨窗口接棒、续跑、恢复

这层的核心结论已经很清楚：memory 不是外挂插件，而是 harness 内部的 context/state 治理。

### 4. 执行边界与控制面：让 agent 有手，但别乱伸手
有能力不等于有边界。

- [[agent-sandboxing]]：隔离环境、降低故障半径
- [[agent-approval-patterns]]：高风险动作是否需要人点头
- [[agent-observability]]：过程是否可见、可查、可复盘
- [[approval-vs-sandbox-vs-observability]]：三者职责不同，别互相替代

这一层不是为了“限制 agent”，而是为了让 agent 的能力可运营。

### 5. 工作流与纠偏闭环：从一次回答变成可持续推进
真正的 harness 不是一轮 prompt，而是一个能不断看见错误、修正错误、继续推进的 loop。

- [[coding-agent-workflow-patterns]]：任务拆解、实现、验证、PR 闭环
- [[agent-feedback-loops]]：tests、logs、review、signals 进入修正循环
- [[evaluator-driven-qa]]：把生成与验收角色拆开
- [[evaluator-driven-qa-vs-human-in-the-loop-review]]：自动评估与人工审查各守哪道门
- [[multi-agent-delegation]]：用角色分工和 context firewall 降噪
- [[deterministic-backpressure-vs-durable-retries]]：区分“信号质量问题”和“恢复能力问题”

这一层决定 agent 是不是会“假装完成”。

### 6. 稳定性与评测层：系统强不强，不能靠感觉
到了这层，问题变成：你的 harness 到底是真的有效，还是只是 demo 里看起来顺？

- [[agent-reliability-patterns]]：把约束、验证、隔离、回滚、证据、接棒串成模式库
- [[coding-agent-evals]]：把 agent 系统拉进真实任务和真实失败信号里测
- [[coding-agent-reliability-stack]]：把能力压成六层结构
- [[minimum-viable-agent-harness-checklist]]：给 0→1 落地一个最低配清单
- [[how-to-read-agent-harness-benchmarks]]：教你看 benchmark 时别被单点高分骗

这一层的核心价值是：从“文章说得很对”切到“结构上到底哪里在生效”。

### 7. 平台化与组织化：从个人外挂变成团队系统
当 harness 开始进入团队、后台、平台，这层就会变成新的主战场。

- [[cloud-agent-operations]]：把 agent 扔到云端后台长期跑
- [[from-local-coding-agent-to-team-agent-platform]]：看演进顺序
- [[coding-agent-org-design-patterns]]：组织里谁提需求、谁验收、谁担责
- [[coding-agent-governance-checklist]]：上线前最少的安全与责任检查
- [[coding-agent-maturity-model]]：判断系统处在哪个成熟阶段
- [[managed-harness-vs-open-harness]]：控制权、治理、lock-in 怎么权衡
- [[three-platform-archetypes-for-coding-agents]]：平台工作台、托管底座、开放骨架三路分化

这一层开始回答的是“团队怎么用”，而不是“模型能不能用”。

### 8. 前沿演化层：harness 再往上长会变成什么
这里是研究线和平台线汇合的地方。

- [[natural-language-agent-harnesses]]：把 harness pattern 外化成文本工件
- [[intelligent-harness-runtime]]：shared semantics / runtime substrate
- [[what-nlah-rq2-rq3-actually-show]]：哪些模块真的有效，哪些只是 solved-set replacer
- [[extreme-harness-engineering]]：work orchestration 比单轮 coding loop 更重要
- [[symphony]]：把 issue work 直接变成 autonomous implementation runs
- [[entangled-software]]：长期价值可能进一步上移到组织适配、trust、usage flywheel

这层不是“马上照抄”，而是帮你理解未来两三步的演化方向。

## 最推荐的学习顺序
如果你是想系统学，不建议按时间线读，建议按下面顺序：

1. 先读边界
   - [[harness-engineering]]
   - [[framework-vs-runtime-vs-harness]]
   - [[harness-vs-context-vs-agentic-engineering]]

2. 再读事实底座和上下文
   - [[repo-as-system-of-record]]
   - [[agent-readable-repositories]]
   - [[context-engineering]]
   - [[agent-memory-patterns]]
   - [[progressive-disclosure]]

3. 再读控制与纠偏
   - [[agent-sandboxing]]
   - [[agent-approval-patterns]]
   - [[agent-feedback-loops]]
   - [[evaluator-driven-qa]]
   - [[multi-agent-delegation]]

4. 再读稳定性方法图
   - [[agent-reliability-patterns]]
   - [[coding-agent-reliability-stack]]
   - [[minimum-viable-agent-harness-checklist]]
   - [[how-to-read-agent-harness-benchmarks]]

5. 最后再进平台与前沿
   - [[cloud-agent-operations]]
   - [[managed-harness-vs-open-harness]]
   - [[three-platform-archetypes-for-coding-agents]]
   - [[natural-language-agent-harnesses]]
   - [[extreme-harness-engineering]]

## 一个更实用的总判断
如果你以后看任何 agent 产品、论文、文章，都可以拿这 8 层去扫：

- 它在补哪一层？
- 它解决的是 context、state、control、verification、orchestration 里的哪一个缺口？
- 它是让系统更稳，还是只是让 demo 更顺？
- 它是局部技巧，还是能进入平台和组织层的长期结构？

当你能用这张图去拆新材料时，说明你已经不是在“记概念”，而是在建立自己的 harness engineering 判断框架。

## 关联页面
- [[harness-engineering]]
- [[coding-agent-reliability-stack]]
- [[from-local-coding-agent-to-team-agent-platform]]
- [[extreme-harness-engineering]]
- [[natural-language-agent-harnesses]]

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
- [[letta-context-constitution-blog-2026-04-15]]
- [[nlah-arxiv-html-2603-25723-2026-04-15]]
- [[latent-space-extreme-harness-engineering-2026-04-15]]
- [[openai-symphony-spec-2026-04-15]]
