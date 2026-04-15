---
title: Entangled Software
created: 2026-04-15
updated: 2026-04-15
type: concept
tags: [concept, agentic-engineering, workflow, harness-engineering, best-practice]
sources: [raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md]
---

# Entangled Software

## 定义
entangled software 是 João Moura 提出的一个判断框架：当构建软件和 agent 的成本持续坍缩后，真正的竞争点不再只是“谁把工具链做得更完整”，而是产品能否随着客户的真实工作方式持续适配，并与客户的流程、数据和使用模式形成双向塑形关系。

## 为什么它重要
这套说法本质上是在重估 agent 时代的软件防御层。过去很多讨论停留在 framework、scaffold、harness 这些 building layer 名词上，但 João 的核心观点是：这些层都会越来越便宜，甚至被 provider API 吸收。真正难复制的，是客户长期使用后沉淀出的模式、数据、信任和适配能力。

## 这条帖子补出的关键判断
- harness 会像 framework 一样快速 commodity 化。
- planning、memory、file systems、compaction 等今天被视作“更厚的 harness”能力，未来也可能继续下沉为更通用 primitive。
- 企业之所以想自己用 AI 重做内部工具，不只是因为便宜，而是因为他们实际只用 SaaS 的一小部分，而且每个组织都已经在脑中形成了自己的 workflow 变体。
- 真正更强的产品，不是逼客户适应工具，而是让工具适应客户行为。
- 当 agentic system 真正嵌进客户流程、数据与工作模式后，会出现 entangled agentic systems：它们的 intelligence 来自持续使用，而不是初始配置。

## 它在当前知识库里的价值
[[entangled-software]] 不是在否定 [[harness-engineering]]，而是在给它划边界：
- harness 仍然重要，但更像 plumbing
- customer-specific adaptation 才可能成为更长期的产品护城河

所以它和当前库里几条线能自然接上：
- 它延续了 [[agent-memory-patterns]] 里的 usage flywheel / memory ownership 逻辑，但把重点从“谁拥有记忆”推进到“产品是否随使用持续重塑自己”。
- 它扩展了 [[agentic-engineering]]：不只是让 agent 成为 actor，而是让 agent system 逐步吸收组织的真实工作模式。
- 它也给 [[harness-engineering]] 提了一个反身性问题：如果 harness 越来越薄，那么系统的长期价值该沉到哪一层？

## 我的阶段性判断
我觉得这条概念有价值，但要分开看：
- 作为方向判断，它很强：确实把 agent 产品竞争从“工具更全”推向“适配更深”。
- 作为已被证明的成熟范式，它还偏早：目前更像平台叙事与产品战略判断，不是已经被普遍验证的工程定律。

所以更稳的用法是：把 [[entangled-software]] 当成一个上层产品/平台判断框架，而不是拿它替代底层的 harness、context、memory 设计工作。

## 关联
- [[crewai]] 是这条概念的提出方之一。
- [[harness-engineering]] 提供它试图超越的 building layer 背景。
- [[agentic-engineering]] 是它落到组织级工作流时的直接入口。
- [[agent-memory-patterns]] 帮助理解“持续适配”为什么离不开记忆与 usage flywheel。

## 来源
- [[joao-moura-x-post-2043726271449112776-2026-04-15]]
