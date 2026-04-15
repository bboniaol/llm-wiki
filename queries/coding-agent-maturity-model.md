---
title: Coding Agent Maturity Model
created: 2026-04-14
updated: 2026-04-14
type: query
tags: [query-note, workflow, harness-engineering, agentic-engineering, best-practice, infrastructure]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/anthropic-effective-context-engineering-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/inngest-harness-not-framework-2026-04-14.md, raw/articles/claude-x-post-2041927687460024721-2026-04-14.md, raw/articles/gabe-pereyra-x-post-2041568552256197074-2026-04-14.md]
---

# Coding Agent Maturity Model

## 问题
如果把一支团队使用 coding agent 的成熟度压成一张总图，应该怎么分层？什么算试用，什么算可复用，什么算可治理，什么才算真正的平台化？

## 短答案
我更认可把 coding agent maturity 分成 5 级：

1. 可试用
2. 可稳定
3. 可复用
4. 可治理
5. 可平台化

这 5 级不是“买了更贵的工具”就自然升级，而是分别回答了 5 个不同问题：
- 它能不能用？
- 它稳不稳？
- 别人能不能复用？
- 组织敢不敢依赖？
- 它能不能成为共享 operating model？

## 为什么这页值得单独存在
当前这套 wiki 其实已经有多张结构页：
- [[coding-agent-reliability-stack]] 讲的是稳定落地所需的六层能力
- [[from-local-coding-agent-to-team-agent-platform]] 讲的是演进路线
- [[coding-agent-adoption-patterns]] 讲的是扩散方式
- [[coding-agent-org-design-patterns]] 讲的是责任地图
- [[coding-agent-governance-checklist]] 讲的是最低上线门槛

这页的作用，是把它们再往上收一层，变成一张成熟度模型总图。

## 五级成熟度模型

### Level 1：可试用
一句话：
- agent 已经能帮少数人完成真实小任务，但仍然主要靠个人手感驱动。

典型特征：
- 有人已经在真实仓库里用 agent 写代码、查文档、做局部修改
- 任务以短平快为主
- 成功很依赖高手个人 prompt、个人判断和个人纠偏
- 规则、memory、workflow 基本还没沉淀成共享资产

常见表现：
- 看起来很惊艳
- 但复现性差
- 离团队级 adoption 还远

这一层回答的是：
- 它能不能帮我干活？

对应页面：
- [[coding-agent-adoption-patterns]] 里的 individual pull
- [[from-local-coding-agent-to-team-agent-platform]] 的“本地可用”

### Level 2：可稳定
一句话：
- agent 不只是偶尔灵光，而是多数时候不添乱。

典型特征：
- [[context-engineering]] 已经成形
- 有基本的 [[agent-approval-patterns]] / [[agent-sandboxing]]
- 验证信号更清楚，不再只靠 agent 自评
- 失败模式开始可预期，而不是随机爆炸

常见表现：
- agent 开始能持续处理一类任务
- 团队对它的信任从“玩具”提升到“可作为辅助执行者”

这一层回答的是：
- 它稳不稳？

对应页面：
- [[coding-agent-reliability-stack]] 的前 1-3 层
- [[from-local-coding-agent-to-team-agent-platform]] 的“本地稳定”

### Level 3：可复用
一句话：
- agent 能力开始脱离个人手感，变成团队内可复制的 workflow。

典型特征：
- rules、memory、skills、workflow 模板开始沉淀
- 有明确 wedge workflow，例如 review、bugfix、test generation、RCA-to-PR
- 新人或别的团队成员也能沿着同样流程跑出相近结果
- 失败后有可接手、可恢复的工件和状态

常见表现：
- 局部团队已经形成“agent working style”
- 但运行面和治理面还未完全组织化

这一层回答的是：
- 别人能不能也用起来？

对应页面：
- [[coding-agent-adoption-patterns]] 的 workflow wedge
- [[coding-agent-workflow-patterns]]
- [[from-local-coding-agent-to-team-agent-platform]] 的“本地可复用”

### Level 4：可治理
一句话：
- 组织已经不只是“能用 agent”，而是“敢把重要流程交给 agent”。

典型特征：
- 后台运行面、durable state、shared identity、artifacts、audit logs 已出现
- 审批、验收、回退、责任边界明确
- 组织知道谁定义 workflow、谁批准高风险动作、谁维护 runtime、谁看 traces
- agent 结果开始进入团队日常节拍，而不是实验项目

常见表现：
- 可以异步跑任务、生成 PR、附带证据
- 事故后能追责、能回放、能复盘
- 平台能力开始比单会话技巧更重要

这一层回答的是：
- 组织敢不敢依赖？

