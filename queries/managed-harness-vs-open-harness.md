---
title: Managed Harness vs Open Harness
created: 2026-04-14
updated: 2026-04-15
type: query
tags: [query-note, harness-engineering, infrastructure, workflow, comparison, best-practice]
sources: [raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/claude-x-post-2041927687460024721-2026-04-14.md, raw/articles/pawel-huryn-x-post-2042008828334764162-2026-04-14.md, raw/articles/alexz-x-post-2041951380836147479-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md, raw/articles/guru-x-post-2042450832126591251-2026-04-14.md, raw/articles/gabe-pereyra-x-post-2041568552256197074-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/harrison-chase-x-post-2042978500567609738-2026-04-15.md]
---

# Managed Harness vs Open Harness

## 问题
当 agent 系统开始从本地工具升级成长期运行、团队协作、可治理的平台时，团队应该优先选择 managed harness，还是 open harness？

## 短答案
没有绝对更优，只有更匹配当前阶段的路线。

- managed harness 更像“先买运行面”
- open harness 更像“先掌握运行面”

如果你现在最缺的是：
- 安全 runtime
- durable execution
- 组织级治理
- 快速上线

那 managed harness 更合适。

如果你现在最缺的是：
- 可控性
- 可移植性
- provider independence
- 深度定制能力

那 open harness 更合适。

真正常见的现实路径不是二选一，而是：
1. 先用 managed harness 跑通平台面
2. 再在高价值链路上补 open harness 能力
或者反过来：
1. 先用 open harness 在本地和团队内部打磨 workflow
2. 再把一部分任务迁到 managed runtime

## 先把两个词说清楚

### 什么是 managed harness
managed harness 指供应商把 agent runtime 的关键基础设施直接托管出去，通常包括：
- 运行环境
- sandbox
- session / state 管理
- lifecycle management
- observability / artifacts / audit surface
- 权限与治理控制

当前库里最明确的代表是 [[claude-managed-agents]]。
它的价值不是“又一个 agent 产品”，而是把原本最难、最脏、最容易踩安全坑的运行面直接产品化。

### 什么是 open harness
open harness 指团队自己掌握 agent system 的主要控制面，通常包括：
- framework / runtime / orchestration 的选择权
- filesystem / memory / permissions / subagents 的组合方式
- model provider 的切换能力
- 部署位置、运行边界、数据面与工具面的定义权

当前库里更接近这一侧的参考对象是 [[deepagents]]，以及更广义上的 [[langchain]] / runtime / workflow infra 组合。

## 两条路线的真正差别

### 1. 买到的是“能力”，还是“自由度”
- managed harness 的优势是，你能更快买到一整套能运行的能力。
- open harness 的优势是，你保留了更多结构自由度。

前者解决的是“先跑起来”。
后者解决的是“以后别被锁死”。

### 2. 优先优化的是 time-to-production，还是 architecture control
- managed harness 优先优化上线速度、治理成型速度、组织采用速度。
- open harness 优先优化控制权、可解释性、长期可演化性。

所以两者不是“封闭 vs 开放”这么简单，而是：
- 你是在买交付速度
- 还是在买结构主权

### 3. 风险长在不同位置
- managed harness 的主要风险：
  - provider lock-in
  - 能力边界受制于供应商产品形态
  - 深度定制和特殊场景支持可能受限
  - 尤其当 memory / compaction / state 也一起托管时，迁移成本会从“换模型”升级成“重建用户记忆”
- open harness 的主要风险：
  - 自己承担 runtime / security / durability / observability 成本
  - 平台建设周期长
  - 容易把“本地工作流问题”过早升级成“平台建设问题”

## 对比表
| 维度 | Managed Harness | Open Harness |
|---|---|---|
| 第一目标 | 快速得到可运行、可治理的 agent 运行面 | 自己掌握 agent 系统的控制面和演化权 |
| 典型价值 | 上线快、安全边界更快成型、组织治理容易落地 | 可移植、可定制、可组合、provider independence、memory sovereignty |
| 主要代价 | 受供应商形态约束，可能 lock-in | 需要自己承担 runtime、sandbox、durability、observability 工程 |
| 最适合的阶段 | 团队已经进入 [[cloud-agent-operations]] / 平台治理阶段 | 团队仍在打磨 [[harness-engineering]] / workflow / memory / subagent 结构 |
| 对组织能力要求 | 更偏产品整合与治理能力 | 更偏系统设计与平台工程能力 |
| 常见代表信号 | [[claude-managed-agents]]、Harvey Spectre 类 durable run 平台 | [[deepagents]]、runtime + harness 自组装路线 |
| 容易踩的坑 | 以为“托管了”就自动等于“适配了你的 workflow” | 以为“开源了”就自动等于“有平台能力了” |

