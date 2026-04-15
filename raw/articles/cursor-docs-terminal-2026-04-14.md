Title: Terminal | Cursor Docs

URL Source: https://www.cursor.com/docs/agent/terminal

Markdown Content:
Agent runs shell commands directly in your terminal, with safe sandbox execution on macOS, Linux, and Windows.

## [Sandbox](https://www.cursor.com/docs/agent/terminal#sandbox)

By default, Agent runs terminal commands in a restricted environment that blocks unauthorized file access and network activity. Commands execute automatically while staying confined to your workspace.

For a deep dive into how sandboxing is implemented on each platform, see [Implementing a secure sandbox for local agents](https://cursor.com/blog/agent-sandboxing).

### [Platform requirements](https://www.cursor.com/docs/agent/terminal#platform-requirements)

#### [macOS](https://www.cursor.com/docs/agent/terminal#macos)

*   Cursor v2.0 or later
*   Works out of the box with no additional setup

#### [Windows](https://www.cursor.com/docs/agent/terminal#windows)

*   [WSL2](https://learn.microsoft.com/en-us/windows/wsl/about) must be installed and configured
*   The sandbox runs inside WSL2, applying the same restrictions as on Linux

#### [Linux](https://www.cursor.com/docs/agent/terminal#linux)

*   **Kernel 6.2 or later** with Landlock v3 support (`CONFIG_SECURITY_LANDLOCK=y`)
*   **Unprivileged user namespaces** enabled (most distributions enable this by default)

If your kernel doesn't meet these requirements, Agent falls back to asking for approval before running commands.

**AppArmor setup**

Some distributions restrict user namespaces through AppArmor. The Cursor desktop package ships with the required profile, so no extra setup is needed for local installations.

Remote environments and the standalone [CLI](https://cursor.com/docs/cli/overview) don't include this profile. If sandbox creation fails with a permissions error related to user namespaces, install the AppArmor package for your distribution:

Debian / Ubuntu:

RHEL / Fedora:

After installing, restart Cursor or your CLI session for the sandbox to work.

### [How the sandbox works](https://www.cursor.com/docs/agent/terminal#how-the-sandbox-works)

The sandbox prevents unauthorized access while allowing workspace operations:

| Access Type | Description |
| --- | --- |
| **File access** | Read access to the filesystem Read and write access to workspace directories |
| **Network access** | Blocked by default. Configure with [`sandbox.json`](https://cursor.com/docs/reference/sandbox) or in settings. |
| **Temporary files** | Full access to `/tmp/` or equivalent system temp directories |

The `.cursor` configuration directory stays protected regardless of allowlist settings.

Some commands need full system access and bypass the sandbox. Agent will indicate when a command runs outside the sandbox and ask for your approval.

### [Allowlist](https://www.cursor.com/docs/agent/terminal#allowlist)

Commands on the allowlist skip sandbox restrictions and run immediately. You can add commands to the allowlist by choosing "Add to allowlist" when prompted after a sandboxed command fails.

When a sandboxed command fails due to restrictions, you can:

| Option | Description |
| --- | --- |
| **Skip** | Cancel the command and let Agent try something else |
| **Run** | Execute the command without sandbox restrictions |
| **Add to allowlist** | Run without restrictions and automatically approve it for future use |

#### [Default network allowlist](https://www.cursor.com/docs/agent/terminal#default-network-allowlist)

When network access is enabled, outbound connections are restricted to a curated set of domains. These cover common package registries, cloud providers, and language toolchains so most development workflows work without extra configuration.

## [Sandbox configuration](https://www.cursor.com/docs/agent/terminal#sandbox-configuration)

Customize sandbox behavior with a `sandbox.json` file placed at `~/.cursor/sandbox.json` (per-user) or `<workspace>/.cursor/sandbox.json` (per-repo). Control network access, filesystem paths, build caches, and more.

See the [`sandbox.json` reference](https://cursor.com/docs/reference/sandbox) for the full schema, network pattern syntax, merge behavior, and protected paths.

## [Environment variables](https://www.cursor.com/docs/agent/terminal#environment-variables)

Cursor injects environment variables into every sandboxed child process. These are available to your scripts, build tools, and automation running inside the sandbox.

| Variable | Platforms | Description |
| --- | --- | --- |
| `CURSOR_SANDBOX` | macOS, Linux, Windows | Set to `"seatbelt"` (macOS) or `"native"` (Linux/Windows) when the process is running inside the sandbox. |
| `CURSOR_ORIG_UID` | macOS, Linux | The UID of the user who launched Cursor, captured **before** the sandbox applies any namespace or identity changes. |
| `CURSOR_ORIG_GID` | macOS, Linux | The GID of the user who launched Cursor, captured before sandbox identity changes. |
| `CURSOR_SANDBOX_LANDLOCK_STATUS` | Linux | Reports the active sandbox backend: `fully_enforced` (Landlock), `bubblewrap` (Bubblewrap fallback). Useful for diagnostics. |

### [Docker and container automation](https://www.cursor.com/docs/agent/terminal#docker-and-container-automation)

A common pattern in automation rules and scripts is running Docker containers that need to match the host user's identity. Because the sandbox remaps the UID on Linux, relying on `$(id -u)` produces the wrong value. Use the `CURSOR_ORIG_*` variables instead:

The `${CURSOR_ORIG_UID:-$(id -u)}` fallback ensures the command also works outside the sandbox, where the variables are not set.

## [Editor configuration](https://www.cursor.com/docs/agent/terminal#editor-configuration)

Configure how Agent runs terminal commands at **Settings > Cursor Settings > Agents > Auto-Run**.

### [Auto-run mode](https://www.cursor.com/docs/agent/terminal#auto-run-mode)

Choose how Agent runs tools like command execution, MCP, and file writes:

| Mode | Behavior |
| --- | --- |
| **Run in Sandbox** | Tools and commands auto-run in the sandbox where possible. Available on macOS, Linux, and Windows (via WSL2). |
| **Ask Every Time** | All tools and commands require user approval before running. |
| **Run Everything** | The agent runs all tools and commands automatically without asking for input. |

### [Auto-run network access](https://www.cursor.com/docs/agent/terminal#auto-run-network-access)

Choose how sandboxed commands access the network:

| Mode | Behavior |
| --- | --- |
| **sandbox.json Only** | Network is limited to domains in your `sandbox.json` allowlist. No Cursor defaults are added. |
| **sandbox.json + Defaults** | Your allowlist plus Cursor's built-in defaults (common package managers, etc.). This is the default. |
| **Allow All** | All network access is allowed in the sandbox, regardless of `sandbox.json`. |

### [Protection settings](https://www.cursor.com/docs/agent/terminal#protection-settings)

| Setting | Description |
| --- | --- |
| **Command Allowlist** | Commands that can run automatically outside of the sandbox. |
| **MCP Allowlist** | MCP tools that can run automatically outside of the sandbox. |
| **Browser Protection** | Prevent Agent from automatically running [Browser](https://cursor.com/docs/agent/tools/browser) tools. |
| **File-Deletion Protection** | Prevent Agent from deleting files automatically. |
| **Dotfile Protection** | Prevent Agent from modifying dot files like .gitignore automatically. |
| **External-File Protection** | Prevent Agent from creating or modifying files outside of the workspace automatically. |

## [Enterprise controls](https://www.cursor.com/docs/agent/terminal#enterprise-controls)

Enterprise admins can override editor configurations or change which settings are visible for end users. Navigate to **Settings > Auto-Run** in the [web dashboard](https://cursor.com/dashboard/settings) to view and change these settings.

| Setting | Description |
| --- | --- |
| **Auto-Run Controls** | Enable controls for auto-run and sandbox mode. When disabled, commands auto-run in the sandbox where available, otherwise they ask for permission. |
| **Sandboxing Mode** | Control whether sandbox is available for end users. When enabled, commands auto-run in the sandbox even if they are not on the allowlist. |
| **Sandbox Networking** | Choose whether sandboxed commands have network access. |
| **Delete File Protection** | Prevent Agent from deleting files automatically. |
| **MCP Tool Protection** | Prevent Agent from automatically running MCP tools. |
| **Terminal Command Allowlist** | Commands that can run automatically without sandboxing. When sandbox is enabled, commands not on this list auto-run in sandbox mode. |
| **Enable Run Everything** | Give end users the ability to enable the "Run Everything" auto-run mode. |

## [Troubleshooting](https://www.cursor.com/docs/agent/terminal#troubleshooting)

### [Disable heavy prompts for Agent sessions](https://www.cursor.com/docs/agent/terminal#disable-heavy-prompts-for-agent-sessions)

Use the `CURSOR_AGENT` environment variable in your shell config to detect when the Agent is running and skip initializing fancy prompts/themes.
