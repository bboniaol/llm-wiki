Title: Subagents | Cursor Docs

URL Source: https://www.cursor.com/docs/context/subagents

Markdown Content:
Subagents are specialized AI assistants that Cursor's agent can delegate tasks to. Each subagent operates in its own context window, handles specific types of work, and returns its result to the parent agent. Use subagents to break down complex tasks, do work in parallel, and preserve context in the main conversation.

You can use subagents in the editor, CLI, and [Cloud Agents](https://cursor.com/docs/cloud-agent).

## [How subagents work](https://www.cursor.com/docs/context/subagents#how-subagents-work)

When Agent encounters a complex task, it can launch a subagent automatically. The subagent receives a prompt with all necessary context, works autonomously, and returns a final message with its results.

Subagents start with a clean context. The parent agent includes relevant information in the prompt since subagents don't have access to prior conversation history.

### [Foreground vs background](https://www.cursor.com/docs/context/subagents#foreground-vs-background)

Subagents run in one of two modes:

| Mode | Behavior | Best for |
| --- | --- | --- |
| **Foreground** | Blocks until the subagent completes. Returns the result immediately. | Sequential tasks where you need the output. |
| **Background** | Returns immediately. The subagent works independently. | Long-running tasks or parallel workstreams. |

## [Built-in subagents](https://www.cursor.com/docs/context/subagents#built-in-subagents)

Cursor includes three built-in subagents that handle context-heavy operations automatically. These subagents were designed based on analysis of agent conversations where context window limits were hit.

| Subagent | Purpose | Why it's a subagent |
| --- | --- | --- |
| **Explore** | Searches and analyzes codebases | Codebase exploration generates large intermediate output that would bloat the main context. Uses a faster model to run many parallel searches. |
| **Bash** | Runs series of shell commands | Command output is often verbose. Isolating it keeps the parent focused on decisions, not logs. |
| **Browser** | Controls browser via MCP tools | Browser interactions produce noisy DOM snapshots and screenshots. The subagent filters this down to relevant results. |

### [Why these subagents exist](https://www.cursor.com/docs/context/subagents#why-these-subagents-exist)

These three operations share common traits: they generate noisy intermediate output, benefit from specialized prompts and tools, and can consume significant context. Running them as subagents solves several problems:

*   **Context isolation** — Intermediate output stays in the subagent. The parent only sees the final summary.
*   **Model flexibility** — The explore subagent uses a faster model by default. This enables running 10 parallel searches in the time a single main-agent search would take.
*   **Specialized configuration** — Each subagent has prompts and tool access tuned for its specific task.
*   **Cost efficiency** — Faster models cost less. Isolating token-heavy work in subagents with appropriate model choices reduces overall cost.

You don't need to configure these subagents. Agent uses them automatically when appropriate.

## [When to use subagents](https://www.cursor.com/docs/context/subagents#when-to-use-subagents)

| Use subagents when... | Use skills when... |
| --- | --- |
| You need context isolation for long research tasks | The task is single-purpose (generate changelog, format) |
| Running multiple workstreams in parallel | You want a quick, repeatable action |
| The task requires specialized expertise across many steps | The task completes in one shot |
| You want an independent verification of work | You don't need a separate context window |

## [Quick start](https://www.cursor.com/docs/context/subagents#quick-start)

Agent automatically uses subagents when appropriate. You can also create a custom subagent by asking Agent:

For more control, create custom subagents manually in your project or user directory.

## [Custom subagents](https://www.cursor.com/docs/context/subagents#custom-subagents)

Define custom subagents to encode specialized knowledge, enforce team standards, or automate repetitive workflows.

### [File locations](https://www.cursor.com/docs/context/subagents#file-locations)

| Type | Location | Scope |
| --- | --- | --- |
| **Project subagents** | `.cursor/agents/` | Current project only |
|  | `.claude/agents/` | Current project only (Claude compatibility) |
|  | `.codex/agents/` | Current project only (Codex compatibility) |
| **User subagents** | `~/.cursor/agents/` | All projects for current user |
|  | `~/.claude/agents/` | All projects for current user (Claude compatibility) |
|  | `~/.codex/agents/` | All projects for current user (Codex compatibility) |

Project subagents take precedence when names conflict. When multiple locations contain subagents with the same name, `.cursor/` takes precedence over `.claude/` or `.codex/`.

### [File format](https://www.cursor.com/docs/context/subagents#file-format)

Each subagent is a markdown file with YAML frontmatter:

### [Configuration fields](https://www.cursor.com/docs/context/subagents#configuration-fields)

| Field | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `name` | string | No | Derived from filename | Display name and identifier. Use lowercase letters and hyphens. |
| `description` | string | No | — | Short description shown in Task tool hints. Agent reads this to decide delegation. |
| `model` | string | No | `inherit` | Model to use: `fast`, `inherit`, or a specific model ID. See [model configuration](https://www.cursor.com/docs/context/subagents#model-configuration). |
| `readonly` | boolean | No | `false` | If `true`, the subagent runs with restricted write permissions (no file edits, no state-changing shell commands). |
| `is_background` | boolean | No | `false` | If `true`, the subagent runs in the background without blocking the parent. |

### [Model configuration](https://www.cursor.com/docs/context/subagents#model-configuration)

The `model` field controls which model a subagent uses. There are three options:

| Value | Behavior |
| --- | --- |
| `inherit` | Uses the same model as the parent agent. This is the default. |
| `fast` | Uses a smaller, faster model optimized for speed and cost. Good for high-volume tasks like search, verification, or test execution. |
| A specific model ID | Uses the exact model you specify, such as `claude-4-sonnet` or `gpt-5-mini`. See the [models reference](https://cursor.com/docs/models-and-pricing) for available IDs. |

Choose `inherit` when the subagent needs the same reasoning power as the parent. Choose `fast` for tasks where speed and cost matter more than depth. Use a specific model ID when you need a particular model's capabilities regardless of what the parent uses.

#### [When the configured model won't be used](https://www.cursor.com/docs/context/subagents#when-the-configured-model-wont-be-used)

Cursor honors the `model` field in your subagent frontmatter unless one of these conditions applies:

*   **Team admin restrictions** — Your organization's admin has blocked the specified model.
*   **Max Mode required** — The model requires [Max Mode](https://cursor.com/help/ai-features/max-mode) and you don't have it enabled.
*   **Plan limitations** — The model isn't available on your current plan.

In these cases, Cursor falls back to a compatible model. If you're seeing unexpected model behavior, check your plan settings and Max Mode status.

## [Using subagents](https://www.cursor.com/docs/context/subagents#using-subagents)

### [Automatic delegation](https://www.cursor.com/docs/context/subagents#automatic-delegation)

Agent proactively delegates tasks based on:

*   The task complexity and scope
*   Custom subagent descriptions in your project
*   Current context and available tools

Include phrases like "use proactively" or "always use for" in your description field to encourage automatic delegation.

### [Explicit invocation](https://www.cursor.com/docs/context/subagents#explicit-invocation)

Request a specific subagent by using the `/name` syntax in your prompt:

You can also invoke subagents by mentioning them naturally:

### [Parallel execution](https://www.cursor.com/docs/context/subagents#parallel-execution)

Launch multiple subagents concurrently for maximum throughput:

Agent sends multiple Task tool calls in a single message, so subagents run simultaneously.

## [Resuming subagents](https://www.cursor.com/docs/context/subagents#resuming-subagents)

Subagents can be resumed to continue previous conversations. This is useful for long-running tasks that span multiple invocations.

Each subagent execution returns an agent ID. Pass this ID to resume the subagent with full context preserved:

## [Common patterns](https://www.cursor.com/docs/context/subagents#common-patterns)

### [Verification agent](https://www.cursor.com/docs/context/subagents#verification-agent)

A verification agent independently validates whether claimed work was actually completed. This addresses a common issue where AI marks tasks as done but implementations are incomplete or broken.

This pattern is useful for:

*   Validating that features work end-to-end before marking tickets complete
*   Catching partially implemented functionality
*   Ensuring tests actually pass (not just that test files exist)

### [Orchestrator pattern](https://www.cursor.com/docs/context/subagents#orchestrator-pattern)

For complex workflows, a parent agent can coordinate multiple specialist subagents in sequence:

1.   **Planner** analyzes requirements and creates a technical plan
2.   **Implementer** builds the feature based on the plan
3.   **Verifier** confirms the implementation matches requirements

Each handoff includes structured output so the next agent has clear context.

## [Example subagents](https://www.cursor.com/docs/context/subagents#example-subagents)

### [Debugger](https://www.cursor.com/docs/context/subagents#debugger)

### [Test runner](https://www.cursor.com/docs/context/subagents#test-runner)

## [Best practices](https://www.cursor.com/docs/context/subagents#best-practices)

*   **Write focused subagents** — Each subagent should have a single, clear responsibility. Avoid generic "helper" agents.
*   **Invest in descriptions** — The `description` field determines when Agent delegates to your subagent. Spend time refining it. Test by making prompts and checking if the right subagent gets triggered.
*   **Keep prompts concise** — Long, rambling prompts dilute focus. Be specific and direct.
*   **Add subagents to version control** — Check `.cursor/agents/` into your repository so the team benefits.
*   **Start with Agent-generated agents** — Let Agent help you draft the initial configuration, then customize.
*   **Use hooks for file output** — If you need subagents to produce structured output files, consider using [hooks](https://cursor.com/docs/hooks) to process and save their results consistently.

### [Anti-patterns to avoid](https://www.cursor.com/docs/context/subagents#anti-patterns-to-avoid)

*   **Vague descriptions** — "Use for general tasks" gives Agent no signal about when to delegate. Be specific: "Use when implementing authentication flows with OAuth providers."
*   **Overly long prompts** — A 2,000-word prompt doesn't make a subagent smarter. It makes it slower and harder to maintain.
*   **Duplicating slash commands** — If a task is single-purpose and doesn't need context isolation, use a [slash command](https://cursor.com/help/customization/rules) instead.
*   **Too many subagents** — Start with 2-3 focused subagents. Add more only when you have clear, distinct use cases.

## [Managing subagents](https://www.cursor.com/docs/context/subagents#managing-subagents)

### [Creating subagents](https://www.cursor.com/docs/context/subagents#creating-subagents)

The easiest way to create a subagent is to ask Agent to create one for you:

You can also create subagents manually by adding markdown files to `.cursor/agents/` (project) or `~/.cursor/agents/` (user).

### [Viewing subagents](https://www.cursor.com/docs/context/subagents#viewing-subagents)

Agent includes all custom subagents in its available tools. You can see which subagents are configured by checking the `.cursor/agents/` directory in your project.

## [Performance and cost](https://www.cursor.com/docs/context/subagents#performance-and-cost)

Subagents have trade-offs. Understanding them helps you decide when to use them.

| Benefit | Trade-off |
| --- | --- |
| Context isolation | Startup overhead (each subagent gathers its own context) |
| Parallel execution | Higher token usage (multiple contexts running simultaneously) |
| Specialized focus | Latency (may be slower than main agent for simple tasks) |

### [Token and cost considerations](https://www.cursor.com/docs/context/subagents#token-and-cost-considerations)

*   **Subagents consume tokens independently** — Each subagent has its own context window and token usage. Running five subagents in parallel uses roughly five times the tokens of a single agent.
*   **Evaluate the overhead** — For quick, simple tasks, the main agent is often faster. Subagents shine for complex, long-running, or parallel work.
*   **Subagents can be slower** — The benefit is context isolation, not speed. A subagent doing a simple task may be slower than the main agent because it starts fresh.

## [FAQ](https://www.cursor.com/docs/context/subagents#faq)
