---
title: Hermes Agent
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [product, coding-agent, harness-engineering, workflow, tooling]
sources: [raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/wolfbench-site-overview-2026-04-14.md, raw/articles/wolfbench-github-repo-overview-2026-04-14.md]
---

# Hermes Agent

## 它是什么
Hermes Agent 是一个面向真实工程任务的 coding / agentic harness 形态。在当前知识库里，它的重要性暂时不来自完整文档线，而来自一条明确的 benchmark 信号：在 WolfBench 披露的 89 个真实任务上，它作为 agentic harness 的表现超过了 Claude Code 与 OpenClaw，并且不只是平均分更高，稳定性下限也更高。

## 当前可确认的信号
- 它被 WolfBench 明确按“agentic harness”来比较，而不是只按裸模型比较。
- 这个比较现在不再只有 X 帖子摘要，WolfBench 官网已经公开了五指标展示框架与对应结果面板。
- WolfBench 仓库进一步说明，这类结果来自统一 sandbox 条件下的多次重复运行，而不是一次性单 run 宣布。
- 同时在 Opus 4.6 与 GPT-5.4 两个模型底座上取得领先，说明优势未必只是某一底模专属调优。
- WolfBench 特别强调 higher floor：不是只靠少数高光 run，而是更多任务在每次运行里都更稳定地解出。

## 现阶段边界
目前库里关于 [[hermes-agent]] 的公开证据还很薄，主要来自一条 X 帖子式 benchmark 宣布，因此现在更适合把它视为“值得跟踪的强信号”，而不是已经被充分文档化、充分案例化的成熟产品画像。

## 关联
- [[coding-agent-evals]] 是理解这条信号的第一入口。
- [[harness-engineering]] 很重要，因为这条 benchmark 明确比较的是 harness 表现而不是只比较模型。
- [[wolfbench]] 是当前这条证据的 benchmark 来源。

## 来源
- [[wolfbench-hermes-agent-x-post-2026-04-14]]
- [[wolfbench-site-overview-2026-04-14]]
- [[wolfbench-github-repo-overview-2026-04-14]]
