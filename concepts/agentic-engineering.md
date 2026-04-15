---
title: Agentic Engineering
created: 2026-04-14
updated: 2026-04-15
type: concept
tags: [concept, agentic-engineering, workflow, orchestration, coding-agent, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/cursor-money-forward-case-study-2026-04-14.md, raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md, raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md]
---

# Agentic Engineering

## 定义
agentic engineering 指把智能体视作系统中的主动执行者之后，对任务分解、工具使用、状态流转、审查机制、人机分工和恢复策略所做的工程化设计。重点不只是“模型能不能做”，而是“如何把智能体纳入稳定可运行的生产流程”。

## 在这些文章中的体现
[[openai]] 的文章虽然主标题是 [[harness-engineering]]，但背后其实也呈现了典型的 agentic engineering：工程师不再直接写每一行代码，而是设计任务、约束、审批与闭环，让 [[codex]] 作为主动执行者持续推进 PR、修复、验证和合并。Money Forward 这篇案例则把 agentic engineering 从“工程团队里的执行者设计”，扩到了“整个软件组织的人机分工重构”：QA、product、design 都开始把 agent 当作主动参与者，而不只是问答助手。Sentry 这篇案例又补了另一类信号：agent 不只是内部辅助者，还能被直接嵌进产品本身的 bug fixing 流水线里。

## 关键关注点
- 智能体能执行哪些阶段：编码、测试、评审、修复、合并、清理？
- 任务如何拆解成智能体能稳定处理的粒度？
- 人类应该在哪些节点介入判断，哪些节点应自动化？
- 当智能体出错、漂移或卡住时，系统如何恢复？
- 哪些非工程角色也该被纳入 agent workflow，而不是只围绕程序员设计？
- agent 是只在团队内部用，还是会变成你产品能力的一部分？

## 常见设计元素
- 明确的任务入口、验收标准和完成定义。
- 工具链接入，例如代码托管、测试、日志、浏览器、可观测性与部署环境。
- 自动审查、结构测试、lint 和反馈循环。
- 智能体之间的协作、复查与后台维护任务，例如文档修剪、技术债清理。
- 跨职能工作流设计：让 QA、product、design 等角色也能稳定调用 agent。
- 产品级 agent handoff 设计：比如 Sentry 把 RCA 结果直接交给 coding agent 生成 PR。
- 当 building layer 继续 commodity 化时，agentic engineering 还需要回答另一个更上层的问题：系统是否会随着组织的真实流程、数据与使用模式持续适配，还是仍停留在人工配置出来的静态 agent。João Moura 把后一种更深层方向称为 [[entangled-software]]。
## 与相近概念的关系
- [[agentic-engineering]] 关心的是“让智能体成为工作流中的 actor”。
- [[harness-engineering]] 更强调为了让这个 actor 稳定工作，需要怎样的环境、支架和控制系统。
- [[context-engineering]] 则聚焦信息输入层，帮助智能体获得正确上下文。
- 在实践里，这三者高度重叠，但问题焦点不同：actor、context、harness 分别对应执行者、信息供给和运行支架。

## 常见误区
- 只让智能体“多做事”，却不给足工具、验证和恢复机制。
- 把 agentic engineering 当作产品 demo 编排，而不是工程系统设计。
- 忽略人机边界，导致该人工判断的决策被过度自动化。
- 把 agent 只设计给工程师用，忽略它对 QA、product、design 等角色的流程重塑价值。
- 只把 agent 当作团队内部工具，忽略它也可能成为对外产品能力的一部分。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[cursor-money-forward-case-study-2026-04-14]]
- [[anthropic-sentry-managed-agents-case-study-2026-04-14]]
- [[joao-moura-x-post-2043726271449112776-2026-04-15]]
