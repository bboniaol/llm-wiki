---
title: Three Platform Archetypes for Coding Agents
created: 2026-04-14
updated: 2026-04-14
type: query
tags: [query-note, workflow, harness-engineering, infrastructure, best-practice, agentic-engineering]
sources: [raw/articles/cursor-product-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/claude-x-post-2041927687460024721-2026-04-14.md, raw/articles/langchain-deepagents-overview-2026-04-14.md, raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md]
---

# Three Platform Archetypes for Coding Agents

## 问题
如果把当前 coding agent 平台路线压成几种典型原型，而不是按单个产品名来记，最有用的分类应该怎么做？

## 短答案
基于当前库里的证据，我更认可把 coding agent 平台分成 3 种 archetype：

1. 平台工作台型
2. 托管底座型
3. 开放骨架型

对应当前库里的代表对象：
- 平台工作台型 → [[cursor]]
- 托管底座型 → [[claude-managed-agents]]
- 开放骨架型 → [[deepagents]]

这 3 类不是“谁替代谁”的关系，而是分别站在不同平台层回答不同问题：
- 谁来承载日常工作面
- 谁来托管运行底座
- 谁来作为自建平台底盘

## 为什么这页值钱
如果只按产品名记忆，你会一直陷在“谁更强”的比较里。
但如果按 archetype 看，问题会更清楚：
- 你到底需要的是工作台，还是底座，还是骨架？
- 你是在选 end-user surface，还是 managed substrate，还是 open foundation？

这比单纯产品对比更稳，也更适合未来补新对象。

## Archetype 1：平台工作台型
一句话：
- 把开发者和跨职能团队真正每天操作的 agent 工作面做完整。

核心特征：
- 本地交互面强
- workflow surface 宽
- 从 IDE 会话一路延伸到 cloud agents / automations
- 对 end-user 来说，平台能力是“看得见、点得到、能直接工作”的
- 通常会比较强调：
  - plan / debug / terminal
  - browser loop
  - subagents
  - artifacts
  - enterprise controls
  - cross-functional adoption

代表对象：
- [[cursor]]

它最擅长回答的问题：
- 怎样让很多角色都在同一个 agent working surface 上工作？

最强项：
- workflow breadth
- interaction surface 完整度
- 本地到云端的一体化体验
- 平台作为工作台的可见性

天然弱项：
- 容易让人误以为“工作面完整 = 底层运行面已经被充分证明”
- 组织 operating model 证据，常常落后于产品控制面成熟度

适合谁：
- 想先把 agent 变成团队日常工作台的组织
- 很重视 adoption 面、交互面、workflow 宽度的团队

## Archetype 2：托管底座型
一句话：
- 把最难自建的 agent runtime、sandbox、session、lifecycle 直接托管成平台底座。

核心特征：
- 平台感主要来自运行底座，而不是 end-user 界面
- 更强调 secure runtime、durable state、sandbox、lifecycle management
- 常常适合嵌进产品闭环，而不只是给人直接使用
- 更像 managed substrate，而不是广义工作台

代表对象：
- [[claude-managed-agents]]

它最擅长回答的问题：
- 怎样让团队不用自己造 runtime，就能把 agent 安全地接进真实产品或后台流程？

最强项：
- managed runtime
- governance-first substrate
- 托管安全边界
- customer product embedding

天然弱项：
- workflow breadth 的公开证据通常不如工作台型丰富
- end-user surface 不一定是主卖点
- 容易被误解成“只是 API / 只是底层”，其实它已经是平台，只是平台层级不同

适合谁：
- 已经明确要做后台 agent / product-embedded agent 的团队
- 不想自己造 secure runtime / lifecycle / sandbox 的组织

## Archetype 3：开放骨架型
一句话：
- 提供足够完整的 runtime / memory / permissions / subagents / sandbox 骨架，让团队自己搭平台。

核心特征：
- 平台价值主要来自可构建性，而不是开箱即用完成态
- 更强调：
  - runtime primitives
  - memory / filesystem
  - permission rules
  - HITL
  - backend abstraction
  - developer control
- 更适合被看作自建平台底盘或 reference implementation

