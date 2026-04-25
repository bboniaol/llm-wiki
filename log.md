# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to log-YYYY.md, start fresh.

## [2026-04-14] create | Wiki initialized
- Domain: AI 圈 Harness Engineering 学习知识库
- Structure created with SCHEMA.md, index.md, log.md
- Directories created: raw/articles, raw/papers, raw/transcripts, raw/assets, entities, concepts, comparisons, queries

## [2026-04-14] ingest | 工程技术：在智能体优先的世界中利用 Codex
- Source URL: https://openai.com/zh-Hans-CN/index/harness-engineering/
- Raw source saved: raw/articles/openai-harness-engineering-2026-04-14.md
- Direct fetch returned 403; ingested via r.jina.ai mirror fallback
- Created: entities/openai.md
- Created: entities/codex.md
- Created: concepts/harness-engineering.md
- Created: concepts/agent-readable-repositories.md
- Updated: index.md

## [2026-04-14] update | 补充基础概念骨架
- Created: concepts/context-engineering.md
- Created: concepts/agentic-engineering.md
- Created: comparisons/harness-vs-context-vs-agentic-engineering.md
- Updated: index.md

## [2026-04-14] update | 补充工程层概念
- Created: concepts/agent-feedback-loops.md
- Created: concepts/coding-agent-evals.md
- Created: concepts/agent-observability.md
- Updated: index.md

## [2026-04-14] update | 补充控制层概念
- Created: concepts/agent-approval-patterns.md
- Created: concepts/agent-sandboxing.md
- Created: concepts/repo-as-system-of-record.md
- Updated: index.md

## [2026-04-14] update | 补充实践层页面
- Created: concepts/coding-agent-workflow-patterns.md
- Created: concepts/doc-gardening-agents.md
- Created: comparisons/approval-vs-sandbox-vs-observability.md
- Updated: index.md

## [2026-04-14] update | 补充工程专题页
- Created: concepts/long-running-agent-tasks.md
- Created: concepts/agent-memory-patterns.md
- Created: concepts/multi-agent-delegation.md
- Created: concepts/agent-reliability-patterns.md
- Created: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] update | 补充 Claude Code 与 Cursor 实体资料
- Raw source saved: raw/articles/anthropic-claude-code-2026-04-14.md
- Raw source saved: raw/articles/cursor-product-2026-04-14.md
- Created: entities/claude-code.md
- Created: entities/cursor.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] ingest | Claude Code 与 Cursor 文档层
- Raw source saved: raw/articles/claude-code-docs-overview-2026-04-14.md
- Raw source saved: raw/articles/claude-code-auto-mode-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-subagents-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-rules-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-mcp-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-terminal-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-agent-overview-2026-04-14.md
- Updated: entities/claude-code.md
- Updated: entities/cursor.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] ingest | Effective harnesses for long-running agents
- Source URL: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Raw source saved: raw/articles/anthropic-effective-harnesses-long-running-agents-2026-04-14.md
- Updated: concepts/long-running-agent-tasks.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agent-approval-patterns.md
- Updated: concepts/agent-reliability-patterns.md
- Created: entities/anthropic.md
- Updated: entities/claude-code.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] ingest | Claude Code 深挖文档层
- Raw source saved: raw/articles/claude-code-docs-permission-modes-2026-04-14.md
- Raw source saved: raw/articles/claude-code-docs-memory-2026-04-14.md
- Raw source saved: raw/articles/claude-code-docs-sub-agents-2026-04-14.md
- Raw source saved: raw/articles/claude-code-docs-common-workflows-2026-04-14.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/coding-agent-workflow-patterns.md
- Updated: concepts/multi-agent-delegation.md
- Updated: entities/claude-code.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md


## [2026-04-14] ingest | Harness design for long-running application development
- Source URL: https://www.anthropic.com/engineering/harness-design-long-running-apps
- Raw source saved: raw/articles/anthropic-harness-design-long-running-apps-2026-04-14.md
- Updated: concepts/long-running-agent-tasks.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agent-feedback-loops.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: concepts/multi-agent-delegation.md
- Updated: entities/anthropic.md
- Updated: entities/claude-code.md
- Updated: index.md

