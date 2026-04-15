Title: Automations | Cursor Docs

URL Source: https://www.cursor.com/docs/cloud-agent/automations

Markdown Content:
Cursor Automations run [cloud agents](https://cursor.com/docs/cloud-agent) in the background, either on a schedule or in response to events from GitHub, Slack, and more.

Automations can be used to automate tasks like [tedious code maintenance](https://cursor.com/marketplace/automations/clean-up-feature-flags), [performing deep review for vulnerabilities](https://cursor.com/marketplace/automations/find-vulnerabilities), and [triaging bugs in Slack](https://cursor.com/marketplace/automations/fix-slack-bugs).

## [Getting started](https://www.cursor.com/docs/cloud-agent/automations#getting-started)

Create a new automation at [cursor.com/automations](https://cursor.com/automations), or start from a template in the [marketplace](https://cursor.com/marketplace/automations).

1.   Choose a trigger, e.g. every hour or when a pull request is opened.
2.   Write a prompt with instructions for the automation.
3.   Choose the tools the agent is able to use, such as Send to Slack, Comment on Pull Request, or tools from MCP.
4.   Create the automation and watch it run!

## [Billing](https://www.cursor.com/docs/cloud-agent/automations#billing)

Automations create cloud agents and are billed based on cloud agent usage. See [cloud agent pricing](https://cursor.com/docs/models-and-pricing#model-pricing) for details.

How usage is billed depends on the automation's [permission scope](https://www.cursor.com/docs/cloud-agent/automations#permissions):

*   **Team Owned**: Usage is billed to the team's usage pool. Automations execute under a shared team service account, so no individual user's usage is affected.
*   **Private**: Usage is billed to the user who created the automation.
*   **Team Visible**: Usage is billed to the user who created the automation, the same as Private.

## [Triggers](https://www.cursor.com/docs/cloud-agent/automations#triggers)

Triggers decide when an automation runs. An automation can have more than one trigger and is run when _any_ trigger fires.

### [Scheduled triggers](https://www.cursor.com/docs/cloud-agent/automations#scheduled-triggers)

Scheduled triggers run on a recurring schedule. Choose from preset options or enter a cron expression for precise control.

Scheduled triggers may run with a delay but will not start before the indicated time.

### [GitHub triggers](https://www.cursor.com/docs/cloud-agent/automations#github-triggers)

GitHub triggers respond to GitHub events, such as when a pull request is opened or merged.

*   **Draft opened** - When a draft pull request is created.
*   **Pull request opened** - When a non-draft PR is created or a draft is marked ready for review.
*   **Pull request pushed** - When new commits are pushed to an existing PR.
*   **Pull request label changed** - When a specific label, or any label, is added to or removed from an existing PR.
*   **Pull request merged** - When a PR is merged.
*   **Pull request commented** - When someone comments on a PR.
*   **Push to branch** - When commits are pushed to a specific branch outside a pull request.
*   **CI completed** - When a GitHub Check finishes on a pull request or branch.

### [Slack triggers](https://www.cursor.com/docs/cloud-agent/automations#slack-triggers)

Slack triggers respond to events from the [Cursor Slack integration](https://cursor.com/docs/integrations/slack).

*   **New message in channel** - When a message is sent to a connected Slack channel. Without a message filter, the trigger only fires on top-level channel messages. Add a keyword or regex filter if you want runs from threaded replies as well.
*   **Channel created** - When a new public Slack channel is created in your workspace.

### [Webhook triggers](https://www.cursor.com/docs/cloud-agent/automations#webhook-triggers)

Webhook triggers create a private HTTP endpoint for your automation. POST to the endpoint to start a run. You can use webhooks to connect automations to internal systems, CI pipelines, monitoring tools, and more.

To retrieve the webhook URL, you must save the automation first, which will then generate a webhook URL to call and an API key for authentication.

### [Linear triggers](https://www.cursor.com/docs/cloud-agent/automations#linear-triggers)

Linear triggers respond to events from the [Cursor Linear integration](https://cursor.com/docs/integrations/linear).

*   **Issue created** - When a new issue is created.
*   **Status changed** - When an issue's status changes.
*   **End of cycle** - When a Linear cycle completes.

PagerDuty triggers run on incident events and can be helpful to automatically triage or even resolve incidents.

*   **Incident triggered** - When a new incident is created.
*   **Incident acknowledged** - When an incident is acknowledged.
*   **Incident resolved** - When an incident is resolved.
*   **Any incident event** - Matches all incident event types.

## [Tools](https://www.cursor.com/docs/cloud-agent/automations#tools)

Cursor Automations can have tools enabled for richer capabilities around GitHub, Slack, memory, MCP, and more. Automations also include the same base set of tools as other cloud agents. See [Cloud agent capabilities](https://cursor.com/docs/cloud-agent/capabilities) for details.

### [Open pull request](https://www.cursor.com/docs/cloud-agent/automations#open-pull-request)

Lets the agent create a new pull request on GitHub. The agent can write code, create a branch, and open the pull request.

Use this when the automation should make code changes.

Posts comments on the triggering pull request. Supports top-level review comments and inline code comments.

This action requires a pull request trigger.

### [Request reviewers](https://www.cursor.com/docs/cloud-agent/automations#request-reviewers)

Requests reviewers on the triggering pull request. The agent can use `git`, memory, and other tools to identify domain experts.

This action requires a pull request trigger.

### [Send to Slack](https://www.cursor.com/docs/cloud-agent/automations#send-to-slack)

Sends messages to a Slack channel. You can target a specific channel or let the agent dynamically choose any channel.

Note that the agent is granted read access to public channels that it can send messages to.

### [Read Slack channels](https://www.cursor.com/docs/cloud-agent/automations#read-slack-channels)

Gives the agent read-only access to list and read messages from public Slack channels.

Use this when the agent needs more context before it replies or opens a pull request.

### [MCP server](https://www.cursor.com/docs/cloud-agent/automations#mcp-server)

Connects an [MCP (Model Context Protocol)](https://cursor.com/docs/mcp) server so the agent can use external tools and data sources.

### [Memories](https://www.cursor.com/docs/cloud-agent/automations#memories)

Memories let the agent read and write persistent notes across runs for the same automation. Use this to build agents that remember and improve over time. Each memory is stored as a named entry (`MEMORIES.md` by default) that exists outside the agent's working filesystem.

Memories are enabled by default but can be disabled. Memories can be viewed and edited from the tool configuration UI.

## [Automation settings](https://www.cursor.com/docs/cloud-agent/automations#automation-settings)

### [Model](https://www.cursor.com/docs/cloud-agent/automations#model)

Choose which model the agent uses. The same models as cloud agents are available, which are tailored for autonomous use cases. Cursor chooses a default model when you create the automation.

### [Environment](https://www.cursor.com/docs/cloud-agent/automations#environment)

Automations inherit environment configuration from your [Cloud Agents dashboard](https://cursor.com/dashboard/cloud-agents) and [Cloud agent setup](https://cursor.com/docs/cloud-agent/setup).

*   **Enabled**: The agent installs dependencies before running. Use this when the automation needs to build, test, or execute code.
*   **Disabled**: The agent skips dependency installation. Use this when it only needs to read or review code.

Configure environment settings and secrets in the [Cloud Agents dashboard](https://cursor.com/dashboard/cloud-agents). The automation uses the same settings for the selected repository.

### [Permissions](https://www.cursor.com/docs/cloud-agent/automations#permissions)

Control who can view and manage the automation. The permission scope also determines how usage is [billed](https://www.cursor.com/docs/cloud-agent/automations#billing).

*   **Private**: Only you can manage the automation. Team admins can view and disable the automation.
*   **Team Visible**: Only you can manage the automation. Team members can view the automation, and team admins can disable the automation. It still runs with your auth.
*   **Team Owned**: Team members can view the automation. Only team admins can manage the automation. It runs with the team's shared automations service account.

Promoting an automation from Private or Team Visible to Team Owned changes the identity it runs as. It stops using your auth and starts using the team's shared automations service account. If the automation uses webhook triggers, regenerate its webhook API key after the scope change. If it uses MCPs or other integrations that rely on personal OAuth credentials, make sure those are configured for the team's service account instead. Only team admins can promote an automation to Team Owned.

### [Identity](https://www.cursor.com/docs/cloud-agent/automations#identity)

When an automation acts on external services, it uses the following identities:

*   GitHub comments, review approvals, and reviewer requests run as `cursor`.
*   Team-scoped automations open pull requests as `cursor`.
*   Private automations open pull requests as your GitHub account.
*   Slack messages are sent as the Cursor bot.

## [Writing prompts](https://www.cursor.com/docs/cloud-agent/automations#writing-prompts)

Prompts define what the agent should do. Write them the same way you would write instructions for a cloud agent run.

Tips:

*   Be specific about what the agent should check, change, or produce.
*   Reference the actions you enabled - you can at-mention tools or informally mention their names.
*   Include decision rules for what to do in different cases.
*   Set a quality bar for when the agent should open a pull request, comment, or do nothing.
*   Describe the output format you want.

*   [Cloud agents overview](https://cursor.com/docs/cloud-agent)
*   [Cloud agent setup](https://cursor.com/docs/cloud-agent/setup)
*   [Cloud agent pricing](https://cursor.com/docs/models-and-pricing#model-pricing)
*   [GitHub integration](https://cursor.com/docs/integrations/github)
*   [Slack integration](https://cursor.com/docs/integrations/slack)
*   [Linear integration](https://cursor.com/docs/integrations/linear)
