---
title: Harness Engineering 7-Day Study Plan
created: 2026-04-15
updated: 2026-04-15
type: query
tags: [query-note, harness-engineering, context-engineering, workflow, best-practice, agentic-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md, raw/articles/latent-space-extreme-harness-engineering-2026-04-15.md, raw/articles/openai-symphony-spec-2026-04-15.md]
---

# Harness Engineering 7-Day Study Plan

## 问题
如果工作日每天大约只能投入 2 小时，周末可以多学一些，怎么在 7 天内把这套 harness engineering 知识库学出“系统感”，而不是只记住一堆术语？

## 短答案
最稳的节奏不是平均分配，而是：

- 工作日：打地基，解决概念边界、核心组件、关键判断框架
- 周末：拉通系统，集中啃平台化、前沿研究和整体地图

所以这套 7 天路线我按“5 个轻负载工作日 + 2 个重负载周末日”来设计。

## 使用方法
每天都只做 3 件事：
1. 读指定页面
2. 写 5-10 句话自己的总结
3. 回答当天的检查问题

不要贪多。你不是在冲阅读量，而是在建立一套以后看产品、文章、论文都能直接套用的判断框架。

---

## Day 1（工作日 / 2h）
## 目标
先把词义边界打清楚，避免后面越学越乱。

## 阅读顺序
1. [[harness-engineering]]
2. [[framework-vs-runtime-vs-harness]]
3. [[harness-vs-context-vs-agentic-engineering]]

## 今天要学会的 3 个判断
- harness 不是 prompt 技巧，而是系统支架
- runtime 强，不等于 harness 就完整
- context engineering / agentic engineering 和 harness engineering 不是一回事

## 输出要求
写一段你自己的定义：
“在我的理解里，harness engineering 主要负责 ______，它和 framework/runtime/context/agentic engineering 的区别是 ______。”

## 检查问题
如果一个产品只强调：
- 模型很强
- 工具很多
- 有 runtime

但不讲 verification、approval、state、workflow，你会不会认为它 harness 很成熟？为什么？

---

## Day 2（工作日 / 2h）
## 目标
把 agent 的“生存环境”与“事实边界”看懂。

## 阅读顺序
1. [[repo-as-system-of-record]]
2. [[agent-readable-repositories]]
3. [[context-engineering]]
4. [[progressive-disclosure]]

## 今天要学会的 3 个判断
- repo 不只是代码仓库，还是 agent 的事实母体
- context engineering 的关键不是更多，而是更高信号
- progressive disclosure 是控制 instruction budget 的实战原则

## 输出要求
写一张小表：
- 什么信息应该常驻上下文
- 什么信息应该按需检索
- 什么信息应该版本化沉淀到 repo

## 检查问题
为什么很多团队的 `AGENTS.md` / `CLAUDE.md` 越写越长，反而让 agent 更不稳？

---

## Day 3（工作日 / 2h）
## 目标
把 memory、continuity、长任务接棒这条线真正串起来。

## 阅读顺序
1. [[agent-memory-patterns]]
2. [[long-running-agent-tasks]]
3. [[context-constitution]]

## 今天要学会的 3 个判断
- memory 不只是聊天历史保存
- 长任务问题本质上是 context/state continuity 问题
- Letta 这条线值钱的地方是把 memory 提升成 harness 内部治理问题

## 输出要求
写出 3 种 memory：
- 会话记忆
- 工件记忆
- 规则记忆
并各写一句：它们应该放在哪里、什么时候回收。

## 检查问题
为什么“加一个 memory plugin”通常不等于你已经解决了 agent memory？

---

## Day 4（工作日 / 2h）
## 目标
把控制面看懂：agent 为什么需要边界，而不是只要能力。

## 阅读顺序
1. [[agent-sandboxing]]
2. [[agent-approval-patterns]]
3. [[agent-observability]]
4. [[approval-vs-sandbox-vs-observability]]

## 今天要学会的 3 个判断
- sandboxing 解决的是故障半径
- approval 解决的是责任边界和高风险动作守门
- observability 解决的是可查、可复盘、可追责

## 输出要求
写一个你自己的最小控制面模板：
- 哪类操作自动放行
- 哪类操作必须审批
- 哪类证据必须保留

## 检查问题
为什么“我已经做了审批”不能替代 sandbox 和 observability？

---

