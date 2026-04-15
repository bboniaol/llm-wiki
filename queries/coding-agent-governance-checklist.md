---
title: Coding Agent Governance Checklist
created: 2026-04-14
updated: 2026-04-14
type: query
tags: [query-note, workflow, security, reliability, best-practice, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md, raw/articles/claude-x-post-2041927687460024721-2026-04-14.md, raw/articles/gabe-pereyra-x-post-2041568552256197074-2026-04-14.md]
---

# Coding Agent Governance Checklist

## 问题
如果一个团队准备把 coding agent 从“个人使用”推进到“团队可依赖”，上线前最少应该检查什么？

## 短答案
别把 governance 理解成合规文档堆。
governance 的最低目标只有一句话：
- agent 可以跑
- 跑偏时能拦
- 出事时能查
- 风险大时能回退

最实用的做法不是空谈原则，而是过一张 8 项 checklist：
1. 任务边界
2. 权限与身份
3. sandbox 与运行面
4. 审批与验收
5. 证据与可观测性
6. workflow 与回退
7. 组织责任
8. 成本与规模保护

如果这 8 项里有 3 项答不清，基本就还不该把 agent 当团队生产能力上线。

## 0. 先给一个结论阈值
上线前，至少要满足：
- 知道 agent 可以做什么，不能做什么
- 知道谁能批准高风险动作
- 知道失败后怎么回滚
- 知道出了问题去哪看 traces / artifacts / audit logs
- 知道谁对结果负责

少任何一条，都不算治理到位。

## 1. 任务边界 checklist
要问：
- 哪些任务允许 agent 自动执行？
- 哪些任务只允许建议，不允许落地？
- done definition 是什么？
- 成功输出是 PR、comment、artifact，还是外部系统动作？

过线标准：
- 至少有 1-2 个边界清晰的 wedge workflow
- 能明确说出“什么任务不该交给 agent”
- 不是把“所有开发任务都能试试”当策略

红旗信号：
- workflow 目标模糊
- 没有明确成功定义
- 失败后只能靠人读聊天记录猜它想干嘛

关联页面：
- [[coding-agent-workflow-patterns]]
- [[coding-agent-adoption-patterns]]

## 2. 权限与身份 checklist
要问：
- agent 用的是什么身份？个人身份、service account，还是共享机器人身份？
- 高风险工具权限有没有单独分级？
- 是否区分 read / write / external side effect？
- cloud automation 的 ownership 是谁？

过线标准：
- 权限最小化，不是默认全开
- 高风险动作有明确升级路径
- 自动化任务不用个人长期凭证裸跑
- 至少能说清 agent 在 GitHub / Slack / CI / MCP 上的身份边界

红旗信号：
- 用开发者个人 token 跑长期 automation
- 谁都能新建高权限 agent
- 没人知道某个 bot 背后是谁的责任

关联页面：
- [[agent-approval-patterns]]
- [[cloud-agent-operations]]
- [[coding-agent-org-design-patterns]]

## 3. sandbox 与运行面 checklist
要问：
- agent 在哪里跑？本地、隔离 worktree、云端 VM，还是共享主机？
- 网络、文件系统、浏览器、部署权限有没有分层？
- automation 是不是和交互式会话混用一套控制策略？

过线标准：
- 本地和云端控制面分开设计
- 高风险任务不直接跑在主环境
- 有明确的 sandbox / protected paths / network policy
- 长任务和后台任务有独立运行面，不依赖某个人电脑一直在线

红旗信号：
- 把 allowlist 当安全证明
- 交互式 agent 和后台 automation 共用一套模糊权限
- 跑在生产凭证 / 主目录 / 主环境上却没有隔离

关联页面：
- [[agent-sandboxing]]
- [[local-agent-controls-vs-cloud-agent-controls]]
- [[managed-harness-vs-open-harness]]

## 4. 审批与验收 checklist
要问：
- 哪些动作必须人工批准？
- 审批发生在任务级、步骤级，还是工具级？
- 谁有最终验收权？
- 验收看什么证据，不通过又怎么退回？

过线标准：
- 验收权和执行权没有完全重叠
- 高风险动作有明确人工闸门
- PR、部署、外部消息、批量改动这类动作有特殊规则
- agent 不拥有“自己宣布 done”的绝对权力

红旗信号：
- 所有动作都要批，最后系统瘫痪
- 或者完全不批，最后没人敢背锅
- reviewer 看不到过程证据，只能看最终结果