对应页面：
- [[coding-agent-governance-checklist]]
- [[coding-agent-org-design-patterns]]
- [[managed-harness-vs-open-harness]]
- [[cloud-agent-operations]]

### Level 5：可平台化
一句话：
- coding agent 已经从团队工具升级成共享 operating model，开始重塑组织如何交付软件。

典型特征：
- agent 不只服务工程师个人，而进入 QA、product、design、support 等角色
- 后台 agent、云端 runtime、workflow orchestration、team governance 已经组合成系统
- 组织不是“用了 agent”，而是把 agent 纳入 SDLC / 产品闭环 / 运营闭环
- 平台团队和业务团队之间形成稳定分工

常见表现：
- adoption 不再靠局部 champion 硬拉
- agent 成为组织标准工作面的一部分
- 可以谈 operating model，而不仅是工具选型

这一层回答的是：
- 它能不能成为组织共享能力和运行模型？

对应页面：
- [[from-local-coding-agent-to-team-agent-platform]] 的后 3 阶段
- [[coding-agent-adoption-patterns]] 的 cross-functional spillover
- [[coding-agent-org-design-patterns]] 的平台型模式

## 一张最实用的判断表
| 成熟度 | 关键问题 | 主要标志 | 最大风险 |
|---|---|---|---|
| Level 1 可试用 | 它能不能用？ | 少数高手真实在用 | 只停留在个人玩具 |
| Level 2 可稳定 | 它稳不稳？ | 上下文、权限、验证开始成形 | 看起来能用，实则高波动 |
| Level 3 可复用 | 别人能不能复制？ | workflow、rules、memory 已沉淀 | 个人成功无法团队扩散 |
| Level 4 可治理 | 组织敢不敢依赖？ | approval、audit、artifacts、回退、责任清楚 | 自动化已上生产，但没人兜底 |
| Level 5 可平台化 | 它能不能变成 operating model？ | 跨职能扩散、后台运行面、共享标准出现 | 平台很强，但 workflow 空心化 |

## 最常见的成熟度错觉

### 错觉 1：工具很强 = 成熟度很高
不是。
模型和产品再强，如果 workflow 不能复用、验收人不明确、失败不可回退，成熟度依然很低。

### 错觉 2：有 automation = 已经平台化
也不是。
很多团队只是把不稳定流程搬到了后台，并不等于进入 Level 5。

### 错觉 3：工程团队用得多 = 组织成熟
不够。
真正的高成熟度，通常还伴随：
- shared rules
- shared runtime
- shared evidence surface
- cross-functional spillover

### 错觉 4：有治理 = 会变慢
不一定。
低成熟度团队觉得治理是阻力，高成熟度团队会发现治理其实是在降低事故成本和沟通摩擦。

## 一个实用判定法
如果你只想快速判断团队当前在哪一级，我会问这 5 个问题：
1. 去掉最会用 agent 的那几个人，系统还好用吗？
2. 同一类任务能否稳定复跑，而不是全靠运气？
3. 新成员能否沿着已有 workflow 接手？
4. 出问题时，能否快速定位、回退、追责？
5. agent 是否已经进入跨角色、跨团队的共享工作面？

大致对应：
- 只能回答 1 → Level 1
- 能回答 1-2 → Level 2
- 能回答 1-3 → Level 3
- 能回答 1-4 → Level 4
- 五个都能稳答 → Level 5

## 我更认可的一条升级逻辑
成熟度提升通常不是直线加功能，而是这样长出来：
1. 先从局部可用开始
2. 再把稳定性补齐
3. 再让经验变成共享资产
4. 再把责任和治理接上
5. 最后才让 agent 真正变成组织 operating model 的一部分

也就是说：
- 先有用
- 再稳定
- 再复用
- 再治理
- 最后平台化

## 结论
coding agent maturity 的本质，不是“用了多少 AI”，而是：
- 从个人手感，走到组织能力
- 从局部惊艳，走到长期稳定
- 从单人效率，走到共享 operating model

如果一定要压成一句：
- Level 1-2 解决“能不能用”
- Level 3 解决“能不能复制”
- Level 4 解决“组织敢不敢依赖”
- Level 5 才解决“它是不是平台能力”

## 关联页面
- [[coding-agent-reliability-stack]]
- [[from-local-coding-agent-to-team-agent-platform]]
- [[coding-agent-adoption-patterns]]
- [[coding-agent-org-design-patterns]]
- [[coding-agent-governance-checklist]]
- [[managed-harness-vs-open-harness]]

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
- [[inngest-harness-not-framework-2026-04-14]]
- [[claude-x-post-2041927687460024721-2026-04-14]]
- [[gabe-pereyra-x-post-2041568552256197074-2026-04-14]]
