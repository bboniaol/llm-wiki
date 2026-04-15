---
title: Coding Agent Platform Readiness Audit
created: 2026-04-14
updated: 2026-04-14
type: query
tags: [query-note, workflow, infrastructure, best-practice, harness-engineering, agentic-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/claude-x-post-2041927687460024721-2026-04-14.md, raw/articles/gabe-pereyra-x-post-2041568552256197074-2026-04-14.md]
---

# Coding Agent Platform Readiness Audit

## 问题
如果现在要审一支团队，判断它到底有没有准备好从“会用 coding agent”进入“agent 平台阶段”，最实用的审计框架应该长什么样？

## 短答案
不要只问“他们用了什么工具”，要问 5 个层面：

1. workflow readiness
2. reliability readiness
3. governance readiness
4. org readiness
5. platform readiness

这 5 层里，只要有 2 层明显空心，就说明这团队还没准备好进入平台期。

一句更狠的话：
- 不是“有 cloud agent”就算平台
- 也不是“有 automation”就算 ready
- 真正的 readiness，是 workflow、责任、治理、运行面和证据面同时过线

## 这页怎么用
这不是一页理念文，而是一张审计表。
你可以拿它去审：
- 一个团队是否该上 agent platform
- 一个 vendor 的“平台叙事”有多真
- 一个内部项目现在卡在能力问题，还是卡在组织问题

## 五层审计框架

### 1. Workflow readiness
核心问题：
- 有没有至少一个稳定 wedge workflow，而不是所有东西都“能试试”？

要审什么：
- 任务边界是否清楚
- done definition 是否明确
- workflow 是否模式化
- 失败后是否可恢复
- 新人是否能沿已有流程接手

判定标准：
- 低：主要靠个人 prompt 手感，流程不可复用
- 中：有 1-2 条可稳定复跑的 workflow
- 高：workflow 已成为团队共享资产，并能跨人复用

典型红旗：
- automation 很多，但没有一个流程能稳定跑通
- agent 常常“看起来完成了”，但没人说得清完成标准是什么

关联页面：
- [[coding-agent-workflow-patterns]]
- [[coding-agent-adoption-patterns]]

### 2. Reliability readiness
核心问题：
- 这个系统除了“偶尔有效”，是否已经具备可持续稳定性？

要审什么：
- 上下文治理是否成形
- 权限与工具面是否可控
- 验证信号是否足够清楚
- 状态与恢复机制是否存在
- 长任务与后台任务是否有编排能力

判定标准：
- 低：主要靠人工盯着纠偏
- 中：本地和中等复杂任务已可稳定完成
- 高：长任务、后台任务和团队协作任务也能稳定运行

典型红旗：
- 单轮 demo 漂亮，但多步链路就崩
- 失败无法定位层次，是上下文、验证、权限还是状态问题

关联页面：
- [[coding-agent-reliability-stack]]
- [[coding-agent-maturity-model]]

### 3. Governance readiness
核心问题：
- 组织有没有最低限度的“能拦、能查、能退、能追责”能力？

要审什么：
- 权限与身份是否最小化
- sandbox 与运行面是否隔离
- 高风险动作是否有批准机制
- traces / artifacts / audit logs 是否可得
- 回退机制是否存在
- 并发、预算、重试是否有保护

判定标准：
- 低：能跑，但基本没有控制面
- 中：关键动作已可批准、回放、回退
- 高：治理已成为默认运行方式，不依赖临时救火

典型红旗：
- 用个人 token 跑长期 automation
- 只留 success/failure，不留证据
- 出问题后只能问“当时谁在电脑前”

关联页面：
- [[coding-agent-governance-checklist]]
- [[agent-sandboxing]]
- [[local-agent-controls-vs-cloud-agent-controls]]

### 4. Org readiness
核心问题：
- 责任地图是不是清楚，还是大家都在模糊共担？

要审什么：
- 谁定义 workflow
- 谁维护 runtime / permissions / identities
- 谁拥有验收权
- 谁能批准高风险动作
- 谁在事故时能拿到完整证据并主持复盘

判定标准：
- 低：只有一个模糊 AI owner，大家都说自己只是配合
- 中：workflow owner / runtime owner / reviewer 已初步分开
- 高：责任边界清楚，平台团队与业务团队协作稳定

典型红旗：
- 只有平台，没有 workflow owner
- 执行自动化有了，验收责任没人认
- reviewer 要背结果，但看不到 traces / artifacts