## [2026-04-14] ingest | Effective context engineering for AI agents
- Source URL: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Raw source saved: raw/articles/anthropic-effective-context-engineering-2026-04-14.md
- Updated: concepts/context-engineering.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/multi-agent-delegation.md
- Updated: comparisons/harness-vs-context-vs-agentic-engineering.md
- Updated: entities/anthropic.md

## [2026-04-14] update | 补充 evaluator-driven QA 概念页
- Created: concepts/evaluator-driven-qa.md
- Updated: concepts/agent-feedback-loops.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: index.md

## [2026-04-14] ingest | Cursor 控制面与浏览器工具深挖
- Raw source saved: raw/articles/cursor-docs-reference-permissions-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-reference-sandbox-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-browser-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-agent-security-2026-04-14.md
- Updated: entities/cursor.md
- Updated: concepts/agent-sandboxing.md
- Updated: concepts/agent-approval-patterns.md
- Updated: concepts/coding-agent-workflow-patterns.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] update | 补充评估与人工审查对比页
- Created: comparisons/evaluator-driven-qa-vs-human-in-the-loop-review.md
- Updated: index.md

## [2026-04-14] ingest | Cursor cloud agents / automations / enterprise controls
- Raw source saved: raw/articles/cursor-docs-cloud-agent-overview-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-cloud-agent-automations-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-cloud-agent-capabilities-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-enterprise-llm-safety-controls-2026-04-14.md
- Raw source saved: raw/articles/cursor-docs-enterprise-compliance-monitoring-2026-04-14.md
- Created: concepts/cloud-agent-operations.md
- Updated: entities/cursor.md
- Updated: concepts/agent-observability.md
- Updated: concepts/agent-sandboxing.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: concepts/coding-agent-workflow-patterns.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] update | 补充本地控制与云端控制对比页
- Created: comparisons/local-agent-controls-vs-cloud-agent-controls.md
- Updated: index.md

## [2026-04-14] ingest | The Anatomy of an Agent Harness
- Source URL: https://blog.langchain.com/the-anatomy-of-an-agent-harness/
- Raw source saved: raw/articles/langchain-anatomy-of-an-agent-harness-2026-04-14.md
- Created: entities/langchain.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agent-readable-repositories.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/agent-sandboxing.md
- Updated: concepts/long-running-agent-tasks.md
- Updated: comparisons/harness-vs-context-vs-agentic-engineering.md
- Updated: index.md

## [2026-04-14] ingest | Deep Agents overview
- Source URL: https://docs.langchain.com/oss/python/deepagents/overview
- Raw source saved: raw/articles/langchain-deepagents-overview-2026-04-14.md
- Created: entities/deepagents.md
- Updated: entities/langchain.md
- Updated: concepts/multi-agent-delegation.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/agent-approval-patterns.md
- Updated: index.md

## [2026-04-14] ingest | Deep Agents backends / sandboxes / permissions / HITL
- Source URL: https://docs.langchain.com/oss/python/deepagents/overview
- Raw source saved: raw/articles/langchain-deepagents-overview-2026-04-14.md
- Created: concepts/pluggable-agent-backends.md
- Updated: entities/deepagents.md
- Updated: entities/langchain.md
- Updated: concepts/multi-agent-delegation.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/agent-approval-patterns.md
- Updated: index.md

## [2026-04-14] update | 补充 framework / runtime / harness 对比页
- Created: comparisons/framework-vs-runtime-vs-harness.md
- Updated: index.md

## [2026-04-14] ingest | Money Forward brings Cursor's coding agents to product, design, and QA
- Source URL: https://cursor.com/blog/money-forward
- Raw source saved: raw/articles/cursor-money-forward-case-study-2026-04-14.md
- Created: entities/money-forward.md
- Updated: entities/cursor.md
- Updated: concepts/coding-agent-workflow-patterns.md
- Updated: concepts/agentic-engineering.md
- Updated: concepts/cloud-agent-operations.md
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md
- Updated: index.md