代表对象：
- [[deepagents]]

它最擅长回答的问题：
- 如果我不想把平台能力绑定到一个供应商成品上，怎样拿一套开放骨架自己搭出 agent platform？

最强项：
- 自定义权
- 可移植性
- open harness 路线的底盘价值
- 很适合当 reference implementation

天然弱项：
- 组织 adoption 和治理落地需要团队自己补
- 平台 readiness 更多来自“骨架完整”，而不是“商业成品已经大规模被证明”
- 容易被人误判成“只是框架”，其实它已经比普通 framework 更接近平台骨架

适合谁：
- 重视 provider independence
- 有平台工程能力
- 想自己掌控 runtime / workflow / governance 组合方式的团队

## 一张总对照表
| Archetype | 代表对象 | 核心价值 | 平台感主要来自 | 最强项 | 天然短板 |
|---|---|---|---|---|---|
| 平台工作台型 | [[cursor]] | 把 agent 变成日常工作面 | interaction surface + workflow surface | workflow 宽度、交互完整度、跨职能工作面 | 底层与组织证据可能落后于产品面 |
| 托管底座型 | [[claude-managed-agents]] | 把 runtime / sandbox / lifecycle 托管出去 | managed runtime substrate | 安全运行面、平台底座感、可嵌入产品闭环 | workflow 广度公开证据较窄 |
| 开放骨架型 | [[deepagents]] | 给团队一套自建平台的开放底盘 | runtime primitives + harness skeleton | 自定义权、开放性、底盘价值 | adoption / governance 需团队自己补 |

## 最常见的误判

### 误判 1：把三者当同类产品打排行榜
不对。
它们回答的问题层级不同：
- 工作台型在回答“怎么让人和 agent 一起工作”
- 托管底座型在回答“怎么让 agent 安全持续地跑”
- 开放骨架型在回答“怎么自己搭出平台”

### 误判 2：觉得工作台型更完整，所以一定更高级
不对。
工作台更完整，不代表底座更强。
很多时候，你真正缺的是 runtime substrate，不是更多 UI surface。

### 误判 3：觉得托管底座型更底层，所以一定更通用
也不对。
底座强不代表 workflow 宽。
如果团队要的是 adoption 面和工作面，光有底座不够。

### 误判 4：觉得开放骨架型只是框架，不算平台
这也不对。
当一个开放对象已经提供 runtime、memory、permissions、subagents、sandbox backends 这些骨架能力时，它就已经在平台边缘了，只是平台完成度和商业产品不同。

## 一条很实用的选型问法
别先问“选哪个产品”，先问你缺哪一层：

1. 如果你缺的是：
- 团队统一工作面
- 更宽的 workflow surface
- 本地到云端的一体化体验
先看：平台工作台型

2. 如果你缺的是：
- secure runtime
- durable session
- lifecycle management
- 托管运行面
先看：托管底座型

3. 如果你缺的是：
- provider independence
- 自建平台底盘
- runtime / workflow / governance 自定义权
先看：开放骨架型

## 结论
当前 coding agent 平台路线，至少已经分化成三种很不同的 archetype：
- [[cursor]] 代表平台工作台型
- [[claude-managed-agents]] 代表托管底座型
- [[deepagents]] 代表开放骨架型

如果一定要压成一句：
- 工作台型负责“让人用起来”
- 托管底座型负责“让 agent 跑起来”
- 开放骨架型负责“让团队自己搭起来”

## 关联页面
- [[cursor-platform-readiness-audit]]
- [[claude-managed-agents-platform-readiness-audit]]
- [[deepagents-platform-readiness-audit]]
- [[cursor-vs-claude-managed-agents-platform-readiness]]
- [[managed-harness-vs-open-harness]]
- [[coding-agent-platform-readiness-audit]]

## 来源
- [[cursor-product-2026-04-14]]
- [[cursor-money-forward-case-study-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[claude-x-post-2041927687460024721-2026-04-14]]
- [[langchain-deepagents-overview-2026-04-14]]
- [[langchain-anatomy-of-an-agent-harness-2026-04-14]]
