Title: Overview | Cursor Docs

URL Source: https://www.cursor.com/docs/agent/overview

Markdown Content:
## Cursor Agent

Agent is Cursor's assistant that can complete complex coding tasks independently, run terminal commands, and edit code. Access in sidepane with Cmd+I Ctrl+I.

Learn more about [how agents work](https://cursor.com/learn/agents) and help you build faster.

## [How Agent works](https://www.cursor.com/docs/agent/overview#how-agent-works)

An agent is built on three components:

1.   **Instructions**: The system prompt and [rules](https://cursor.com/docs/rules) that guide agent behavior
2.   **Tools**: File editing, codebase search, terminal execution, and more
3.   **Model**: The agent model you pick for the task

Cursor's agent orchestrates these components for each model we support, tuning instructions and tools specifically for every frontier model. As new models are released, you can focus on building software while Cursor handles the model-specific optimizations.

## [Tools](https://www.cursor.com/docs/agent/overview#tools)

Tools are the building blocks of Agent. They are used to search your codebase and the web to find relevant information, make edits to your files, run terminal commands, and more.

To understand how tool calling works under the hood, see our [tool calling fundamentals](https://cursor.com/learn/tool-calling).

There is no limit on the number of tool calls Agent can make during a task.

## [Checkpoints](https://www.cursor.com/docs/agent/overview#checkpoints)

Checkpoints save snapshots of your codebase during an Agent session. Agent automatically creates them before making significant changes, capturing the state of all modified files.

If Agent takes a wrong turn, click any checkpoint in the chat timeline to preview your files at that point, then restore to revert all files to that state. You can also restore from the `Restore Checkpoint` button on previous requests or the + button when hovering over a message.

Checkpoints are useful for exploratory work, complex refactoring, and iterative development where you want safe rollback points.

## [Queued messages](https://www.cursor.com/docs/agent/overview#queued-messages)

Queue follow-up messages while Agent is working on the current task. Your instructions wait in line and execute automatically when ready.

### [Using the queue](https://www.cursor.com/docs/agent/overview#using-the-queue)

1.   While Agent is working, type your next instruction
2.   Press Enter to add it to the queue
3.   Messages appear in order below the active task
4.   Drag to reorder queued messages as needed
5.   Agent processes them sequentially after finishing

### [Keyboard shortcuts](https://www.cursor.com/docs/agent/overview#keyboard-shortcuts)

While Agent is working:

*   Press Enter to queue your message (it waits until Agent finishes the current task)
*   Press Cmd+Enter Ctrl+Enter to send immediately, bypassing the queue

### [Immediate messaging](https://www.cursor.com/docs/agent/overview#immediate-messaging)

When you use Cmd+Enter Ctrl+Enter to send immediately, your message is appended to the most recent user message in the chat and processed right away without waiting in the queue.

*   Your message attaches to tool results and sends immediately
*   This creates a more responsive experience for urgent follow-ups
*   Use this when you need to interrupt or redirect Agent's current work