## [2026-04-14] ingest | How Sentry built end-to-end bug fixing with Claude Managed Agents
- Source URL: https://claude.com/customers/sentry
- Raw source saved: raw/articles/anthropic-sentry-managed-agents-case-study-2026-04-14.md
- Created: entities/sentry.md
- Created: entities/claude-managed-agents.md
- Updated: entities/anthropic.md
- Updated: concepts/cloud-agent-operations.md
- Updated: concepts/agentic-engineering.md
- Updated: index.md

## [2026-04-14] ingest | CircleCI customer story with Claude
- Source URL: https://claude.com/customers/circleci
- Raw source saved: raw/articles/anthropic-circleci-claude-case-study-2026-04-14.md
- Created: entities/circleci.md
- Updated: entities/claude-code.md
- Updated: entities/anthropic.md
- Updated: concepts/coding-agent-workflow-patterns.md
- Updated: index.md

## [2026-04-14] ingest | Skill Issue: Harness engineering for coding agents
- Source URL: https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents
- Raw source saved: raw/articles/humanlayer-skill-issue-harness-engineering-2026-04-14.md
- Ingested via r.jina.ai mirror
- Created: entities/humanlayer.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/context-engineering.md
- Updated: concepts/multi-agent-delegation.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: index.md

## [2026-04-14] ingest | HumanLayer 配套文章：CLAUDE.md / advanced context engineering / context-efficient backpressure
- Raw source saved: raw/articles/humanlayer-writing-a-good-claude-md-2026-04-14.md
- Raw source saved: raw/articles/humanlayer-advanced-context-engineering-2026-04-14.md
- Raw source saved: raw/articles/humanlayer-context-efficient-backpressure-2026-04-14.md
- Ingested via r.jina.ai mirror
- Created: concepts/progressive-disclosure.md
- Updated: entities/humanlayer.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/context-engineering.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/long-running-agent-tasks.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: index.md

## [2026-04-14] ingest | Your agent needs a harness, not a framework
- Source URL: https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework
- Raw source saved: raw/articles/inngest-harness-not-framework-2026-04-14.md
- Ingested via r.jina.ai mirror
- Created: entities/inngest.md
- Updated: concepts/harness-engineering.md
- Updated: comparisons/framework-vs-runtime-vs-harness.md
- Updated: concepts/multi-agent-delegation.md
- Updated: concepts/long-running-agent-tasks.md
- Updated: index.md

## [2026-04-14] update | 补充 in-process harness 与 event-driven harness 对比页
- Created: comparisons/in-process-harness-vs-event-driven-harness.md
- Updated: entities/humanlayer.md
- Updated: entities/inngest.md
- Updated: index.md

## [2026-04-14] update | 补充 deterministic backpressure 与 durable retries 对比页
- Created: comparisons/deterministic-backpressure-vs-durable-retries.md
- Updated: entities/humanlayer.md
- Updated: entities/inngest.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Reliability Stack
- Filed: queries/coding-agent-reliability-stack.md
- Updated: concepts/agent-reliability-patterns.md
- Updated: concepts/harness-engineering.md
- Updated: index.md

## [2026-04-14] lint | 8 issues found
- Fixed: added missing tags `open-source` and `documentation` to SCHEMA.md taxonomy
- Fixed: added inbound links for comparisons/approval-vs-sandbox-vs-observability.md
- Fixed: added inbound links for comparisons/evaluator-driven-qa-vs-human-in-the-loop-review.md
- Fixed: added inbound links for comparisons/local-agent-controls-vs-cloud-agent-controls.md
- Updated: concepts/agent-approval-patterns.md
- Updated: concepts/agent-sandboxing.md
- Updated: concepts/evaluator-driven-qa.md
- Updated: concepts/cloud-agent-operations.md
- Updated: SCHEMA.md

## [2026-04-14] query | From Local Coding Agent to Team Agent Platform
- Filed: queries/from-local-coding-agent-to-team-agent-platform.md
- Updated: queries/coding-agent-reliability-stack.md
- Updated: concepts/cloud-agent-operations.md
- Updated: index.md

## [2026-04-14] ingest | WolfBench X post on Hermes Agent benchmark result
- Source URL: https://x.com/wandb/status/2039797885982953800
- Raw source saved: raw/articles/wolfbench-hermes-agent-x-post-2026-04-14.md
- Ingested via r.jina.ai mirror
- Created: entities/hermes-agent.md
- Created: entities/wolfbench.md
- Updated: concepts/coding-agent-evals.md
- Updated: concepts/harness-engineering.md
- Updated: index.md

