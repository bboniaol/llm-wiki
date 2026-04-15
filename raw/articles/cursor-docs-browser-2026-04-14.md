Title: Browser | Cursor Docs

URL Source: https://www.cursor.com/docs/agent/tools/browser

Markdown Content:
Agent can control a web browser to test applications, visually edit layouts and styles, audit accessibility, convert designs into code, and more. With full access to console logs and network traffic, Agent can debug issues and automate comprehensive testing workflows.

## [Native integration](https://www.cursor.com/docs/agent/tools/browser#native-integration)

Agent displays browser actions like screenshots and actions in the chat, as well as the browser window itself either in a separate window or an inline pane.

We've optimized the browser tools to be more efficient and reduce token usage, as well as:

*   **Efficient log handling**: Browser logs are written to files that Agent can grep and selectively read. Instead of summarizing verbose output after every action, Agent reads only the relevant lines it needs. This preserves full context while minimizing token usage.
*   **Visual feedback with images**: Screenshots are integrated directly with the file reading tool, so Agent actually sees the browser state as images rather than relying on text descriptions. This enables better understanding of visual layouts and UI elements.
*   **Smart prompting**: Agent receives additional context about browser logs, including total line counts and preview snippets, helping it make informed decisions about what to inspect.
*   **Development server awareness**: Agent is prompted to detect running development servers and use the correct ports instead of starting duplicate servers or guessing port numbers.

You can use Browser without installing or configuring any external tools.

## [Browser capabilities](https://www.cursor.com/docs/agent/tools/browser#browser-capabilities)

Agent has access to the following browser tools:

The browser includes a design sidebar for modifying your site directly in Cursor. Design and code simultaneously with real-time visual adjustments.

### [Visual editing capabilities](https://www.cursor.com/docs/agent/tools/browser#visual-editing-capabilities)

The sidebar provides powerful visual editing controls:

*   **Position and layout**: Move and rearrange elements on the page. Change flex direction, alignment, and grid layouts.
*   **Dimensions**: Adjust width, height, padding, and margins with precise pixel values.
*   **Colors**: Update colors from your design system or add new gradients. Access color tokens through a visual picker.
*   **Appearance**: Experiment with shadows, opacity, and border radius using visual sliders.
*   **Theme testing**: Test your designs across light and dark themes instantly.

### [Applying changes](https://www.cursor.com/docs/agent/tools/browser#applying-changes)

When your visual adjustments match your vision, click the apply button to trigger an agent that updates your codebase. The agent translates your visual changes into the appropriate code modifications.

You can also select multiple elements across your site and describe changes in text. Agents kick off in parallel, and your changes appear live on the page after hot-reload.

## [Session persistence](https://www.cursor.com/docs/agent/tools/browser#session-persistence)

Browser state persists between Agent sessions based on your workspace. This means:

*   **Cookies**: Authentication cookies and session data remain available across browser sessions
*   **Local Storage**: Data stored in `localStorage` and `sessionStorage` persists
*   **IndexedDB**: Database content is retained between sessions

The browser context is isolated per workspace, ensuring that different projects maintain separate storage and cookie states.

## [Use cases](https://www.cursor.com/docs/agent/tools/browser#use-cases)

### [Web development workflow](https://www.cursor.com/docs/agent/tools/browser#web-development-workflow)