## 一个更实用的判断框架

### 选 managed harness，如果你符合这几条
1. 你已经明确要做云端 / 后台 agent，而不是只做本地 coding helper
2. 你最痛的是安全、隔离、生命周期、审计，不是 prompt 细节
3. 你希望更快进入组织级 adoption
4. 你愿意接受一部分产品边界，换更快的生产可用性

一句人话：
- 如果你现在最缺的是“别让我自己造运行面”，那就偏 managed。

### 选 open harness，如果你符合这几条
1. 你还在快速迭代 workflow，本体还没稳定
2. 你希望 agent 结构跟着业务深度定制
3. 你不想把模型、运行面、工具面全部绑死在一个供应商上
4. 你团队内部有能力长期维护 runtime / orchestration / sandbox / observability

一句人话：
- 如果你现在最缺的是“让我自己定义系统长什么样”，那就偏 open。

## 最常见的误判

### 误判 1：把 managed harness 当作万能捷径
不是。
managed harness 解决的是 runtime 和治理面的一大块问题，但它不会自动替你解决：
- 任务拆解
- 上下文组织
- 验证闭环
- domain workflow 设计

所以它不能替代 [[harness-engineering]]，只是把其中一部分高成本运行面托管掉。

### 误判 2：把 open harness 当作天然先进路线
也不是。
open harness 的确给你更多自由，但自由本身就是工程负担。
如果团队还没跑通 [[from-local-coding-agent-to-team-agent-platform]] 里的前 3 阶段，就直接自建平台，大概率是在放大混乱。

### 误判 3：把选择理解成一次性不可逆
现实里更像分层混搭：
- 核心 workflow 和认知层保持 open
- 高成本运行面采用 managed
- 或者先 managed 快速试错，再把关键链路回迁到 open stack

## 一条我更认可的路线图

### 路线 A：open first, managed later
适合：
- 还在探索 agent workflow
- 需要快速试很多结构
- 更重视 system learning than platform polish

顺序通常是：
1. 先在本地 / 半托管环境里把 workflow、memory、subagents、approval 这些调顺
2. 形成可复用 harness
3. 再把长任务 / durable run / org governance 那部分接到 managed runtime

### 路线 B：managed first, open later
适合：
- 已经明确有平台化目标
- 组织很在意安全、审计、SLA、合规
- 更想先要一条能上线的后台 agent 路径

顺序通常是：
1. 先把托管 runtime 接进生产闭环
2. 快速拿到 durable execution、sandbox、artifacts、audit surface
3. 再针对高价值场景补自定义 harness 或 open runtime

## 新补充的一条判断线：你是否拥有自己的 memory
Harrison Chase 这条新帖子把一个之前容易被弱化的判断条件说得很直白：managed vs open 的差别，不只是 runtime 在谁手里，更是 memory data plane 在谁手里。

如果你的 stateful threads、compaction summary、long-term memory 和记忆读取逻辑都锁在 provider 后面，那么你失去的不只是“可迁移性”，而是用户偏好、任务历史和 agent 习惯本身。对 agent 产品来说，这往往是最值钱的数据资产。

所以更实用的判准可以再补一句：
- 你能不能导出并复用自己的 memory
- 你能不能在不重训使用习惯的前提下切换 harness 或 model
- 你的记忆结构是否对自己可见、可审计、可重放

如果这三条都做不到，所谓 managed convenience 很可能是在拿未来主权换现在速度。

## 结论
managed harness 和 open harness 的真正差别，不是“谁更高级”，而是：
- 一个优先帮你买到运行面
- 一个优先帮你保留定义权

如果今天一定要给一个偏向性建议，我会这样说：
- workflow 还没稳定，优先 open
- 平台面和治理面已成硬需求，优先 managed

更进一步说：
- 在 agent 早期，开放性更值钱
- 在 agent 平台期，托管运行面更值钱

所以最稳的答案不是站队，而是分阶段混搭。

## 关联页面
- [[harness-engineering]]
- [[cloud-agent-operations]]
- [[framework-vs-runtime-vs-harness]]
- [[from-local-coding-agent-to-team-agent-platform]]
- [[claude-managed-agents]]
- [[deepagents]]

## 来源
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[claude-x-post-2041927687460024721-2026-04-14]]
- [[pawel-huryn-x-post-2042008828334764162-2026-04-14]]
- [[alexz-x-post-2041951380836147479-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
- [[guru-x-post-2042450832126591251-2026-04-14]]
- [[gabe-pereyra-x-post-2041568552256197074-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
- [[harrison-chase-x-post-2042978500567609738-2026-04-15]]