## [2026-04-14] ingest | WolfBench site overview
- Source URL: https://wolfbench.ai/
- Raw source saved: raw/articles/wolfbench-site-overview-2026-04-14.md
- Ingested via r.jina.ai mirror
- Updated: entities/wolfbench.md
- Updated: entities/hermes-agent.md
- Updated: concepts/coding-agent-evals.md

## [2026-04-14] ingest | WolfBench GitHub repo overview
- Source URL: https://github.com/wandb/WolfBench
- Raw source saved: raw/articles/wolfbench-github-repo-overview-2026-04-14.md
- Ingested via r.jina.ai mirror
- Updated: entities/wolfbench.md
- Updated: entities/hermes-agent.md
- Updated: concepts/coding-agent-evals.md

## [2026-04-14] query | How to Read Agent Harness Benchmarks
- Filed: queries/how-to-read-agent-harness-benchmarks.md
- Updated: concepts/coding-agent-evals.md
- Updated: entities/wolfbench.md
- Updated: index.md

## [2026-04-14] query | Social Benchmark and Product Signals (2026-04-14)
- Filed: queries/social-benchmark-and-product-signals-2026-04-14.md
- Updated: index.md
- Note: 12 social posts fetched successfully in this batch; remaining URLs need follow-up fetch attempts due flaky X extraction

## [2026-04-14] ingest | X social signals follow-up batch
- Raw source saved: raw/articles/pawel-huryn-x-post-2042008828334764162-2026-04-14.md
- Raw source saved: raw/articles/ramp-labs-x-post-2042660310851449223-2026-04-14.md
- Raw source saved: raw/articles/rohit-x-post-2041548810804211936-2026-04-14.md
- Raw source saved: raw/articles/gabe-pereyra-x-post-2041568552256197074-2026-04-14.md
- Raw source saved: raw/articles/gabe-pereyra-x-post-2041167397453758863-2026-04-14.md
- Raw source saved: raw/articles/harrison-chase-x-post-2042612328701812789-2026-04-14.md
- Raw source saved: raw/articles/harrison-chase-x-post-2042978845347745871-2026-04-14.md
- Raw source saved: raw/articles/viv-x-post-2041927488918413589-2026-04-14.md
- Raw source saved: raw/articles/alexz-x-post-2041951380836147479-2026-04-14.md
- Raw source saved: raw/articles/claude-x-post-2041927687460024721-2026-04-14.md
- Raw source saved: raw/articles/guru-x-post-2042450832126591251-2026-04-14.md
- Updated: queries/social-benchmark-and-product-signals-2026-04-14.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/cloud-agent-operations.md
- Updated: concepts/agent-memory-patterns.md
- Updated: entities/claude-managed-agents.md
- Updated: index.md

## [2026-04-14] query | Managed Harness vs Open Harness
- Filed: queries/managed-harness-vs-open-harness.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Adoption Patterns
- Filed: queries/coding-agent-adoption-patterns.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Org Design Patterns
- Filed: queries/coding-agent-org-design-patterns.md
- Updated: queries/coding-agent-adoption-patterns.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Governance Checklist
- Filed: queries/coding-agent-governance-checklist.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Maturity Model
- Filed: queries/coding-agent-maturity-model.md
- Updated: index.md

## [2026-04-14] query | Coding Agent Platform Readiness Audit
- Filed: queries/coding-agent-platform-readiness-audit.md
- Updated: index.md

## [2026-04-14] query | Cursor Platform Readiness Audit
- Filed: queries/cursor-platform-readiness-audit.md
- Updated: index.md

## [2026-04-14] query | Claude Managed Agents Platform Readiness Audit
- Filed: queries/claude-managed-agents-platform-readiness-audit.md
- Updated: index.md

## [2026-04-14] update | Cursor vs Claude Managed Agents platform readiness comparison
- Created: comparisons/cursor-vs-claude-managed-agents-platform-readiness.md
- Updated: index.md