关联页面：
- [[coding-agent-org-design-patterns]]
- [[agentic-engineering]]

### 5. Platform readiness
核心问题：
- 这到底是“多人在用工具”，还是“已经形成共享 operating model”？

要审什么：
- 是否已进入后台运行面
- 是否有 shared identity、shared runtime、shared evidence surface
- 是否出现跨职能 spillover
- 是否已有 vendor/runtime 选型策略
- 是否已有平台团队与业务团队稳定分工

判定标准：
- 低：只是多人都装了同一工具
- 中：团队共享运行面与治理能力开始出现
- 高：agent 已经成为 SDLC / 产品闭环 / 运营闭环的一部分

典型红旗：
- 平台功能很全，但真实 workflow 很少
- 组织买了平台，却仍停留在个人助手阶段

关联页面：
- [[managed-harness-vs-open-harness]]
- [[from-local-coding-agent-to-team-agent-platform]]
- [[coding-agent-maturity-model]]

## 一张审计总表
| 维度 | 关键问题 | 低成熟信号 | 过线信号 | 红旗 |
|---|---|---|---|---|
| Workflow readiness | 有没有稳定 wedge workflow？ | 全靠个人手感 | 至少 1-2 条流程可稳定复跑 | automation 很多但没闭环 |
| Reliability readiness | 系统稳不稳？ | 单轮有效、多轮脆弱 | 上下文、验证、恢复、编排有层次 | 失败无法归因 |
| Governance readiness | 能拦、能查、能退吗？ | 控制面薄弱 | approval、audit、rollback 已成形 | 个人 token / 无证据运行 |
| Org readiness | 责任清不清？ | AI owner 一人兜底 | workflow / runtime / review 分责明确 | 有执行无人验收 |
| Platform readiness | 是否真形成共享 operating model？ | 只是多人装同一工具 | shared runtime + shared evidence + spillover 出现 | 平台很全但 workflow 空心 |

## 最短版审计问卷
如果只允许问 10 个问题，我会问：
1. 你们最稳定跑通的 2 条 agent workflow 是什么？
2. 去掉最会用的人，剩下的人还能跑吗？
3. 失败后，你们从哪里恢复？
4. 谁定义 done definition？
5. 谁批准高风险动作？
6. agent 用什么身份在跑？
7. traces / artifacts / audit logs 在哪看？
8. reviewer / oncall 能否直接看到这些证据？
9. 你们现在更像工具型、工作流型，还是平台型？
10. 如果明天把 agent 接到更多团队，最先崩的是哪一层？

这 10 个问题，基本能把“平台宣传”和“平台 readiness”分开。

## 一个实用评分法
可以粗暴打分，每层 0-2 分：
- 0 = 基本缺位
- 1 = 局部有了，但不稳定
- 2 = 已成默认能力

总分解释：
- 0-3：还在工具试用期，不该谈平台
- 4-6：已进入 workflow 建设期，可以继续打基础
- 7-8：开始具备平台 readiness，但治理和责任仍需补齐
- 9-10：已经接近真正的平台阶段

注意：
- 只要 Governance readiness 或 Org readiness 为 0，再高的总分也不算真正 ready

## 结论
platform readiness 不是“买没买平台”，而是：
- workflow 是否成形
- reliability 是否过线
- governance 是否兜底
- org responsibility 是否清楚
- platform surface 是否真的成为共享 operating model

所以最实用的审计结论通常不会是“上平台 / 不上平台”这么简单，而是：
- 现在卡在 workflow
- 卡在 reliability
- 卡在 governance
- 还是卡在 org design

只有先把卡点说清楚，平台这两个字才不是自我感动。

## 关联页面
- [[coding-agent-maturity-model]]
- [[coding-agent-governance-checklist]]
- [[coding-agent-org-design-patterns]]
- [[coding-agent-adoption-patterns]]
- [[coding-agent-reliability-stack]]
- [[managed-harness-vs-open-harness]]
- [[from-local-coding-agent-to-team-agent-platform]]

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[anthropic-effective-context-engineering-2026-04-14]]
- [[cursor-money-forward-case-study-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
- [[cursor-docs-cloud-agent-overview-2026-04-14]]
- [[cursor-docs-cloud-agent-automations-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
- [[cursor-docs-reference-permissions-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[inngest-harness-not-framework-2026-04-14]]
- [[claude-x-post-2041927687460024721-2026-04-14]]
- [[gabe-pereyra-x-post-2041568552256197074-2026-04-14]]
