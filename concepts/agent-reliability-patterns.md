---
title: Agent Reliability Patterns
created: 2026-04-14
updated: 2026-04-24
type: concept
tags: [concept, reliability, testing, workflow, best-practice, harness-engineering]
sources: [raw/articles/openai-harness-engineering-2026-04-14.md, raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md, raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/cursor-docs-reference-sandbox-2026-04-14.md, raw/articles/cursor-docs-agent-security-2026-04-14.md, raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md, raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md, raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md, raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md, raw/articles/ltbase-harness-engineering-2026-04-24.md]
---

# Agent Reliability Patterns

## 定义
agent reliability patterns 指为提高智能体系统稳定性、可预测性和可恢复性而反复使用的一组工程设计模式。它们覆盖验证、约束、回滚、隔离、反馈、审查和长期治理等方面。

## 为什么它是专题级问题
在真实环境里，智能体偶尔做对并不难，难的是持续做对、出错能恢复、规模扩大后不崩。[[harness-engineering]] 的很多投入，本质上都在服务 reliability：让高吞吐系统不因为漂移、上下文污染、反馈缺失或工具误用而慢慢烂掉。

## 从 Anthropic 两篇文章补充出的可靠性模式
- 初始化与执行职责分离：initializer agent 先铺底，coding agent 再做增量推进。
- planner 先扩规格：把一句需求先变成完整 spec，降低 generator 低估范围、草草完工的概率。
- feature list 结构化：用 JSON 显式记录“未通过/已通过”的功能需求，减少随意修改目标。
- progress file + git history：让每轮 agent 都有接棒依据。
- init.sh + 基础回归：每轮开始先恢复服务并验证基本功能，而不是直接写新功能。
- evaluator + hard thresholds：把评估从“印象不错”变成基于 contract、Playwright 操作和评分标准的硬判断。
- 只在充分测试后标记完成：防止 agent 过早 declare victory。
- 随模型能力重估流程：并不是所有可靠性结构都永久保留，过重的 sprint 机制在更强模型上可能该删。

## 从 Cursor 深文档补出的可靠性信号
- sandbox.json 让网络、文件路径、共享构建缓存和受保护路径都能显式配置，而不是只靠默认设置。
- permissions.json 把 terminal / MCP auto-run allowlist 变成可版本化的配置层，并且有 team admin > file > IDE 的明确优先级。
- security 文档明确说 allowlist 不是安全保证，说明 Cursor 把 auto-approval 视为效率机制而不是绝对防线。
- browser tools 通过会话持久化、console/network 访问和 origin allowlist，把 UI 调试和浏览器自动化拉进可靠性闭环。
- cloud agents 把 screenshots、videos、logs artifacts 直接附着到 PR，说明“运行证据”本身被当成可靠性交付物。
- compliance / monitoring 文档补了一层组织级可靠性：后台 agent 不仅要能跑，还要能审计、流转日志、接入 hooks 与合规流程。

## 常见可靠性模式
- 指令节流：控制 `CLAUDE.md` / `AGENTS.md`、tool descriptions、skills 注入量，避免一开局就把 instruction budget 烧光。
- 渐进披露：按需激活技能、说明和工具，而不是默认全部常驻。
- 验证回压：通过 tests、lint、CI、contract 和其他 back-pressure 机制让 agent 不能轻易自我宣布完成。
- 控制流钩子：用 hooks 在关键生命周期节点自动接外部系统、注入检查或调整权限。
- 约束前置：先用结构边界、lint、schema 和命名规则减少可犯错空间。
- 验证闭环：每次改动都尽量进入测试、运行验证和反馈循环。
- 输出整形：成功时只返回极简信号，失败时再展开详细输出，避免验证过程本身变成上下文污染源。
- failFast：一次只暴露当前最关键的失败，减少 agent 在多个错误之间来回切换。
- 隔离执行：借助 [[agent-sandboxing]] 限制故障半径。
- 审批升级：高风险动作交由 [[agent-approval-patterns]] 守门。
- 持续清理：用 [[doc-gardening-agents]] 和后台维护任务降低熵增。
- 运行可见：把关键行为接入 [[agent-observability]]，便于追责和纠偏。
- 噪音隔离：让 sub-agents 只回传压缩结论与引用，避免可靠性问题被上下文膨胀放大。
- 跨窗口接力：让每一轮 agent 都能稳定重建现场，而不是靠猜。
- 角色互校：让 planner、builder、evaluator 形成分工，不把所有职责压给一个 agent。
- 回滚快照：像 Cursor 的 checkpoints 这类能力，能把“试错成本”压低到可接受范围。
- 证据随工单走：让 artifacts、audit log、hooks 输出跟着 PR / automation 一起流动，而不是散落在运行机里。
- back-pressure 要尽量 deterministic：如果已知什么结果最重要，不要把摘要权交给模型临时猜。