## [2026-04-14] query | Deep Agents Platform Readiness Audit
- Filed: queries/deepagents-platform-readiness-audit.md
- Updated: index.md

## [2026-04-14] query | Three platform archetypes for coding agents
- Filed: queries/three-platform-archetypes-for-coding-agents.md
- Updated: index.md

## [2026-04-15] ingest | Harrison Chase "Your harness, your memory"
- Source URL: https://x.com/hwchase17/status/2042978500567609738
- Raw source saved: raw/articles/harrison-chase-x-post-2042978500567609738-2026-04-15.md
- Updated: concepts/agent-memory-patterns.md
- Updated: queries/managed-harness-vs-open-harness.md
- Updated: entities/deepagents.md
- Updated: entities/langchain.md
- Updated: index.md

## [2026-04-15] ingest | Sarah Wooders "Why memory isn't a plugin (it's the harness)"
- Source URL: https://x.com/sarahwooders/status/2040121230473457921
- Raw source saved: raw/articles/sarah-wooders-x-post-2040121230473457921-2026-04-15.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agent-readable-repositories.md

## [2026-04-15] ingest | Letta Context Constitution
- Source URL: https://www.letta.com/blog/context-constitution
- Raw source saved: raw/articles/letta-context-constitution-blog-2026-04-15.md
- Raw source saved: raw/articles/letta-context-constitution-constitution-md-2026-04-15.md
- Created: entities/letta.md
- Created: concepts/context-constitution.md
- Updated: concepts/context-engineering.md
- Updated: concepts/progressive-disclosure.md
- Updated: concepts/agent-memory-patterns.md
- Updated: index.md

## [2026-04-15] ingest | João Moura "Agent Harnesses Are Dead. Long Live Agent Harnesses."
- Source URL: https://x.com/joaomdmoura/status/2043726271449112776
- Raw source saved: raw/articles/joao-moura-x-post-2043726271449112776-2026-04-15.md
- Created: entities/crewai.md
- Created: concepts/entangled-software.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agentic-engineering.md
- Updated: index.md

## [2026-04-15] ingest | Karan "Agent Harness is the new system design in 2026"
- Source URL: https://x.com/kmeanskaran/status/2043618895328932340
- Raw source saved: raw/articles/karan-x-post-2043618895328932340-2026-04-15.md
- Created: entities/desysflow.md
- Updated: concepts/evaluator-driven-qa.md
- Updated: concepts/agent-memory-patterns.md
- Updated: concepts/agent-readable-repositories.md
- Updated: concepts/harness-engineering.md
- Updated: index.md

## [2026-04-15] query | Minimum Viable Agent Harness Checklist
- Filed: queries/minimum-viable-agent-harness-checklist.md
- Updated: index.md

## [2026-04-15] update | Social Benchmark and Product Signals (2026-04-14)
- Updated: queries/social-benchmark-and-product-signals-2026-04-14.md

## [2026-04-15] ingest | Natural-Language Agent Harnesses (NLAH) paper deep dive
- Source URL: https://arxiv.org/abs/2603.25723
- Raw source saved: raw/articles/nlah-arxiv-abs-2603-25723-2026-04-15.md
- Raw source saved: raw/articles/nlah-arxiv-html-2603-25723-2026-04-15.md
- Created: concepts/natural-language-agent-harnesses.md
- Created: concepts/intelligent-harness-runtime.md
- Updated: concepts/harness-engineering.md
- Updated: concepts/agent-readable-repositories.md
- Updated: queries/social-benchmark-and-product-signals-2026-04-14.md
- Updated: index.md

## [2026-04-15] query | What NLAH RQ2 and RQ3 Actually Show
- Filed: queries/what-nlah-rq2-rq3-actually-show.md
- Updated: index.md

## [2026-04-15] ingest | Extreme Harness Engineering / Frontier / Symphony
- Source URL: https://latent.space/p/harness-eng
- Raw source saved: raw/articles/latent-space-extreme-harness-engineering-2026-04-15.md
- Raw source saved: raw/articles/openai-frontier-overview-2026-04-15.md
- Raw source saved: raw/articles/openai-symphony-spec-2026-04-15.md
- Created: entities/openai-frontier.md
- Created: entities/symphony.md
- Filed: queries/extreme-harness-engineering.md
- Updated: concepts/cloud-agent-operations.md
- Updated: entities/openai.md
- Updated: entities/codex.md
- Updated: index.md

