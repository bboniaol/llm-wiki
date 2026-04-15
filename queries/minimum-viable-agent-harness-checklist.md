---
title: Minimum Viable Agent Harness Checklist
created: 2026-04-15
updated: 2026-04-15
type: query
tags: [query-note, harness-engineering, workflow, best-practice, reliability, infrastructure]
sources: [raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md, raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md, raw/articles/letta-context-constitution-blog-2026-04-15.md, raw/articles/letta-context-constitution-constitution-md-2026-04-15.md, raw/articles/karan-x-post-2043618895328932340-2026-04-15.md]
---

# Minimum Viable Agent Harness Checklist

## 问题
如果现在不追求“最强平台”，只想先搭出一套最小可用、能稳定工作的 agent harness，最少该具备哪些能力？

## 短答案
基于 [[harness-engineering]]、[[evaluator-driven-qa]]、[[agent-memory-patterns]]、[[agent-readable-repositories]]、[[context-engineering]] 与 [[progressive-disclosure]]，一个 minimum viable agent harness 至少该过 6 个检查点：

1. 有独立评估/批判环
2. 有可续接的会话与状态层
3. 有最小可用的 context management
4. 有 markdown / repo 级外部记忆载体
5. 有基础 guardrails
6. 有 follow-up continuity

少一两项不是完全不能跑，但会很容易退化成“单轮 demo 工具”，而不是可持续系统。

## 一张最小清单

### 1. 独立评估 / critic-in-loop
最小要求：
- 不让生成 agent 完全自己给自己打分
- 至少有一层结构化批判、验收或 judge 机制

为什么：
- Anthropic 这条线说明 generator 自评经常不可靠
- Karan 的实现帖则给了一个更轻量版本：`LLM as Judge` / critic-in-loop 也能先顶上一层

没这一项时常见症状：
- 输出“看起来完成了”，但细看问题一堆
- 幻觉和格式错漏没人拦

对应页面：
- [[evaluator-driven-qa]]
- [[agent-feedback-loops]]

### 2. 可续接的会话 / 状态层
最小要求：
- follow-up 不是开新生命，而是能接上已有 session
- history、memory、latest result 至少有一套可回收机制

为什么：
- 没状态续接，agent 每轮都像失忆
- Karan 这条帖子把这件事压得很实：CLI 侧 SQLite、UI 侧 Redis，也是一种够用的最小实现

没这一项时常见症状：
- 一追问就重开上下文
- 多轮任务越做越飘
- 需要人类反复重新解释现场

对应页面：
- [[agent-memory-patterns]]
- [[long-running-agent-tasks]]

### 3. 最小可用的 context management
最小要求：
- 有 compaction / summarization / snapshot 思路
- 不把所有上下文硬塞进主线程
- 至少会注入 repo snapshot、workspace preference 或等价高信号上下文

为什么：
- [[context-engineering]] 的底线就是：给最小但高信号的上下文
- Letta 则把它进一步上升成正式原则：context window 与 external context 要分层治理

没这一项时常见症状：
- agent 初期聪明，后期崩溃
- token 用得很多，结果越来越差
- follow-up 时无法快速找回关键状态

对应页面：
- [[context-engineering]]
- [[context-constitution]]

### 4. markdown / repo 级外部记忆载体
最小要求：
- 不把所有知识都寄托在聊天记录
- 至少有一类人和 agent 都能读写的外部记忆工件
- 最小可用形态通常就是 `.md` / `README` / `AGENTS.md`

为什么：
- Sarah Wooders 把 memory 说成 harness 内部的 context governance
- Karan 这条帖则给了很直白的落地点：`.md` files are the new brain for agents

没这一项时常见症状：
- 经验不沉淀
- 新会话只能靠历史聊天捞状态
- 规则不可迁移、不可审计、不可复用

对应页面：
- [[agent-readable-repositories]]
- [[agent-memory-patterns]]

### 5. 基础 guardrails
最小要求：
- 至少明确哪些敏感信息不能被随便带进输出
- 对 credentials / API keys / 高风险操作有最小保护

为什么：
- 没有 guardrails，agent 越能干，事故越大
- Karan 这条帖虽然薄，但很对路：最先该拦的就是代码库里的 internal API keys / credentials

没这一项时常见症状：
- 输出泄密
- 工具越权
- 自动化刚起量就出安全事故

对应页面：
- [[agent-sandboxing]]
- [[agent-approval-patterns]]

### 6. follow-up continuity
最小要求：
- 用户回来追问时，系统能延续前次工作，而不是只保留静态聊天记录
- 新一轮能读到“当前状态 + 最近结果 + 记忆边界”

为什么：
- 这决定系统到底是“会话机器人”还是“长期协作者”
- Letta 这条线强调 continuity，Karan 这条线强调 existing session reload，本质上都在说同一件事

没这一项时常见症状：
- 只能做一次性任务
- 复杂任务切不到多轮
- 用户越用越觉得系统不长记性

对应页面：
- [[context-constitution]]
- [[agent-memory-patterns]]

## 最小版本，不等于简陋版本
一个 minimum viable harness 不需要一上来就有：
- 完整云端平台
- 复杂多 agent 编排
- 全套企业治理面
- 大而全的 memory system

但它必须能过下面这条底线：
- 能接住上下文
- 能接住状态
- 能接住反馈
- 能接住风险

如果这四件事接不住，那大概率还停留在“单轮 prompt automation”，不算真正的 harness。

## 一张更实用的落地顺序
如果你现在从 0 到 1，我建议按这个顺序搭：

1. 先加 critic / judge
2. 再补 session continuity
3. 再补 markdown brains / repo memory
4. 再补 compaction 与 context snapshot
5. 再补 guardrails
6. 最后再考虑更重的 orchestration / background runtime

原因很简单：
- 先把“会胡说、会失忆、会断线”这三类最常见失败模式压住
- 再往上做平台化，性价比更高

## 结论
如果让我把 minimum viable agent harness 压成一句话，我会这么说：

它至少要让 agent：
- 被评估
- 能续接
- 会压缩
- 有外部脑
- 不乱泄密
- 多轮不失忆

再少，就更像 demo。
再多，才开始接近平台。

## 关联页面
- [[harness-engineering]]
- [[evaluator-driven-qa]]
- [[agent-memory-patterns]]
- [[agent-readable-repositories]]
- [[context-engineering]]
- [[progressive-disclosure]]
- [[context-constitution]]

## 来源
- [[anthropic-harness-design-long-running-apps-2026-04-14]]
- [[sarah-wooders-x-post-2040121230473457921-2026-04-15]]
- [[letta-context-constitution-blog-2026-04-15]]
- [[letta-context-constitution-constitution-md-2026-04-15]]
- [[karan-x-post-2043618895328932340-2026-04-15]]