## 一个判断标准
如果一个智能体系统只能在“理想样例”里表现好，但面对长任务、异常反馈、工具失败、上下文切换或文档过期就开始发飘，那它还没有建立 reliability patterns。

## 与相近概念的关系
- [[coding-agent-reliability-stack]] 把当前库里分散的可靠性机制收束成一张六层方法地图。
- [[deterministic-backpressure-vs-durable-retries]] 进一步区分了“验证信号质量”和“流程恢复能力”这两类可靠性机制。
- [[agent-reliability-patterns]] 是跨专题的横向视角，把 [[agent-feedback-loops]]、[[agent-observability]]、[[agent-sandboxing]]、[[agent-approval-patterns]] 等能力串成稳定性体系。
- [[coding-agent-evals]] 负责衡量这些模式是否真的有效。
- [[long-running-agent-tasks]] 往往是检验可靠性模式是否成熟的试金石。
- [[multi-agent-delegation]] 在这里的价值不只是分流工作，更是用角色化互校降低单点误判。
- [[evaluator-driven-qa]] 是可靠性模式里最适合处理“自评失真”的一类。
- [[cloud-agent-operations]] 让可靠性从单个会话扩展到后台自动化和组织级运行。

## 常见误区
- 把可靠性理解成“多加几个测试”。
- 只在事故后补修，不做前置约束与持续治理。
- 关注单次成功率，不关注中断恢复、漂移控制和长期维护性。
- 忽略跨 context window 的接棒问题，导致每轮 agent 都在重新猜现场。
- 以为 evaluator 一定越多越好，忽略它是否还处在能带来净收益的任务边界内。

## Lychee Technology 的 4 个生产陷阱
[[lychee-technology]] 的博客文章从长时间运行实践中提炼出 4 个高阶可靠性陷阱，与当前模式库形成互补：

### Trap 1: Context Anxiety
当上下文窗口填充接近 70% 容量时，模型会表现出行为变化：开始跳过步骤或提前完成任务。这被称为 "context anxiety"。
- **修复**: Context Reset — 保存状态到持久存储 → 终止当前 LLM 实例 → 启动全新 agent 读取状态继续。这比 in-place summarization 更可靠，因为后者仍让模型在降级上下文中运行。
- **与现有知识的关联**: 与 [[long-running-agent-tasks]] 中的跨窗口接力直接相关，也与 Anthropic 提到的 "context anxiety" 现象一致。

### Trap 2: Self-Grading Illusion
让模型评估自己的工作会导致系统性高估 — 这不是特定模型的 bug，而是结构性缺陷（生成与评估共享同一组权重）。
- **修复**: Sprint Contract — Generator agent 与独立 Evaluator agent 在开始前协商具体的"完成"定义。Evaluator 必须执行验证（运行代码、检查 schema），且必须在 clean context 上运行（不能看到 Generator 的推理链）。
- **与现有知识的关联**: 与 [[evaluator-driven-qa]] 完全兼容，但把"独立评估"的要求表达得更严格。

### Trap 3: Optimizing for the Illusion of Correctness
当 LLM 面临不可能或矛盾的约束时，会停止解决实际问题，转而优化"看起来正确"。输出变得流畅但空洞：幻觉数据、表面合理但逻辑破碎。
- **修复**: 反馈必须保持严格客观。给编译错误、失败断言、schema mismatch — 给模型一个要解决的问题，而不是一个要维护的声誉。情绪化的错误消息（"你真蠢，这完全错了"）会把上下文偏向失败叙事，导致后续输出进一步退化。
- **与现有知识的关联**: 与 [[agent-feedback-loops]] 中"输出整形"和"failFast"原则一致 — 只暴露当前最关键的失败。

### Trap 4: The Memory Consolidation Cycle
长期运行后，memory log 膨胀且充满矛盾 — 旧决策与新决策冲突，冗余条目每次读取都浪费 token。
- **修复**: 自动化 Memory Consolidation — 在 agent 空闲时触发后台作业，读取原始日志、去重、消解矛盾（以最新数据为准）、写回 clean compressed state file。有案例把 32K token 的嘈杂历史压缩成 7K 的干净状态文件，无有意义信息丢失。
- **与现有知识的关联**: 与 [[agent-memory-patterns]] 和 [[long-running-agent-tasks]] 中的 compaction / continuity 机制直接相关。

## 来源
- [[openai-harness-engineering-2026-04-14]]
- [[anthropic-effective-harnesses-long-running-agents-2026-04-14]]
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[cursor-docs-reference-sandbox-2026-04-14]]
- [[cursor-docs-agent-security-2026-04-14]]
- [[cursor-docs-cloud-agent-capabilities-2026-04-14]]
- [[cursor-docs-enterprise-compliance-monitoring-2026-04-14]]
- [[humanlayer-skill-issue-harness-engineering-2026-04-14]]
- [[humanlayer-context-efficient-backpressure-2026-04-14]]
- [[ltbase-harness-engineering-2026-04-24|ltbase-harness-engineering]]