## [2026-04-15] query | Harness Engineering System Map
- Filed: queries/harness-engineering-system-map.md
- Updated: index.md

## [2026-04-15] query | Harness Engineering 7-Day Study Plan
- Filed: queries/harness-engineering-7-day-study-plan.md
- Updated: index.md


## [2026-04-16] ingest | X signals for harness engineering (Cursor / Cognition / LangChain)
- Source URL: https://x.com/cursor_ai/status/2044136953239740909
- Source URL: https://x.com/cognition/status/2044174496312242544
- Source URL: https://cognition.ai/blog/swe-check-10x-faster
- Source URL: https://x.com/LangChain/status/2044429013301485916
- Source URL: https://www.langchain.com/conceptual-guides/traces-start-agent-improvement-loop
- Raw source saved: raw/articles/cursor-x-post-2044136953239740909-2026-04-16.md
- Raw source saved: raw/articles/cognition-x-post-2044174496312242544-2026-04-16.md
- Raw source saved: raw/articles/cognition-swe-check-10x-faster-2026-04-16.md
- Raw source saved: raw/articles/langchain-x-post-2044429013301485916-2026-04-16.md
- Raw source saved: raw/articles/langchain-agent-improvement-loop-2026-04-16.md
- Created: entities/cognition.md
- Created: queries/harness-engineering-signals-2026-04-16.md
- Updated: concepts/coding-agent-evals.md
- Updated: concepts/agent-feedback-loops.md
- Updated: concepts/agent-observability.md
- Updated: entities/langchain.md
- Updated: entities/cursor.md
- Updated: index.md

## [2026-04-16] query | Harness Engineering Signals (2026-04-16)
- Filed: queries/harness-engineering-signals-2026-04-16.md
- Updated: index.md

## [2026-04-16] ingest | From offline benchmark to online evals
- Source URL: https://docs.langchain.com/langsmith/evaluation
- Source URL: https://www.braintrust.dev/docs/evaluate/score-online
- Source URL: https://langfuse.com/docs/evaluation/overview
- Source URL: https://arize.com/docs/phoenix/evaluation/llm-evals
- Source URL: https://docs.coderabbit.ai/
- Source URL: https://www.meticulous.ai/
- Raw source saved: raw/articles/langsmith-evaluation-overview-2026-04-16.md
- Raw source saved: raw/articles/braintrust-score-production-traces-2026-04-16.md
- Raw source saved: raw/articles/langfuse-evaluation-overview-2026-04-16.md
- Raw source saved: raw/articles/phoenix-evaluation-overview-2026-04-16.md
- Raw source saved: raw/articles/coderabbit-docs-overview-2026-04-16.md
- Raw source saved: raw/articles/meticulous-product-overview-2026-04-16.md
- Filed: queries/from-offline-benchmark-to-online-evals.md
- Updated: concepts/coding-agent-evals.md
- Updated: concepts/agent-feedback-loops.md
- Updated: concepts/agent-observability.md
- Updated: concepts/evaluator-driven-qa.md
- Updated: index.md

## [2026-04-18] query | Harness Engineering Signals (2026-04-18)
- Filed: queries/harness-engineering-signals-2026-04-18.md
- Updated: concepts/harness-engineering.md
- Updated: entities/cognition.md
- Updated: index.md
## [2026-04-19] query | Harness Engineering Signals (2026-04-19)
- Official x-cli preflight failed: Missing env var X_API_KEY; used existing recovered X/raw-source signals in /Users/gaara/wiki rather than write-capable API.
- Filed: queries/harness-engineering-signals-2026-04-19.md
- Updated: entities/langchain.md
- Updated: concepts/harness-engineering.md
- Updated: index.md
- Raw sources reused: raw/articles/langchain-x-post-2044429013301485916-2026-04-16.md, raw/articles/langchain-agent-improvement-loop-2026-04-16.md, raw/articles/cognition-x-post-2044174496312242544-2026-04-16.md, raw/articles/cognition-swe-check-10x-faster-2026-04-16.md, raw/articles/cursor-x-post-2044136953239740909-2026-04-16.md

