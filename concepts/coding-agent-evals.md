---
title: Coding Agent Evals
created: 2026-04-14
updated: 2026-04-25
type: concept
tags: [concept, evaluation, coding-agent, benchmark, testing, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/wolfbench-site-overview-2026-04-14.md, raw/articles/wolfbench-github-repo-overview-2026-04-14.md, raw/articles/cognition-x-post-2044174496312242544-2026-04-16.md, raw/articles/cognition-swe-check-10x-faster-2026-04-16.md, raw/articles/langsmith-evaluation-overview-2026-04-16.md, raw/articles/braintrust-score-production-traces-2026-04-16.md, raw/articles/langfuse-evaluation-overview-2026-04-16.md, raw/articles/phoenix-evaluation-overview-2026-04-16.md, raw/articles/coderabbit-docs-overview-2026-04-16.md, raw/articles/meticulous-product-overview-2026-04-16.md, raw/papers/terminal-bench-2.0-paper-2026-01-17.md, raw/articles/stanford-meta-harness-tbench2-2026-04-25.md]
---

# Coding Agent Evals

## 定义
coding agent evals 指针对代码智能体执行软件工程任务能力所建立的评测体系。它不只看模型会不会补全代码，还评估其在修 bug、跑测试、理解仓库、调用工具、响应审查和完成多步骤任务时的表现。

## 为什么重要
当团队开始依赖 [[codex]] 这类智能体推进真实开发时，必须知道两个问题：
1. 智能体在哪些任务上可靠，哪些任务上容易失真；
2. 新的上下文、工具、规则或 workflow 调整，是否真的改善了结果。

没有评测，[[harness-engineering]] 就容易沦为凭感觉调系统。

## 评测维度
- 平均完成率：看总体分数，但不能掩盖大幅波动。
- 稳定性下限：看同一系统多次运行时，是否经常掉到很差的结果。
- Ceiling：理论上“至少有一次能做到多少”。
- Best / Worst：单次运行上下界。
- Solid：每次运行都稳定解出的任务比例。
- 任务完成率：是否真正达到验收标准
- 修复质量：是否只修表面，还是解决根因
- 工具使用能力：是否能正确调用测试、浏览器、日志和代码托管工具
- 仓库理解能力：是否能在复杂结构中找到正确修改点
- 稳定性：多次运行结果是否一致
- 成本与耗时：完成任务消耗多少时间、token 和人工介入

## 公开 benchmark 信号的新补充
- WolfBench 报告：[[hermes-agent]] 作为 harness，在 Opus 4.6 与 GPT-5.4 上都跑赢 Claude Code 与 OpenClaw。
- 更关键的是“higher floor”：这说明评测不只看 top run，而看多次运行的一致性。
- 官网进一步说明了 WolfBench 的 Five-Metric Framework：solid / worst / average / best / ceiling，用来展示性能分布而不是单点均值。
- 仓库还说明了 run data 在 `wolfbench-runs/` 中组织，full trajectories / traces 上传到 W&B Weave，这让它比"只有排行榜截图"的 benchmark 更可追溯。
- **Terminal-Bench 2.0**（arXiv:2601.11868，2026-01-17）是当前最重要的终端 agent benchmark 之一：89 个真实工作流任务，frontier models/agents 得分 < 65%，证明 benchmark 足够难以区分能力。使用 Harbor harness，支持 Claude Code、Codex CLI、OpenHands、Mini-SWE-Agent 等主流 agent。
- **Stanford Meta-Harness**（GitHub: stanford-iris-lab/meta-harness-tbench2-artifact）在 Terminal-Bench 2.0 上达到 **76.4%**（Claude Opus 4.6），是目前该 benchmark 上的最高分。关键创新：**automated harness evolution** — harness 不是人工设计，而是自动发现/进化出来的。核心 trick 是 **environment bootstrapping**：在 agent 循环开始前注入 sandbox 环境快照（工作目录、文件列表、可用语言/工具、包管理器、内存），节省 2-5 轮早期探索。这是 Akshay Pachaar 文中 "LLM 自优化 harness 76.4%" 的具体所指，也是 harness 层可以自动优化的首个公开实证。
- 这类信号的价值在于补第三方评测层；但即便如此，仍要区分"有方法说明"与"方法已被充分审查"这两件事。

