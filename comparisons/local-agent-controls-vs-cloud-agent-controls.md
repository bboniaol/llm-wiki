---
title: Local Agent Controls vs Cloud Agent Controls
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, security, workflow, infrastructure, best-practice, harness-engineering]
sources: [raw/articles/cursor-docs-reference-permissions-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md]
---

# Local Agent Controls vs Cloud Agent Controls

## 为什么要区分
很多团队会把“agent 控制面”当成一套统一问题来谈，但本地 agent 和 cloud agent 面对的风险面、运行方式、审计要求完全不同。本地更像“交互式协作控制”；云端更像“后台自动化治理”。如果不分开设计，轻则控制失焦，重则把后台自动化当成本地小助手来放权。

## 对比表
| 维度 | Local agent controls | Cloud agent controls |
|---|---|---|
| 运行位置 | 本地终端 / IDE / 浏览器上下文 | 云端隔离 VM / 后台 automation |
| 核心问题 | 怎样在高交互场景下安全放权 | 怎样在无人值守和并行执行下可控运行 |
| 主要控制对象 | terminal、browser、MCP、文件修改、origin | triggers、identity、tool scope、branch/PR、artifacts、audit logs |
| 常见控制手段 | `permissions.json`、`sandbox.json`、browser allowlist、逐步 approval | team-owned automations、permission scope、service identity、enterprise safety controls、hooks、audit logging |
| 典型证据 | 本地提示、命令审批、回滚 checkpoint、浏览器日志 | PR artifacts、screenshots/videos、log references、audit logs、webhook/hook 输出 |
| 主要失败模式 | 用户误放权、allowlist 误解成安全边界、本地越权 | 后台长期越权、自动化 prompt 漂移、无人感知失败、审计断层 |

## Local controls 的强项
- 更适合高交互任务：边看边改、边批边跑、边调试边验证。
- 用户可以在每个关键动作前介入，纠偏成本低。
- 本地沙箱、browser origin 控制、checkpoint 回滚这类能力，对探索式开发特别顺手。
- 更容易把“人类判断”插入执行链条。

## Cloud controls 的强项
- 适合长任务、并行任务、定时任务和事件驱动任务。
- 不依赖本地机器在线，可以把 agent 变成后台劳动力。
- 更容易形成组织级治理：team-owned billing、shared identity、audit logs、hooks、DLP。
- 能把 artifacts 跟 PR / issue / 自动化运行绑在一起，方便远程验收。

## 设计重点的本质差异
### 本地控制重点：交互安全
本地 agent 的核心是“在不打断太多操作流的前提下，控制高风险动作”。所以重点会落在：
- 命令审批
- allowlist / sandbox
- browser origin 控制
- 文件保护
- checkpoint 回滚

### 云端控制重点：运行治理
cloud agent 的核心是“在没人盯着的时候，它还能按边界运行且留下证据”。所以重点会落在：
- trigger 设计
- tool scope
- identity / ownership
- artifacts 输出
- audit / hooks / compliance logging
- enterprise deterministic controls

## 一个实用判断法
- 如果问题是“这个命令现在该不该跑”，你在处理 local controls。
- 如果问题是“这个 automation 每天跑 20 次会不会越权、出了事谁知道”，你在处理 cloud controls。

## 更现实的结论：两者不是替代，而是分层
成熟系统通常是：
1. 本地先用 local controls 支撑探索、开发、调试；
2. 稳定后的 workflow 再迁移到 cloud controls，做后台自动化、并行执行和组织级治理。

也就是说，本地控制更像“副驾驶护栏”，云端控制更像“生产调度与合规系统”。

## 常见误区
- 把本地 allowlist 逻辑直接照搬到 cloud automation。
- 以为有云端隔离 VM 就自动安全了，忽略 identity、trigger 和审计问题。
- 把 cloud agent 只当远程机器，不把它当后台系统资产管理。
- 在本地过度治理，导致交互效率崩掉；在云端治理不足，导致后台风险积累。

## 结论
local agent controls 和 cloud agent controls 解决的是两类不同问题：前者解决交互式放权，后者解决后台化治理。真正成熟的 agent 平台，不是只把本地权限做细，或者只把云端自动化做强，而是明确区分：本地看“怎么安全协作”，云端看“怎么长期可控运行”。

## 来源
- [[cursor-docs-reference-permissions-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
- [[cursor-docs-cloud-agent-overview-2026-04-14]]
- [[cursor-docs-cloud-agent-automations-2026-04-14]]
- [[cursor-docs-cloud-agent-capabilities-2026-04-14]]
- [[cursor-docs-enterprise-llm-safety-controls-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
