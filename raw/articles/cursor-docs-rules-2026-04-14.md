Title: Rules | Cursor Docs

URL Source: https://www.cursor.com/docs/context/rules

Markdown Content:
Rules provide system-level instructions to Agent. They bundle prompts, scripts, and more together, making it easy to manage and share workflows across your team.

Cursor supports four types of rules:

## [How rules work](https://www.cursor.com/docs/context/rules#how-rules-work)

Large language models don't retain memory between completions. Rules provide persistent, reusable context at the prompt level.

When applied, rule contents are included at the start of the model context. This gives the AI consistent guidance for generating code, interpreting edits, or helping with workflows.

## [Project rules](https://www.cursor.com/docs/context/rules#project-rules)

Project rules live in `.cursor/rules` as markdown files and are version-controlled. They are scoped using path patterns, invoked manually, or included based on relevance.

Use project rules to:

*   Encode domain-specific knowledge about your codebase
*   Automate project-specific workflows or templates
*   Standardize style or architecture decisions

### [Rule file structure](https://www.cursor.com/docs/context/rules#rule-file-structure)

Each rule is a markdown file that you can name anything you want. Cursor supports `.md` and `.mdc` extensions. Use `.mdc` files with frontmatter to specify `description` and `globs` for more control over when rules are applied.

### [Rule anatomy](https://www.cursor.com/docs/context/rules#rule-anatomy)

Each rule is a markdown file with frontmatter metadata and content. Control how rules are applied from the type dropdown which changes properties `description`, `globs`, `alwaysApply`.

| Rule Type | Description |
| --- | --- |
| `Always Apply` | Apply to every chat session |
| `Apply Intelligently` | When Agent decides it's relevant based on description |
| `Apply to Specific Files` | When file matches a specified pattern |
| `Apply Manually` | When @-mentioned in chat (e.g., `@my-rule`) |

### [Creating a rule](https://www.cursor.com/docs/context/rules#creating-a-rule)

There are two ways to create rules:

*   **`/create-rule` in chat**: Type `/create-rule` in Agent and describe what you want. Agent generates the rule file with proper frontmatter and saves it to `.cursor/rules`.
*   **From settings**: Open `Cursor Settings > Rules, Commands` and click `+ Add Rule`. This creates a new rule file in `.cursor/rules`. From settings you can see all rules and their status.

## [Best practices](https://www.cursor.com/docs/context/rules#best-practices)

Good rules are focused, actionable, and scoped.

*   Keep rules under 500 lines
*   Split large rules into multiple, composable rules
*   Provide concrete examples or referenced files
*   Avoid vague guidance. Write rules like clear internal docs
*   Reuse rules when repeating prompts in chat
*   Reference files instead of copying their contents—this keeps rules short and prevents them from becoming stale as code changes

### [What to avoid in rules](https://www.cursor.com/docs/context/rules#what-to-avoid-in-rules)

*   **Copying entire style guides**: Use a linter instead. Agent already knows common style conventions.
*   **Documenting every possible command**: Agent knows common tools like npm, git, and pytest.
*   **Adding instructions for edge cases that rarely apply**: Keep rules focused on patterns you use frequently.
*   **Duplicating what's already in your codebase**: Point to canonical examples instead of copying code.

Check your rules into git so your whole team benefits. When you see Agent make a mistake, update the rule. You can even tag `@cursor` on a GitHub issue or PR to have Agent update the rule for you.

## [Rule file format](https://www.cursor.com/docs/context/rules#rule-file-format)

Each rule is a markdown file with frontmatter metadata and content. The frontmatter metadata is used to control how the rule is applied. The content is the rule itself.

If alwaysApply is true, the rule will be applied to every chat session. Otherwise, the description of the rule will be presented to the Cursor Agent to decide if it should be applied.

## [Examples](https://www.cursor.com/docs/context/rules#examples)

Examples are available from providers and frameworks. Community-contributed rules are found across crowdsourced collections and repositories online.

## [Team Rules](https://www.cursor.com/docs/context/rules#team-rules)

Team and [Enterprise](https://cursor.com/docs/enterprise) plans can create and enforce rules across their entire organization from the [Cursor dashboard](https://cursor.com/dashboard/team-content). Admins can configure whether or not each rule is required for team members.

Team Rules work alongside other rule types and take precedence to ensure organizational standards are maintained across all projects. They provide a powerful way to ensure consistent coding standards, practices, and workflows across your entire team without requiring individual setup or configuration.

### [Managing Team Rules](https://www.cursor.com/docs/context/rules#managing-team-rules)

Team administrators can create and manage rules directly from the Cursor dashboard:

Once team rules are created, they automatically apply to all team members and are visible in the dashboard:

### [Activation and enforcement](https://www.cursor.com/docs/context/rules#activation-and-enforcement)

*   **Enable this rule immediately**: When checked, the rule is active as soon as you create it. When unchecked, the rule is saved as a draft and does not apply until you enable it later.
*   **Enforce this rule**: When enabled, the rule is required for all team members and cannot be disabled in their Cursor settings. When not enforced, team members can toggle the rule off in `Cursor Settings → Rules` under the Team Rules section.

### [Format and how Team Rules are applied](https://www.cursor.com/docs/context/rules#format-and-how-team-rules-are-applied)

*   **Content**: Team Rules are free‑form text. They do not use the folder structure of Project Rules.
*   **Glob patterns**: Team Rules support glob patterns for file-scoped application. When a glob pattern is set (e.g., `**/*.py`), the rule only applies when matching files are in context. Rules without a glob pattern apply to every conversation.
*   **Where they apply**: When a Team Rule is enabled (and not disabled by the user, unless enforced), it is included in the model context for Agent (Chat) across all repositories and projects for that team.
*   **Precedence**: Rules are applied in this order: **Team Rules → Project Rules → User Rules**. All applicable rules are merged; earlier sources take precedence when guidance conflicts.

## [Importing Rules](https://www.cursor.com/docs/context/rules#importing-rules)

You can import rules from external sources to reuse existing configurations or bring in rules from other tools.

### [Remote rules (via GitHub)](https://www.cursor.com/docs/context/rules#remote-rules-via-github)

Import rules directly from any GitHub repository you have access to—public or private.

1.   Open **Cursor Settings → Rules, Commands**
2.   Click `+ Add Rule` next to `Project Rules`, then select Remote Rule (Github)
3.   Paste the GitHub repository URL containing the rule
4.   Cursor will pull and sync the rule into your project

Imported rules stay synced with their source repository, so updates to the remote rule are automatically reflected in your project.

## [AGENTS.md](https://www.cursor.com/docs/context/rules#agentsmd)

`AGENTS.md` is a simple markdown file for defining agent instructions. Place it in your project root as an alternative to `.cursor/rules` for straightforward use cases.

Unlike Project Rules, `AGENTS.md` is a plain markdown file without metadata or complex configurations. It's perfect for projects that need simple, readable instructions without the overhead of structured rules.

Cursor supports AGENTS.md in the project root and subdirectories.

### [Improvements](https://www.cursor.com/docs/context/rules#improvements)

## [User Rules](https://www.cursor.com/docs/context/rules#user-rules)

User Rules are global preferences defined in **Cursor Settings → Rules** that apply across all projects. They are used by Agent (Chat) and are perfect for setting preferred communication style or coding conventions:

## [FAQ](https://www.cursor.com/docs/context/rules#faq)
