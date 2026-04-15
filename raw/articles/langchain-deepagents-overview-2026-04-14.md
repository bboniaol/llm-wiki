Title: Deep Agents overview - Docs by LangChain

URL Source: https://docs.langchain.com/oss/python/deepagents/overview

Markdown Content:
# Deep Agents overview - Docs by LangChain

[Skip to main content](https://docs.langchain.com/oss/python/deepagents/overview#content-area)

Join us May 13th & May 14th at Interrupt, the Agent Conference by LangChain. [Buy tickets >](https://interrupt.langchain.com/)

[Docs by LangChain home page![Image 1: light logo](https://mintcdn.com/langchain-5e9cc07a/nQm-sjd_MByLhgeW/images/brand/langchain-docs-dark-blue.png?fit=max&auto=format&n=nQm-sjd_MByLhgeW&q=85&s=5babf1a1962208fd7eed942fa2432ecb)![Image 2: dark logo](https://mintcdn.com/langchain-5e9cc07a/nQm-sjd_MByLhgeW/images/brand/langchain-docs-light-blue.png?fit=max&auto=format&n=nQm-sjd_MByLhgeW&q=85&s=0bcd2a1f2599ed228bcedf0f535b45b1)](https://docs.langchain.com/)![Image 3: https://mintlify.s3.us-west-1.amazonaws.com/langchain-5e9cc07a/images/brand/langchain-icon.png](https://mintlify.s3.us-west-1.amazonaws.com/langchain-5e9cc07a/images/brand/langchain-icon.png)Open source

Search...

Ctrl K

*   [Ask AI](https://chat.langchain.com/)
*   [GitHub](https://github.com/langchain-ai)
*   [Try LangSmith](https://smith.langchain.com/)
*   [Try LangSmith](https://smith.langchain.com/)

Search...

Navigation

Deep Agents overview

[Deep Agents](https://docs.langchain.com/oss/python/deepagents/overview)[LangChain](https://docs.langchain.com/oss/python/langchain/overview)[LangGraph](https://docs.langchain.com/oss/python/langgraph/overview)[Integrations](https://docs.langchain.com/oss/python/integrations/providers/overview)[Learn](https://docs.langchain.com/oss/python/learn)[Reference](https://docs.langchain.com/oss/python/reference/overview)[Contribute](https://docs.langchain.com/oss/python/contributing/overview)

Python

*   [Overview](https://docs.langchain.com/oss/python/deepagents/overview)

##### Get started

*   [Quickstart](https://docs.langchain.com/oss/python/deepagents/quickstart)
*   [Customization](https://docs.langchain.com/oss/python/deepagents/customization)
*   [Comparison](https://docs.langchain.com/oss/python/deepagents/comparison)
*   [Changelog](https://docs.langchain.com/oss/python/releases/changelog)

##### Deployment

*   [Deploy with the CLI](https://docs.langchain.com/oss/python/deepagents/deploy)
*   [Going to production](https://docs.langchain.com/oss/python/deepagents/going-to-production)

##### Core capabilities

*   [Overview](https://docs.langchain.com/oss/python/deepagents/harness)
*   [Models](https://docs.langchain.com/oss/python/deepagents/models)
*   [Context engineering](https://docs.langchain.com/oss/python/deepagents/context-engineering)
*   [Backends](https://docs.langchain.com/oss/python/deepagents/backends)
*   [Subagents](https://docs.langchain.com/oss/python/deepagents/subagents)
*   [Async subagents](https://docs.langchain.com/oss/python/deepagents/async-subagents)
*   [Human-in-the-loop](https://docs.langchain.com/oss/python/deepagents/human-in-the-loop)
*   [Permissions](https://docs.langchain.com/oss/python/deepagents/permissions)
*   [Memory](https://docs.langchain.com/oss/python/deepagents/memory)
*   [Skills](https://docs.langchain.com/oss/python/deepagents/skills)
*   [Sandboxes](https://docs.langchain.com/oss/python/deepagents/sandboxes)
*   [Streaming](https://docs.langchain.com/oss/python/deepagents/streaming)

##### Frontend

*   [Overview](https://docs.langchain.com/oss/python/deepagents/frontend/overview)
*   Patterns  

##### Protocols

*   [Agent Client Protocol (ACP)](https://docs.langchain.com/oss/python/deepagents/acp)

##### Command line interface

*   [Use the CLI](https://docs.langchain.com/oss/python/deepagents/cli/overview)
*   [Model providers](https://docs.langchain.com/oss/python/deepagents/cli/providers)
*   [Configuration](https://docs.langchain.com/oss/python/deepagents/cli/configuration)
*   [MCP Tools](https://docs.langchain.com/oss/python/deepagents/cli/mcp-tools)

On this page

*   [Create a deep agent](https://docs.langchain.com/oss/python/deepagents/overview#create-a-deep-agent)
*   [When to use the Deep Agents](https://docs.langchain.com/oss/python/deepagents/overview#when-to-use-the-deep-agents)
*   [Core capabilities](https://docs.langchain.com/oss/python/deepagents/overview#core-capabilities)
*   [Get started](https://docs.langchain.com/oss/python/deepagents/overview#get-started)

# Deep Agents overview

Copy page

Build agents that can plan, use subagents, and leverage file systems for complex tasks

Copy page

The easiest way to start building agents and applications powered by LLMs—with built-in capabilities for task planning, file systems for context management, subagent-spawning, and long-term memory. You can use deep agents for any task, including complex, multi-step tasks.We think of `deepagents` as an [“agent harness”](https://docs.langchain.com/oss/python/concepts/products#agent-harnesses-like-the-deep-agents-sdk). It is the same core tool calling loop as other agent frameworks, but with built-in tools and capabilities.[`deepagents`](https://pypi.org/project/deepagents/) is a standalone library built on top of [LangChain](https://docs.langchain.com/oss/python/langchain)’s core building blocks for agents. It uses the [LangGraph](https://docs.langchain.com/oss/python/langgraph) runtime for durable execution, streaming, human-in-the-loop, and other features.The [`deepagents` repository](https://github.com/langchain-ai/deepagents) contains:
*   **Deep Agents SDK**: A package for building agents that can handle any task
*   [**Deep Agents CLI**](https://docs.langchain.com/oss/python/deepagents/cli): A terminal coding agent built on the Deep Agents SDK
*   [**ACP integration**](https://docs.langchain.com/oss/python/deepagents/acp): An Agent Client Protocol connector for using deep agents in code editors like Zed

[LangChain](https://docs.langchain.com/oss/python/langchain) is the framework that provides the core building blocks for your agents. To learn more about the differences between LangChain, LangGraph, and Deep Agents, see [Frameworks, runtimes, and harnesses](https://docs.langchain.com/oss/python/concepts/products).
## [​](https://docs.langchain.com/oss/python/deepagents/overview#create-a-deep-agent)

 Create a deep agent

```
# pip install -qU deepagents
from deepagents import create_deep_agent

def get_weather(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

agent = create_deep_agent(
    model="openai:gpt-5.4",
    tools=[get_weather],
    system_prompt="You are a helpful assistant",
)

# Run the agent
agent.invoke(
    {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
)
```

See the [Quickstart](https://docs.langchain.com/oss/python/deepagents/quickstart) and [Customization guide](https://docs.langchain.com/oss/python/deepagents/customization) to get started building your own agents and applications with Deep Agents.

Use [LangSmith](https://docs.langchain.com/langsmith/home) to trace requests, debug agent behavior, and evaluate outputs. Set `LANGSMITH_TRACING=true` and your API key to get started.

## [​](https://docs.langchain.com/oss/python/deepagents/overview#when-to-use-the-deep-agents)

When to use the Deep Agents

Use the **Deep Agents SDK** when you want to build agents that can:
*   **Handle complex, multi-step tasks** that require planning and decomposition
*   **Manage large amounts of context** through file system tools and [summarization](https://docs.langchain.com/oss/python/deepagents/context-engineering#summarization)
*   **Swap filesystem backends** to use in-memory state, local disk, durable stores, [sandboxes](https://docs.langchain.com/oss/python/deepagents/sandboxes), or [your own custom backend](https://docs.langchain.com/oss/python/deepagents/backends)
*   **Execute shell commands** via the `execute` tool when using a [sandbox backend](https://docs.langchain.com/oss/python/deepagents/sandboxes)
*   **Delegate work** to specialized subagents for context isolation
*   **Persist memory** across conversations and threads
*   **Control filesystem access** with declarative [permission rules](https://docs.langchain.com/oss/python/deepagents/permissions) that restrict which files agents can read or write
*   **Require human approval** for sensitive operations with [human-in-the-loop](https://docs.langchain.com/oss/python/deepagents/human-in-the-loop) workflows
*   **Use any model** that supports tool calling — [provider agnostic](https://docs.langchain.com/oss/python/deepagents/models) across frontier and open models

For building simpler agents, consider using LangChain’s [`create_agent`](https://docs.langchain.com/oss/python/langchain/agents) or building a custom [LangGraph](https://docs.langchain.com/oss/python/langgraph/overview) workflow.
## [​](https://docs.langchain.com/oss/python/deepagents/overview#core-capabilities)

Core capabilities

## Planning and task decomposition

Deep Agents include a built-in [`write_todos`](https://docs.langchain.com/oss/python/langchain/middleware/built-in#to-do-list) tool that enables agents to break down complex tasks into discrete steps, track progress, and adapt plans as new information emerges.

## Context management

File system tools ([`ls`](https://docs.langchain.com/oss/python/deepagents/harness#virtual-filesystem-access), [`read_file`](https://docs.langchain.com/oss/python/deepagents/harness#virtual-filesystem-access), [`write_file`](https://docs.langchain.com/oss/python/deepagents/harness#virtual-filesystem-access), [`edit_file`](https://docs.langchain.com/oss/python/deepagents/harness#virtual-filesystem-access)) allow agents to offload large context to in-memory or filesystem storage, preventing context window overflow and enabling work with variable-length tool results. Auto-summarization compacts older conversation messages when the context window grows long, keeping the agent effective across extended sessions.

## Shell execution

When using a [sandbox backend](https://docs.langchain.com/oss/python/deepagents/sandboxes), agents get an `execute` tool to run shell commands for tests, builds, git operations, and system tasks. Sandbox backends provide isolation so agents can execute code without compromising your host system.

## Pluggable filesystem backends

The virtual filesystem is powered by [pluggable backends](https://docs.langchain.com/oss/python/deepagents/backends) that you can swap to fit your use case. Choose from in-memory state, local disk, LangGraph store for cross-thread persistence, [sandboxes](https://docs.langchain.com/oss/python/deepagents/sandboxes) for isolated code execution (Modal, Daytona, Deno), or combine multiple backends with composite routing. You can also implement your own custom backend.

## Subagent spawning

A built-in `task` tool enables agents to spawn specialized subagents for context isolation. This keeps the main agent’s context clean while still going deep on specific subtasks.

## Long-term memory

Extend agents with persistent memory across threads using LangGraph’s [Memory Store](https://docs.langchain.com/oss/python/langgraph/persistence#memory-store). Agents can save and retrieve information from previous conversations.

## Filesystem permissions

Declare [permission rules](https://docs.langchain.com/oss/python/deepagents/permissions) that control which files and directories agents can read or write. Subagents can inherit or override the parent’s rules.

## Human-in-the-loop

Configure [human approval](https://docs.langchain.com/oss/python/deepagents/human-in-the-loop) for sensitive tool operations using LangGraph’s interrupt capabilities. Control which tools require confirmation before execution.

## Skills

Extend agents with reusable [skills](https://docs.langchain.com/oss/python/deepagents/skills) that provide specialized workflows, domain knowledge, and custom instructions.

## Smart defaults

Ships with opinionated system prompts that teach the model how to use its tools effectively — plan before acting, verify work, and manage context. Customize or replace the defaults as needed.

## [​](https://docs.langchain.com/oss/python/deepagents/overview#get-started)

Get started

[## SDK Quickstart Build your first deep agent](https://docs.langchain.com/oss/python/deepagents/quickstart)

[## Customization Learn about customization options for the SDK](https://docs.langchain.com/oss/python/deepagents/customization)

[## Models Configure models and providers](https://docs.langchain.com/oss/python/deepagents/models)

[## Backends Choose and configure pluggable filesystem backends](https://docs.langchain.com/oss/python/deepagents/backends)

[## Sandboxes Execute code in isolated environments](https://docs.langchain.com/oss/python/deepagents/sandboxes)

[## Permissions Control filesystem access with permission rules](https://docs.langchain.com/oss/python/deepagents/permissions)

[## Human-in-the-loop Configure approval for sensitive operations](https://docs.langchain.com/oss/python/deepagents/human-in-the-loop)

[## CLI Use the Deep Agents CLI](https://docs.langchain.com/oss/python/deepagents/cli/overview)

[## ACP Use deep agents in code editors via ACP](https://docs.langchain.com/oss/python/deepagents/acp)

[## Reference See the `deepagents` API reference](https://reference.langchain.com/python/deepagents/)

* * *

[Edit this page on GitHub](https://github.com/langchain-ai/docs/edit/main/src/oss/deepagents/overview.mdx) or [file an issue](https://github.com/langchain-ai/docs/issues/new/choose).

[Connect these docs](https://docs.langchain.com/use-these-docs) to Claude, VSCode, and more via MCP for real-time answers.

Was this page helpful?

Yes No

[Quickstart Next](https://docs.langchain.com/oss/python/deepagents/quickstart)

Ctrl+I

[Docs by LangChain home page![Image 4: light logo](https://mintcdn.com/langchain-5e9cc07a/nQm-sjd_MByLhgeW/images/brand/langchain-docs-dark-blue.png?fit=max&auto=format&n=nQm-sjd_MByLhgeW&q=85&s=5babf1a1962208fd7eed942fa2432ecb)![Image 5: dark logo](https://mintcdn.com/langchain-5e9cc07a/nQm-sjd_MByLhgeW/images/brand/langchain-docs-light-blue.png?fit=max&auto=format&n=nQm-sjd_MByLhgeW&q=85&s=0bcd2a1f2599ed228bcedf0f535b45b1)](https://docs.langchain.com/)

[github](https://github.com/langchain-ai)[x](https://x.com/LangChain)[linkedin](https://www.linkedin.com/company/langchain)[youtube](https://www.youtube.com/@LangChain)

Resources

[Forum](https://forum.langchain.com/)[Changelog](https://changelog.langchain.com/)[LangChain Academy](https://academy.langchain.com/)[Contact Sales](https://www.langchain.com/contact-sales)

Company

[Home](https://langchain.com/)[Trust Center](https://trust.langchain.com/)[Careers](https://langchain.com/careers)[Blog](https://blog.langchain.com/)

[github](https://github.com/langchain-ai)[x](https://x.com/LangChain)[linkedin](https://www.linkedin.com/company/langchain)[youtube](https://www.youtube.com/@LangChain)

## Chat LangChain

[](https://chat.langchain.com/ "Open chat.langchain.com in a new tab")
