Title: Capabilities | Cursor Docs

URL Source: https://www.cursor.com/docs/cloud-agent/capabilities

Markdown Content:
## [Computer use](https://www.cursor.com/docs/cloud-agent/capabilities#computer-use)

Each cloud agent runs in its own isolated VM with a full desktop environment. Agents can use a mouse and keyboard to control the desktop and browser, allowing them to interact with the software they build like a human developer.

This means agents can start dev servers, open the app in a browser, click through UI flows, and verify their changes work before pushing a PR. Read more in the [announcement blog post](https://cursor.com/blog/agent-computer-use).

## [Demos and Artifacts](https://www.cursor.com/docs/cloud-agent/capabilities#demos-and-artifacts)

Agents create artifacts such as screenshots, videos, and log references to demonstrate their work. These artifacts are attached to the PR so you can quickly validate changes without checking out the branch locally.

### [Artifacts in GitHub](https://www.cursor.com/docs/cloud-agent/capabilities#artifacts-in-github)

You can opt-in to have Cloud Agents embed artifacts directly into GitHub pull request descriptions by enabling the **Allow posting artifacts to GitHub** setting in the [Cloud Agents dashboard](https://cursor.com/dashboard/cloud-agents#my-pull-requests).

## [MCP tools](https://www.cursor.com/docs/cloud-agent/capabilities#mcp-tools)

Cloud agents can use [MCP (Model Context Protocol)](https://cursor.com/docs/mcp) servers configured for your team. This gives agents access to external tools and data sources like databases, APIs, and third-party services during their runs.

Add and enable MCP servers through the MCP dropdown in [cursor.com/agents](https://cursor.com/agents).

Cloud agents support OAuth for MCP servers that need it. OAuth is per-user, including for MCP servers shared at the team level.

### [Custom MCP servers](https://www.cursor.com/docs/cloud-agent/capabilities#custom-mcp-servers)

You can add custom MCP servers using either **HTTP** or **stdio** transport. SSE and `mcp-remote` are not supported.

MCP configurations are encrypted at rest. Sensitive fields are redacted and cannot be read back by any user after saving:

*   **`env`** — environment variables for stdio servers
*   **`headers`** — request headers for HTTP servers
*   **`CLIENT_SECRET`** — OAuth client secret for HTTP servers

### [HTTP vs stdio](https://www.cursor.com/docs/cloud-agent/capabilities#http-vs-stdio)

*   **HTTP (recommended)** — server configurations are never present in the cloud agent's VM environment. The agent does not have access to refresh tokens, headers, or other credentials. Tool calls are proxied through the backend.
*   **Stdio** — servers run inside the cloud agent's VM, so the agent has access to the server's configuration and environment variables. This is similar to how stdio MCPs work in the Cursor IDE.

## [Fixing CI Failures](https://www.cursor.com/docs/cloud-agent/capabilities#fixing-ci-failures)

Cloud Agents will automatically attempt to fix CI failures in PRs they create. They will ignore failing CI checks that are also failing in the base commit of the PR. Currently, only GitHub Actions is supported.

To disable this feature on all your personal Cloud Agents, go to [Cursor Dashboard → Cloud Agents → My Settings](https://cursor.com/dashboard/cloud-agents) and disable the "Automatically fix CI Failures" option.

To disable this feature on a specific Cloud Agent PR, you can comment `@cursor autofix off` on the PR. To re-enable it, comment `@cursor autofix on`.

If you want cloud agents to fix CI failures in your own PRs, you can simply ask them by tagging Cursor in a comment as normal. For example, `@cursor please fix the CI failures`, or `@cursor fix the CI lint check failure`.