## Day 5（工作日 / 2h）
## 目标
把闭环、验证、可靠性先搭出骨架。

## 阅读顺序
1. [[coding-agent-workflow-patterns]]
2. [[agent-feedback-loops]]
3. [[evaluator-driven-qa]]
4. [[agent-reliability-patterns]]

## 今天要学会的 3 个判断
- 真正的 workflow 不只是“生成代码”，而是实现 + 验证 + 修正
- evaluator 的价值在于打破 agent 自评幻觉
- reliability 不是多上几个测试，而是整套纠偏与恢复机制

## 输出要求
用 6-8 句话写一个最小 workflow：
任务输入 → 执行 → 验证 → 失败信号 → 修正 → 交付。

## 检查问题
什么情况下 evaluator 是高价值模块，什么情况下它会变成额外成本？

---

## Day 6（周末 / 4-5h）
## 目标
集中拉通“系统如何从局部可用变成团队级平台”。

## 阅读顺序
1. [[coding-agent-reliability-stack]]
2. [[minimum-viable-agent-harness-checklist]]
3. [[from-local-coding-agent-to-team-agent-platform]]
4. [[coding-agent-maturity-model]]
5. [[managed-harness-vs-open-harness]]
6. [[three-platform-archetypes-for-coding-agents]]

## 今天要学会的 4 个判断
- reliability stack 是能力分层图
- maturity model 是阶段判断图
- local → team platform 是演进路线图
- managed vs open vs platform archetype 是路线选择图

## 输出要求
做一张你自己的三列表：
- 我现在最认同的最小 harness 能力
- 哪些能力属于团队级平台阶段才需要
- 我最警惕的 lock-in / 治理 / 复杂度问题

## 检查问题
如果你现在要做一个 Spring Boot 微服务 agent 平台，最不该过早投入的是哪一层？为什么？

---

## Day 7（周末 / 4-6h）
## 目标
进入前沿，但不是追热点，而是把“未来演化方向”放回你的总框架里。

## 阅读顺序
1. [[natural-language-agent-harnesses]]
2. [[intelligent-harness-runtime]]
3. [[what-nlah-rq2-rq3-actually-show]]
4. [[extreme-harness-engineering]]
5. [[symphony]]
6. [[entangled-software]]
7. [[harness-engineering-system-map]]

## 今天要学会的 4 个判断
- NLAH 的核心不是 prompt 更长，而是 harness externalization
- IHR 的价值是 shared semantics，不只是一个 runtime 名字
- Extreme Harness Engineering 说明 work orchestration 已经比单轮 coding loop 更重要
- 长期价值可能会从 harness 本身继续上移到组织适配、trust、usage flywheel

## 输出要求
写一页你自己的总结，题目建议直接用：
“我现在如何理解 harness engineering，以及它未来会往哪长”

至少回答这 4 个问题：
1. harness engineering 的核心对象到底是什么？
2. memory / context / workflow / governance 分别在系统里守什么职责？
3. 什么是今天最值得学的结构，什么又太前沿不该直接照抄？
4. 如果我要落地，会从哪一层开始？

## 检查问题
你会不会直接照着 Symphony / dark factory 路线做？如果不会，你会抽走哪些结构，只保留哪些原则？

---

## 一周后的达标标准
如果这 7 天学完，你能稳定回答下面这些问题，基本就算学进去了：

1. harness 和 framework/runtime/context/agentic engineering 的边界是什么？
2. repo、context、memory、workflow、approval、sandbox、observability、eval 各守什么职责？
3. 为什么很多 agent 系统失败，本质不是模型弱，而是 harness 空心？
4. managed harness、open harness、platform workbench 三条路线分别适合什么阶段？
5. 哪些前沿方向值得跟，哪些只是当前组织条件下的极端样本？

## 最后的建议
这 7 天路线不是让你“背完所有页”，而是让你建立一个稳定阅读姿势：

- 新材料先判断它落在哪一层
- 再判断它补的是哪个缺口
- 最后判断它是局部技巧、系统结构，还是平台/组织级变化

一旦这个阅读姿势形成，后面再看新论文、新产品、新 benchmark，你就不容易被 marketing 文案牵着走。

## 关联页面
- [[harness-engineering-system-map]]
- [[coding-agent-reliability-stack]]
- [[coding-agent-maturity-model]]
- [[from-local-coding-agent-to-team-agent-platform]]
- [[extreme-harness-engineering]]

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
