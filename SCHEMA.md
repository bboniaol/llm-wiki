# Wiki Schema

## Domain
AI 圈 Harness Engineering 学习知识库。聚焦 AI Agent / Coding Agent / Eval / Context Engineering / Tooling / Workflow / Infra / Case Study 等与 harness engineering 直接相关的知识，不收录泛化的 AI 新闻八卦，也不做大而全的机器学习百科。

## Conventions
- 文件名统一小写、短横线命名、无空格，例如：`agent-evals.md`、`openai-codex-cli.md`
- 每个 wiki 页面必须以 YAML frontmatter 开头
- 页面之间使用 `[[wikilinks]]` 互相链接；每个新页面至少有 2 个外链
- 更新页面时必须同步修改 `updated` 日期
- 每个新页面必须同步登记到 `index.md`
- 每次创建、更新、查询、巡检都必须追加到 `log.md`
- `raw/` 下的源材料只增不改，纠错写入 wiki 页面，不回写原始资料
- 页面默认中文书写；专有名词保留英文原文，首次出现时给出中文解释
- 优先沉淀“可复用认知”：定义、框架、对比、工作流、坑点、案例，而不是大段搬运原文

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/articles/source-name.md]
---
```

## Tag Taxonomy
### 基础对象
- person
- company
- lab
- product
- model
- framework
- repo
- open-source

### 工程主题
- harness-engineering
- agentic-engineering
- context-engineering
- evaluation
- tooling
- workflow
- infrastructure
- deployment
- documentation
- observability
- reliability
- security
- cost

### 能力与技术
- prompting
- tool-calling
- memory
- planning
- orchestration
- coding-agent
- benchmark
- dataset
- testing
- automation

### 内容类型
- concept
- comparison
- case-study
- best-practice
- anti-pattern
- glossary
- timeline
- query-note

规则：页面里使用的 tag 必须先出现在这里；如果需要新 tag，先更新本文件，再落页面。

## Page Thresholds
- 当一个实体/概念在 2 个以上来源出现，或在 1 个来源中是核心主题时，创建独立页面
- 如果只是已有主题的新信息，优先补充到现有页面，不要重复造页
- 对于路过式提及、边角信息、与本知识库范围无关内容，不单独建页
- 单页超过约 200 行时考虑拆分为子页面
- 被完全替代的页面移入 `_archive/`，并从索引移除

## Entity Pages
一个重要实体一页。适用于人物、公司、实验室、产品、模型、框架、仓库。建议包含：
- 它是什么 / 为什么重要
- 关键时间点与演化
- 与其他实体和概念的关系（至少链接 2 个页面）
- 相关来源与原始证据

## Concept Pages
一个核心概念一页。建议包含：
- 定义与边界
- 它在 harness engineering 中解决什么问题
- 主流做法 / 设计模式
- 常见误区 / 未解决问题
- 相关页面链接

## Comparison Pages
用于横向比较产品、框架、方案、理念。建议包含：
- 比较对象与背景
- 对比维度（优先表格）
- 结论：适用场景、权衡、推荐
- 相关来源

## Query Pages
只保存“值得复用”的查询结论，例如：
- 某类 agent 框架选型建议
- 某个话题的阶段性判断
- 系统性综述
普通一次性问答不要归档。

## Seed Topics
初始化阶段优先围绕以下主题建库：
- harness engineering 的定义、边界、与 agentic engineering / context engineering 的关系
- coding agent 的评测、基准、可靠性、回放、可观测性
- tool use、memory、planning、delegation、sandbox、approval 等核心能力
- OpenAI Codex、Claude Code、Cursor、Hermes Agent、OpenHands、Devin 等工具/产品
- 典型工程实践：任务分解、测试闭环、审计、故障恢复、成本控制

## Update Policy
当新信息与现有内容冲突时：
1. 先看时间，较新的可信来源优先
2. 若确有冲突，保留双方观点并标注日期与来源
3. 在 frontmatter 中加入 `contradictions: [page-name]`
4. 在下次 lint 报告中标记出来，待人工确认