关联页面：
- [[agent-approval-patterns]]
- [[coding-agent-org-design-patterns]]

## 5. 证据与可观测性 checklist
要问：
- 每次运行有没有 traces、logs、artifacts、screenshots、PR references？
- 失败时能不能快速定位：它看到了什么、做了什么、卡在哪？
- 审计日志和运行日志是否分得开？
- 谁可以访问这些证据？

过线标准：
- 不只是 success / failure 二值状态
- 至少能回放关键运行证据
- 后台 agent 输出和审计记录可被团队查询
- reviewer / oncall / owner 能看到足够证据来做判断

红旗信号：
- 只留一句“已完成”
- 出了事只能翻聊天历史
- 平台团队看得到日志，业务 owner 看不到

关联页面：
- [[agent-observability]]
- [[coding-agent-org-design-patterns]]

## 6. workflow 与回退 checklist
要问：
- 失败后怎么回滚？
- 有没有 checkpoint、branch、artifact-based handoff？
- agent 被打断、卡死、跑偏时，下一轮怎么接手？
- workflow 是不是已经模式化，还是每次临时编？

过线标准：
- 至少一条核心 workflow 可以稳定复跑
- 有回退路径，而不是只能“手工救火”
- 长任务有显式收尾动作和可接班状态
- automation prompt 被当系统资产管理，不是随手复制一段聊天

红旗信号：
- 一失败就全靠人工从头重做
- branch / artifact / progress 状态混乱
- 没人说得清该从哪一步恢复

关联页面：
- [[coding-agent-workflow-patterns]]
- [[coding-agent-reliability-stack]]
- [[from-local-coding-agent-to-team-agent-platform]]

## 7. 组织责任 checklist
要问：
- 谁定义 workflow？
- 谁维护 runtime / permissions / service identities？
- 谁对 agent 产出最终负责？
- 谁在事故中主持复盘？

过线标准：
- 至少能区分：workflow owner、runtime owner、review / approval owner
- 不把所有责任糊成一个“AI owner”
- 谁受结果影响，谁就能看到证据面

红旗信号：
- 只有平台，没有 workflow owner
- 只有执行者，没有验收者
- 出问题后责任在团队间踢皮球

关联页面：
- [[coding-agent-org-design-patterns]]
- [[agentic-engineering]]

## 8. 成本与规模保护 checklist
要问：
- 有没有并发、预算、频率、运行时长限制？
- automation 失控时会不会烧穿 token / compute / CI 预算？
- 有没有避免无限重试、重复触发、事件风暴的保护？

过线标准：
- 至少有运行预算感知
- 高频 automation 有速率或并发保护
- 重试和事件触发不会无限放大

红旗信号：
- “先放开跑，回头再看账单”
- 没有 singleton / concurrency / retry guard
- 平台只盯功能，不盯成本与失控面

关联页面：
- [[cloud-agent-operations]]
- [[managed-harness-vs-open-harness]]

## 最低上线门槛：一眼版
如果你只想要一版最短判断，我会看这 6 条：
1. 有清晰 wedge workflow
2. 有最小权限和独立身份
3. 有 sandbox / 隔离运行面
4. 有人工批准和最终验收人
5. 有 traces / artifacts / audit logs
6. 有回退和责任归属

这 6 条过了，才配谈“团队可依赖”。

## 结论
coding agent governance 不是为了让组织显得成熟，而是为了防止三件事：
- 自动化跑偏却没人拦
- 结果出错却没人查
- 责任落地却没人认

所以最实用的治理标准不是“写了多少制度”，而是：
- 任务边界清不清
- 权限身份明不明
- 运行面隔不隔离
- 批准验收清不清楚
- 证据链完不完整
- 回退责任站不站得住

## 关联页面
- [[coding-agent-org-design-patterns]]
- [[coding-agent-adoption-patterns]]
- [[coding-agent-reliability-stack]]
- [[managed-harness-vs-open-harness]]
- [[from-local-coding-agent-to-team-agent-platform]]

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[cursor-docs-reference-permissions-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-cloud-agent-overview-2026-04-14]]
- [[cursor-docs-cloud-agent-automations-2026-04-14]]
- [[cursor-docs-enterprise-llm-safety-controls-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[anthropic-circleci-claude-case-study-2026-04-14]]
- [[claude-x-post-2041927687460024721-2026-04-14]]
- [[gabe-pereyra-x-post-2041568552256197074-2026-04-14]]