## 评测对象不只是模型
在今天的新信号里，这个结论又被进一步压实：很多团队开始把评测能力沉成产品内的专用 checker，而不是只在离线 benchmark 里偶尔跑一次。

## 新增的产品化评测信号
- Cognition 的 [[cognition]] / SWE-check 信号把另一条 eval 路线推清楚了：评测不只发生在 benchmark 榜单上，也可以被产品化成持续运行的 bug detection checker。
- 这条路线最值得记的不是“10x faster”口号，而是其训练做法：在 production setting 中做 RL、用 reward linearization 把全局 F-score 目标转成 sample-level reward、再用两阶段 post-training 在能力与延迟之间做工程折中。
- 这说明 coding agent evals 的价值正从“阶段性测一次”扩展到“把 cheap evaluator / checker 挂到每次 diff 或每次运行里”，让评测成为 [[agent-feedback-loops]] 的常驻部件。

## 评测对象不只是模型
在智能体系统里，eval 的对象通常是“模型 + 上下文 + 工具 + 约束 + workflow”的组合体，而不是裸模型。因此，评测结果本质上也在反映 [[context-engineering]]、[[agentic-engineering]] 和 [[harness-engineering]] 的整体质量。

## 从离线 benchmark 到在线 eval 层
- 2026-04-16 新补的公开资料说明，eval 已经开始分成两种基础设施形态：
  - 一种是 LangSmith、Braintrust、Langfuse、Phoenix 这种 trace-native eval infra，把 scorer / evaluator 直接挂到生产 traces、logs 或 spans 上持续运行；
  - 另一种是 CodeRabbit、Meticulous 这种 workflow-native checker，把 review / regression check 常驻在 PR、CI 或 browser workflow 上。
- 这意味着 [[coding-agent-evals]] 不应再只理解成“周期性 benchmark”，还应理解成一个持续在线的质量层：负责监控真实流量、发现回归、筛选要审的 trace/PR，并把结果回灌到 [[agent-feedback-loops]]。
- 这条线的高价值信号不只是“能不能打分”，而是：是否支持生产 traces、自动规则/采样、span 级打分、evaluator 审计，以及与上线 gate 的连接。
- 更完整的阶段性判断见 [[from-offline-benchmark-to-online-evals]]。

## 与反馈回路的关系
- [[how-to-read-agent-harness-benchmarks]] 把“怎么看 harness benchmark”这件事单独收束成了一页读榜方法。
- [[coding-agent-evals]] 更像系统级体检，帮助你衡量某种配置是否变好了。
- [[agent-feedback-loops]] 更像实时纠偏机制，帮助单次任务在执行中自我修复。
- 两者结合起来，才能同时得到“长期变好”和“当下能救”。

## 常见误区
- 只看单次高分，不看 repeated runs 的稳定性下限。
- 只报平均分，不报 best / worst / solid / ceiling，结果把波动性全抹平。
- 不控制 sandbox 资源、timeout、重复次数，却把结果当成可横向比较的 benchmark。
- 只测 LeetCode/补全，不测真实仓库任务。
- 只看 pass rate，不看成本、稳定性和人工介入比例。
- 把评测当作模型排行榜，而不是工程系统诊断工具。
- **新误区：忽略 harness 层的可优化性**。Stanford Meta-Harness 证明 harness 可以通过 automated evolution 自动发现/优化，而不是只能凭经验手工调。这意味着 eval 体系也需要覆盖 "harness 优化能力" 本身。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[wolfbench-hermes-agent-x-post-2026-04-14]]
- [[wolfbench-site-overview-2026-04-14]]
- [[wolfbench-github-repo-overview-2026-04-14]]
- [[cognition-x-post-2044174496312242544-2026-04-16|cognition-x-post-2044174496312242544]]
- [[cognition-swe-check-10x-faster-2026-04-16]]
- [[terminal-bench-2.0-paper-2026-01-17|terminal-bench-2.0-paper]]
- [[stanford-meta-harness-tbench2-2026-04-25|stanford-meta-harness-tbench2]]
