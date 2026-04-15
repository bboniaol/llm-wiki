Title: Model Context Protocol (MCP) | Cursor Docs

URL Source: https://www.cursor.com/docs/context/mcp

Markdown Content:
## [What is MCP?](https://www.cursor.com/docs/context/mcp#what-is-mcp)

[Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) enables Cursor to connect to external tools and data sources.

### [Why use MCP?](https://www.cursor.com/docs/context/mcp#why-use-mcp)

MCP connects Cursor to external systems and data. Instead of explaining your project structure repeatedly, integrate directly with your tools.

Write MCP servers in any language that can print to `stdout` or serve an HTTP endpoint - Python, JavaScript, Go, etc.

Browse official plugins in the [Cursor Marketplace](https://cursor.com/marketplace). For community plugins and MCP servers, browse [cursor.directory](https://cursor.directory/).

### [How it works](https://www.cursor.com/docs/context/mcp#how-it-works)

MCP servers expose capabilities through the protocol, connecting Cursor to external tools or data sources.

Cursor supports three transport methods:

| Transport | Execution environment | Deployment | Users | Input | Auth |
| --- | --- | --- | --- | --- | --- |
| **`stdio`** | Local | Cursor manages | Single user | Shell command | Manual |
| **`SSE`** | Local/Remote | Deploy as server | Multiple users | URL to an SSE endpoint | OAuth |
| **`Streamable HTTP`** | Local/Remote | Deploy as server | Multiple users | URL to an HTTP endpoint | OAuth |

### [Protocol and extension support](https://www.cursor.com/docs/context/mcp#protocol-and-extension-support)

Cursor supports these MCP protocol capabilities and extensions:

| Feature | Support | Description |
| --- | --- | --- |
| **Tools** | Supported | Functions for the AI model to execute |
| **Prompts** | Supported | Templated messages and workflows for users |
| **Resources** | Supported | Structured data sources that can be read and referenced |
| **Roots** | Supported | Server-initiated inquiries into URI or filesystem boundaries |
| **Elicitation** | Supported | Server-initiated requests for additional information from users |
| **Apps (extension)** | Supported | Interactive UI views returned by MCP tools |

### [MCP apps](https://www.cursor.com/docs/context/mcp#mcp-apps)

Cursor supports the [MCP Apps extension](https://modelcontextprotocol.io/extensions/apps/overview). MCP tools can return interactive UI along with standard tool output.

MCP Apps follow progressive enhancement. If a host cannot render app UI, the same tool still works through normal MCP responses.

## [Installing MCP servers](https://www.cursor.com/docs/context/mcp#installing-mcp-servers)

### [One-click installation](https://www.cursor.com/docs/context/mcp#one-click-installation)

Browse the [Cursor Marketplace](https://cursor.com/marketplace) for official plugins with one-click install. For community plugins and MCP servers, browse [cursor.directory](https://cursor.directory/). Click "Add to Cursor" on a marketplace entry to install it and authenticate with OAuth.

### [Using `mcp.json`](https://www.cursor.com/docs/context/mcp#using-mcpjson)

Configure custom MCP servers with a JSON file:

### [Static OAuth for remote servers](https://www.cursor.com/docs/context/mcp#static-oauth-for-remote-servers)

For MCP servers that use OAuth, you can provide **static OAuth client credentials** in `mcp.json` instead of dynamic client registration. Use this when:

*   The MCP provider gives you a fixed **Client ID** (and optionally **Client Secret**)
*   The provider requires **whitelisting a redirect URL** (e.g. Figma, Linear)
*   The provider does not support OAuth 2.0 Dynamic Client Registration

Add an `auth` object to remote server entries that use `url`:

| Field | Required | Description |
| --- | --- | --- |
| **CLIENT_ID** | Yes | OAuth 2.0 Client ID from the MCP provider |
| **CLIENT_SECRET** | No | OAuth 2.0 Client Secret (if the provider uses confidential clients) |
| **scopes** | No | OAuth scopes to request. If omitted, Cursor will use `/.well-known/oauth-authorization-server` to discover `scopes_supported` |

#### [Static redirect URL](https://www.cursor.com/docs/context/mcp#static-redirect-url)

Cursor uses a **fixed OAuth redirect URL** for all MCP servers:

When configuring the MCP provider's OAuth app, register this URL as an allowed redirect URI. The server is identified via the OAuth `state` parameter, so one redirect URL works for all MCP servers.

#### [Combining with config interpolation](https://www.cursor.com/docs/context/mcp#combining-with-config-interpolation)

`auth` values support the same interpolation as other fields:

Use environment variables for Client ID and Client Secret instead of hardcoding them.

### [STDIO server configuration](https://www.cursor.com/docs/context/mcp#stdio-server-configuration)

For STDIO servers (local command-line servers), configure these fields in your `mcp.json`:

| Field | Required | Description | Examples |
| --- | --- | --- | --- |
| **type** | Yes | Server connection type | `"stdio"` |
| **command** | Yes | Command to start the server executable. Must be available on your system path or contain its full path. | `"npx"`, `"node"`, `"python"`, `"docker"` |
| **args** | No | Array of arguments passed to the command | `["server.py", "--port", "3000"]` |
| **env** | No | Environment variables for the server | `{"API_KEY": "${env:api-key}"}` |
| **envFile** | No | Path to an environment file to load more variables | `".env"`, `"${workspaceFolder}/.env"` |

### [Using the Extension API](https://www.cursor.com/docs/context/mcp#using-the-extension-api)

For programmatic MCP server registration, Cursor provides an extension API that allows dynamic configuration without modifying `mcp.json` files. This is particularly useful for enterprise environments and automated setup workflows.

[Extension API reference Register MCP servers programmatically using `vscode.cursor.mcp.registerServer()`](https://cursor.com/docs/extension-api)

### [Configuration locations](https://www.cursor.com/docs/context/mcp#configuration-locations)

### [Config interpolation](https://www.cursor.com/docs/context/mcp#config-interpolation)

Use variables in `mcp.json` values. Cursor resolves variables in these fields: `command`, `args`, `env`, `url`, and `headers`.

Supported syntax:

*   `${env:NAME}` environment variables
*   `${userHome}` path to your home folder
*   `${workspaceFolder}` project root (the folder that contains `.cursor/mcp.json`)
*   `${workspaceFolderBasename}` name of the project root
*   `${pathSeparator}` and `${/}` OS path separator

Examples

### [Authentication](https://www.cursor.com/docs/context/mcp#authentication)

MCP servers use environment variables for authentication. Pass API keys and tokens through the config.

Cursor supports OAuth for servers that require it.

## [Using MCP in chat](https://www.cursor.com/docs/context/mcp#using-mcp-in-chat)

Agent automatically uses MCP tools listed under `Available Tools` when relevant. This includes [Plan Mode](https://cursor.com/docs/agent/plan-mode#plan). Ask for a specific tool by name or describe what you need. Enable or disable tools from settings.

### [Tool approval](https://www.cursor.com/docs/context/mcp#tool-approval)

Agent asks for approval before using MCP tools by default. Click the arrow next to the tool name to see arguments.

#### [Auto-run](https://www.cursor.com/docs/context/mcp#auto-run)

Enable auto-run for Agent to use MCP tools without asking. Works like terminal commands. Read more about Auto-run settings [here](https://cursor.com/docs/agent/overview#auto-run).

To pre-configure which MCP tools can auto-run without using the settings UI, add them to [`~/.cursor/permissions.json`](https://cursor.com/docs/reference/permissions).

### [Tool response](https://www.cursor.com/docs/context/mcp#tool-response)

Cursor shows the response in chat with expandable views of arguments and responses:

### [Images as context](https://www.cursor.com/docs/context/mcp#images-as-context)

MCP servers can return images - screenshots, diagrams, etc. Return them as base64 encoded strings:

See this [example server](https://github.com/msfeldstein/mcp-test-servers/blob/main/src/image-server.js) for implementation details. Cursor attaches returned images to the chat. If the model supports images, it analyzes them.

## [Security considerations](https://www.cursor.com/docs/context/mcp#security-considerations)

When installing MCP servers, consider these security practices:

*   **Verify the source**: Only install MCP servers from trusted developers and repositories
*   **Review permissions**: Check what data and APIs the server will access
*   **Limit API keys**: Use restricted API keys with minimal required permissions
*   **Audit code**: For critical integrations, review the server's source code

Remember that MCP servers can access external services and execute code on your behalf. Always understand what a server does before installation.

## [Real-world examples](https://www.cursor.com/docs/context/mcp#real-world-examples)

For practical examples of MCP in action:

*   **[Xcode integration](https://cursor.com/docs/integrations/xcode)** — Connect Cursor to Xcode 26.3+ for builds, tests, SwiftUI previews, and Apple documentation search
*   **[Web Development guide](https://cursor.com/for/web-development)** — Integrate Linear, Figma, and browser tools into your development workflow

## [FAQ](https://www.cursor.com/docs/context/mcp#faq)
