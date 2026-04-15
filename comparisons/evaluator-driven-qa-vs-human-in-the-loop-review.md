---
title: Evaluator-driven QA vs Human-in-the-loop Review
created: 2026-04-14
updated: 2026-04-14
type: comparison
tags: [comparison, reliability, testing, workflow, best-practice, harness-engineering]
sources: [raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-browser-2026-04-14.md]
---

# Evaluator-driven QA vs Human-in-the-loop Review

## 为什么要区分
这两种机制都在“给智能体输出把关”，但它们解决的问题不一样。[[evaluator-driven-qa]] 主要解决“生成 agent 自评失真”的问题；human-in-the-loop review 主要解决“高风险决策、产品判断和责任归属”问题。把两者混成一个词，会导致团队不是过度自动化，就是把所有事都推回给人。

## 对比表
| 维度 | [[evaluator-driven-qa]] | Human-in-the-loop review |
|---|---|---|
| 核心目标 | 用独立 evaluator 持续验证实现质量 | 在关键节点由人类做判断、批准或验收 |
| 主要角色 | generator / evaluator / contract / rubric | 人类 reviewer + 智能体执行者 |
| 最擅长处理 | UI 回归、功能缺陷、验收标准、边界条件 | 风险判断、产品方向、品味、责任、外部副作用 |
| 反馈速度 | 快，可轮转多次 | 慢，但更可靠、更有最终裁决权 |
| 成本结构 | 增加 token / 工具 / orchestration 成本 | 增加人工注意力与等待成本 |
| 失败模式 | evaluator 变宽松、评估漂移、误报漏报 | 人类 review 成瓶颈、只做表面确认、低吞吐 |
| 典型落点 | [[agent-feedback-loops]]、[[multi-agent-delegation]]、浏览器测试 | [[agent-approval-patterns]]、PR 审查、上线批准 |

## Evaluator-driven QA 的强项
- 可以在长链路任务里连续工作，不需要每次都等人上线。
- 适合用 Playwright、测试、日志、contract、rubric 做结构化验收。
- 更容易形成 generator → evaluator → generator 的自动修复闭环。
- 对“看起来像成品但实际有 bug”的场景特别有效。

## Human-in-the-loop review 的强项
- 能处理 evaluator 很难稳定量化的问题，例如产品取舍、业务风险、品牌品味、合规边界。
- 能为高风险动作提供明确责任归属，例如部署、外部消息、配置升级、权限放宽。
- 能在模型走偏时直接改方向，而不只是继续局部修补。
- 对“值得不值得做”“是不是该现在做”这类问题更强。

## 什么时候优先用哪种
### 更适合 evaluator-driven QA
- 前端 / 全栈应用需要频繁回归验证。
- 已经有明确 contract、测试标准或评分 rubric。
- 团队想降低人工 review 频率，但又不想放弃质量闭环。
- 任务处在模型 solo 还不够稳、但又不值得人类逐步盯防的区间。

### 更适合 human-in-the-loop review
- 涉及生产环境、敏感数据、外部沟通、权限变更。
- 输出质量高度依赖人类品味或业务上下文。
- 需要明确批准责任，而不是只要技术上“看起来能跑”。
- 团队还没有足够成熟的 [[evaluator-driven-qa]] 支架。

## 更现实的结论：两者通常是叠加，不是二选一
一个成熟系统往往是这样分层：
1. 先用 [[evaluator-driven-qa]] 做高速、结构化、可重复的自动验收；
2. 再用 human-in-the-loop review 处理高风险决策、最终批准和方向性判断。

也就是说，evaluator 更像“自动质检员”，人类 reviewer 更像“最终裁决者”。

## 常见误区
- 以为有 evaluator 就不需要人类 review。
- 以为只要有人 review，就不需要自动 QA。
- 把人类 reviewer 用在低价值机械检查上，浪费最稀缺的注意力。
- 把 evaluator 放到没有 contract、没有证据源的场景里，结果只是另一个会自信胡说的 agent。

## 结论
如果问题是“怎么更高频地发现实现缺陷”，优先补 [[evaluator-driven-qa]]；如果问题是“哪些动作必须有人拍板”，优先补 human-in-the-loop review 与 [[agent-approval-patterns]]。真正成熟的 agent workflow，不是用其中一个替代另一个，而是让自动评估先跑在前，人类判断守在关键节点。

## 来源
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[openai-harness-engineering-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-browser-2026-04-14]]