Browser integrates into web development workflows alongside tools like Figma and Linear. See the [Web Development cookbook](https://cursor.com/for/web-development) for a complete guide on using Browser with design systems, project management tools, and component libraries.

### [Accessibility improvements](https://www.cursor.com/docs/agent/tools/browser#accessibility-improvements)

Agent can audit and improve web accessibility to meet WCAG compliance standards.

### [Automated testing](https://www.cursor.com/docs/agent/tools/browser#automated-testing)

Agent can execute comprehensive test suites and capture screenshots for visual regression testing.

### [Design to code](https://www.cursor.com/docs/agent/tools/browser#design-to-code)

Agent can convert designs into working code with responsive layouts.

### [Adjusting UI design from screenshots](https://www.cursor.com/docs/agent/tools/browser#adjusting-ui-design-from-screenshots)

Agent can refine existing interfaces by identifying visual discrepancies and updating component styles.

## [Security](https://www.cursor.com/docs/agent/tools/browser#security)

Browser runs as a secure web view and is controlled using an MCP server running as an extension. Multiple layers protect you from unauthorized access and malicious actions. Cursor's Browser integrations have also been reviewed by multiple external security auditors.

### [Authentication and isolation](https://www.cursor.com/docs/agent/tools/browser#authentication-and-isolation)

The browser implements several security measures:

*   **Token authentication**: Agent layout generates a random authentication token before each browser session starts
*   **Tab isolation**: Each browser tab receives a unique random ID to prevent cross-tab interference
*   **Session-based security**: Tokens regenerate for each new browser session

### [Tool approval](https://www.cursor.com/docs/agent/tools/browser#tool-approval)

Browser tools require your approval by default. Review each action before Agent executes it. This prevents unexpected navigation, data submission, or script execution.

You can configure approval settings in Agent Settings. Available modes:

| Mode | Description |
| --- | --- |
| **Manual approval** | Review and approve each browser action individually (recommended) |
| **Allow-listed actions** | Actions matching your allow list run automatically; others require approval |
| **Auto-run** | All browser actions execute immediately without approval (use with caution) |

### [Allow and block lists](https://www.cursor.com/docs/agent/tools/browser#allow-and-block-lists)

Browser tools integrate with Cursor's [security guardrails](https://cursor.com/docs/agent/security). Configure which browser actions run automatically:

*   **Allow list**: Specify trusted actions that skip approval prompts
*   **Block list**: Define actions that should always be blocked
*   Access settings through: `Cursor Settings` → `Chat` → `Auto-Run`

The allow/block list system provides best-effort protection. AI behavior can be unpredictable due to prompt injection and other issues. Review auto-approved actions regularly.

### [Browser context](https://www.cursor.com/docs/agent/tools/browser#browser-context)

The browser opens as a pane within Cursor, giving Agent full control through MCP tools.

## [Recommended models](https://www.cursor.com/docs/agent/tools/browser#recommended-models)

We recommend using Sonnet 4.5, GPT-5, and Auto for the best performance.

## [Enterprise usage](https://www.cursor.com/docs/agent/tools/browser#enterprise-usage)

For enterprise customers, browser functionality is managed through toggling availability under MCP controls. Admins have granular controls over each MCP server, as well as over browser access.

### [Enabling browser for enterprise](https://www.cursor.com/docs/agent/tools/browser#enabling-browser-for-enterprise)

To enable browser capabilities for your enterprise team:

1.   Navigate to your [Settings Dashboard](https://cursor.com/dashboard/settings)
2.   Go to **MCP Configuration**
3.   Toggle "browser features"

Once configured, users in your organization will have access to browser tools based on your MCP allowlist or denylist settings.

### [Origin allowlist](https://www.cursor.com/docs/agent/tools/browser#origin-allowlist)

Enterprise administrators can configure an origin allowlist that restricts which sites the agent can automatically navigate to and where MCP tools can run. This provides granular control over browser access for security and compliance.

#### [Configuration](https://www.cursor.com/docs/agent/tools/browser#configuration)

To configure the origin allowlist:

1.   Navigate to your [Admin Dashboard](https://cursor.com/dashboard/settings)
2.   Go to **MCP Configuration**
3.   Ensure **Enable Browser Automation Features (v2.0+)** is enabled
4.   Under **Browser Origin Allowlist (v2.1+)**, click **Add Origin**
5.   Enter the origins you want to allow (e.g., `*`, `http://localhost:3000`, `https://internal.example.com`)

#### [Behavior](https://www.cursor.com/docs/agent/tools/browser#behavior)

When an origin allowlist is configured:

*   **Automatic navigation**: The agent can only use the `browser_navigate` tool to visit URLs matching origins in the allowlist
*   **MCP tool execution**: MCP tools can only run on origins that are in the allowlist
*   **Manual navigation**: Users can still manually navigate the browser to any URL, including origins outside the allowlist (useful for viewing documentation or inspecting external sites)
*   **Tool restrictions**: Once the browser is on an origin not in the allowlist, browser tools (click, type, navigate) are blocked, even if the user navigated there manually

#### [Edge cases](https://www.cursor.com/docs/agent/tools/browser#edge-cases)

The origin allowlist provides best-effort protection. Be aware of these behaviors:

*   **Link navigation**: If the agent clicks a link on an allowed domain that navigates to a non-allowed origin, the navigation will succeed
*   **Redirects**: If the agent navigates to an allowed origin that subsequently redirects to a non-allowed origin, the redirect will be permitted
*   **JavaScript navigation**: Client-side navigation (via `window.location` or similar) from an allowed origin to a non-allowed origin will succeed
