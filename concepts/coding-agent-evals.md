---
title: Coding Agent Evals
created: 2026-04-14
updated: 2026-04-14
type: concept
tags: [concept, evaluation, coding-agent, benchmark, testing, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/wolfbench-site-overview-2026-04-14.md, raw/articles/wolfbench-github-repo-overview-2026-04-14.md]
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
- GitHub 仓库进一步补了方法细节：统一 sandbox 条件、5 次重复运行、1h timeout、结果存入 `wolfbench-runs/`，trace 上传到 W&B Weave。
- 这类信号的价值在于补第三方评测层；但即便如此，仍要区分“有方法说明”与“方法已被充分审查”这两件事。

## 评测对象不只是模型
在智能体系统里，eval 的对象通常是“模型 + 上下文 + 工具 + 约束 + workflow”的组合体，而不是裸模型。因此，评测结果本质上也在反映 [[context-engineering]]、[[agentic-engineering]] 和 [[harness-engineering]] 的整体质量。

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

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[wolfbench-hermes-agent-x-post-2026-04-14]]
- [[wolfbench-site-overview-2026-04-14]]
- [[wolfbench-github-repo-overview-2026-04-14]]