## [2026-04-24] ingest | Anthropic Eric: Vibe Coding 生产环境安全策略
- Source: X video post by @billtheinvestor (https://x.com/billtheinvestor/status/2046269200520577262)
- Video: 31 min, Anthropic Coding Agents 研究负责人 Eric 演讲
- Raw saved: /tmp/vibe_coding_anthropic.mp4 + /tmp/vibe_coding_anthropic.txt (transcript via Whisper)
- Created: concepts/vibe-coding-production-safety.md (7 sections, 200+ lines)
- Updated: index.md (total pages: 78)
- Key concepts: 叶节点/核心架构分层、可验证性设计、TDD 技巧、Claude Code + Cursor 组合、指数增长论

## [2026-04-24] ingest | Lychee Technology: Harness Engineering (7-Layer Stack)
- Source URL: https://blog.ltbase.dev/posts/agents/harness-engineering
- Direct fetch blocked (private network); ingested via browser extraction
- Raw saved: raw/articles/ltbase-harness-engineering-2026-04-24.md
- Created: entities/lychee-technology.md
- Updated: concepts/harness-engineering.md (added 7-layer stack mapping, 4 design principles, 4 production traps, MVH recommendation)
- Updated: concepts/agent-reliability-patterns.md (added 4 frontline traps: Context Anxiety, Self-Grading Illusion, Illusion of Correctness, Memory Consolidation Cycle)
- Updated: concepts/coding-agent-workflow-patterns.md (added layered harness full agent run example)
- Updated: index.md (total pages: 79)
- Key contribution: structured 7-layer framework + 4 design principles + 4 production traps as complementary methodology to existing OpenAI/Anthropic/LangChain sources

## [2026-04-24] ingest | Lychee Technology: Harness Engineering FAQ (Companion)
- Source URL: https://blog.ltbase.dev/posts/agents/harness-engineering-faq
- Direct fetch blocked (private network); ingested via browser extraction
- Raw saved: raw/articles/ltbase-harness-engineering-faq-2026-04-24.md
- Created: queries/harness-engineering-faq-companion.md (9 Q&A + 5 anti-patterns + implementation order)
- Updated: concepts/harness-engineering.md (added FAQ source + link)
- Updated: index.md (total pages: 80)
- Key contribution: 9 production decisions (tool preprocessing, deterministic validation, DAG execution, plan quality, state storage, boundary validation, Sprint Contract, implementation priority, dynamic tool selection) + 5 common anti-patterns

## [2026-04-24] ingest | Lance Martin: Launching Claude Managed Agents
- Source URL: https://x.com/RLanceMartin/status/2041927992986009773
- X post blocked without login; ingested via browser extraction + r.jina.ai fallback
- Raw saved: raw/articles/lance-martin-claude-managed-agents-2026-04-09.md
- Created: entities/lance-martin.md (Anthropic engineer, main driver of Claude Managed Agents)
- Created: entities/claude-managed-agents.md (managed harness product page: brain/hands/session decoupling, 3 core concepts, 4 usage patterns, SDK/CLI/skills onboarding)
- Updated: concepts/harness-engineering.md (added [[claude-managed-agents]] link as validation of "harness thins but doesn't disappear")
- Updated: comparisons/framework-vs-runtime-vs-harness.md (added "托管模式"比喻行: template config / managed infra / managed harness with 3-body separation)
- Updated: index.md (total pages: 82)
- Key contribution: first major "managed harness" product signal — validates that harness engineering is moving toward "thinner harness + heavier infrastructure" rather than "no harness"

## [2026-04-25] ingest | Akshay Pachaar: The Anatomy of an Agent Harness
- Source URL: https://x.com/akshay_pachaar/status/2041146899319971922
- Previous fetch on 2026-04-14 returned login wall; successful re-fetch on 2026-04-25 via r.jina.ai
- Raw saved: raw/articles/akshay-pachaar-anatomy-of-agent-harness-2026-04-25.md (replaced failed raw/articles/x-x-post-2041146899319971922-2026-04-14.md)
- Created: entities/akshay-pachaar.md (12-component + 7-choice harness map, TerminalBench evidence, platform comparison)
- Updated: concepts/harness-engineering.md (added conclusion #19, updated sources + updated date)
- Updated: concepts/coding-agent-workflow-patterns.md (added 7-step TAO cycle + Initializer→Coding Agent接力模式, updated sources + updated date)
- Updated: concepts/agent-memory-patterns.md (added 三层记忆模型 + OpenAI四类持久策略 + 记忆作为hint, updated sources + updated date)
- Updated: comparisons/codex-vs-claude-code-vs-cursor.md (added detailed platform implementation comparison table, updated sources + updated date)
- Updated: index.md (total pages: 83)
- Key contribution: most complete harness component map in the wiki; 12 components + 7 architectural choices + cross-platform implementation details

## [2026-04-25] ingest | Terminal-Bench 2.0 paper + Stanford Meta-Harness artifact
- Source URLs: https://arxiv.org/abs/2601.11868, https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact
- Raw saved: raw/papers/terminal-bench-2.0-paper-2026-01-17.md (arXiv abstract + key facts)
- Raw saved: raw/articles/stanford-meta-harness-tbench2-2026-04-25.md (GitHub README with method details)
- Updated: entities/wolfbench.md (added TerminalBench 2.0 academic foundation + Meta-Harness 76.4% result)
- Updated: concepts/coding-agent-evals.md (added TerminalBench 2.0 as key benchmark + Meta-Harness automated harness evolution as eval new dimension)
- Updated: entities/akshay-pachaar.md (precise TerminalBench + Meta-Harness citation)
- Key findings:
  - TerminalBench 2.0: 89 real-workflow terminal tasks, frontier models/agents < 65%, Harbor harness supports Claude Code/Codex CLI/OpenHands/Mini-SWE-Agent
  - Stanford Meta-Harness: 76.4% on TerminalBench 2.0 (Claude Opus 4.6, 89×5 trials), key innovation = automated harness evolution + environment bootstrapping
  - Environment bootstrapping: inject sandbox snapshot (cwd, files, languages, tools, package managers, memory) before agent loop, saving 2-5 early exploration turns
  - This is the first public empirical evidence that harness layer can be automatically discovered/optimized, not just hand-tuned

## [2026-04-25] ingest | Meta-Harness paper (arXiv:2603.28052)
- Source URL: https://arxiv.org/abs/2603.28052
- Raw saved: raw/papers/meta-harness-paper-2026-03-30.md (full paper extraction)
- Created: entities/meta-harness.md (Stanford IRIS Lab outer-loop harness optimization system)
- Updated: entities/wolfbench.md (added Meta-Harness as TerminalBench-2 #2 ranked agent)
- Updated: index.md (total pages: 84)
- Key findings from paper:
  - Meta-Harness is an outer-loop system that searches over harness code using an agentic proposer with filesystem access to all prior candidates' source code, scores, and execution traces
  - Three domains validated: online text classification (+7.7 pts, 4× fewer tokens), retrieval-augmented math reasoning (+4.7 pts across 5 held-out models), agentic coding (76.4% on TerminalBench-2)
  - Key design: minimum necessary structure — proposer gets raw filesystem access, not pre-processed summaries; full experience history preserved
  - Ablation: full interface (scores+traces) reaches 50.0 median accuracy; scores-only 34.6; scores+summary 34.9 — execution traces are the critical ingredient
  - TerminalBench-2 discovered harness: environment bootstrapping (sandbox snapshot before agent loop: cwd, files, languages, tools, package managers, memory) — saves 2-4 exploration turns
  - Proposer reads extensively from filesystem during search, equal attention to source code and execution traces
  - Search narrative: proposer learns from regressions, forms explicit diagnosis, shifts to safer design pattern
  - OOD generalization: 73.1% average on 9 unseen text classification datasets, outperforming ACE (70.2%)
  - Ranks #2 among all Opus 4.6 agents on TerminalBench-2 (ForgeCode #1 at 81.8% but unreproducible); #1 among all Haiku 4.5 agents
  - Main repo: https://github.com/stanford-iris-lab/meta-harness (framework + 2 reference experiments)
  - TerminalBench-2 artifact: https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact
