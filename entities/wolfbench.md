---
title: WolfBench
created: 2026-04-14
updated: 2026-04-14
type: entity
tags: [product, benchmark, evaluation, harness-engineering, case-study]
sources: [raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md, raw/articles/wolfbench-site-overview-2026-04-14.md, raw/articles/wolfbench-github-repo-overview-2026-04-14.md]
---

# WolfBench

## 它是什么
WolfBench 是一个面向真实任务的 coding / agent benchmark 框架。根据官网，它基于 Terminal-Bench 2.0，把 89 个真实任务的结果从单一平均分拆成五个互补指标，用来衡量 agent / harness 的稳定性分布，而不只是一次高分。此前库里只有一条公开 X 帖子；现在官网材料补上后，这条线已经从“社交信号”升级成“有方法说明的 benchmark 入口”。

## 这条来源的价值
- 它补的是第三方 benchmark 信号，而不是产品方自己写的 adoption case。
- 它把比较对象明确放在 harness 层，而不是简单模型层。
- 它突出的是任务解出稳定性，这和 [[coding-agent-evals]] 里“只看平均分不够，还要看稳定性”的判断是一致的。
- 它把方法写得更完整：Five-Metric Framework 基于 Terminal-Bench 2.0，用 solid / worst / average / best / ceiling 五个指标共同刻画 agent 表现分布。
- 官网与仓库一起补上了实验设定信号：5 runs、1h timeout、统一 sandbox 资源条件，以及 same model / different agent 的横向比较思路。
- 仓库还说明了 run data 在 `wolfbench-runs/` 中组织，full trajectories / traces 上传到 W&B Weave，这让它比“只有排行榜截图”的 benchmark 更可追溯。

## 现阶段边界
虽然官网与仓库已经把框架、运行流程和部分实现组件讲清楚了，但库里目前还没单独抓到更细的 task definitions、scoring implementation 细节、结果 schema 或 Harbor / Weave 集成代码的逐段分析，因此它现在仍更适合作为待继续跟踪的 benchmark 入口，而不是完全吃透的方法学页面。

## 关联
- [[how-to-read-agent-harness-benchmarks]] 总结了当前这条 benchmark 线在方法上该如何解读。
- [[coding-agent-evals]] 是这条线的主入口。
- [[hermes-agent]] 是当前帖子里表现最突出的对象。
- [[harness-engineering]] 用来解释为什么 benchmark 比的是 harness，而不是裸模型。
- [[codex-vs-claude-code-vs-cursor]] 暂时还没有纳入 WolfBench，因为当前第三方评测线对那三者的覆盖还不完整。

## 来源
- [[wolfbench-hermes-agent-x-post-2026-04-14]]
- [[wolfbench-site-overview-2026-04-14]]
- [[wolfbench-github-repo-overview-2026-04-14]]
