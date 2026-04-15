Title: Compliance and Monitoring | Cursor Docs

URL Source: https://www.cursor.com/docs/enterprise/compliance-and-monitoring

Markdown Content:
Compliance requires visibility into who did what, when, and why. This documentation covers audit logs, AI code tracking, certifications, and how to meet regulatory requirements.

## [Audit logs](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#audit-logs)

Audit logs provide a record of security events and administrative actions. Available on the [Enterprise plan](https://cursor.com/contact-sales?source=docs-audit-logs), audit logs help you meet compliance requirements and investigate security incidents.

We log the following events:

*   **Authentication events:** Logins and logouts
*   **User management:** User additions (via SSO, invite, signup, team creation, or auto-enrollment), removals, role changes, and individual spend limits
*   **API key management:** Team and user API key creation and revocation
*   **Team settings:** Team-wide and per-user spending limits, admin settings, team name changes, Slack integration settings, and repository mappings
*   **Repository management:** Repository creation, deletion, and settings updates
*   **Directory groups:** Directory group creation, updates, deletion, membership changes, and permission modifications
*   **Privacy settings:** Privacy Mode changes at user or team level
*   **Team rules:** Team rule management (including Bugbot rules) for custom workflows
*   **Team commands:** Custom command creation, updates, and deletion

We do not log agent responses or generated code content.

Instead, we recommend using [hooks](https://cursor.com/docs/hooks) to log prompts and code.

### [Accessing audit logs](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#accessing-audit-logs)

View audit logs in the [team dashboard](https://cursor.com/dashboard/audit-log). This is available on Enterprise plans, and requires admin access.

### [Streaming audit logs](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#streaming-audit-logs)

For compliance and security monitoring, stream audit logs to your existing systems:

*   SIEM systems (Splunk, Sumo Logic, Datadog, etc.)
*   Webhook endpoints for custom processing
*   S3 buckets for long-term retention
*   Log aggregators like Elasticsearch or CloudWatch

Please contact [hi@cursor.com](mailto:hi@cursor.com) if you would like to receive streaming audit logs.

### [Log format](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#log-format)

Audit logs are delivered as JSON and include metadata and event-specific fields:

The event types include:

*   `login` - User login events (web or app)
*   `logout` - User logout events
*   `add_user` - User additions (with source: `sso`, `invite`, `signup`, `createTeam`, or `autoEnroll`)
*   `remove_user` - User removals from team
*   `update_user_role` - Role changes (OWNER, ADMIN, MEMBER)
*   `user_spend_limit` - Individual user spending limit changes
*   `team_api_key` - Team API key actions (create, revoke)
*   `user_api_key` - User API key actions (create, revoke)
*   `team_settings` - Team setting modifications, including:
*   `team_hard_limit_dollars` - Team-wide spending hard limit
*   `team_hard_limit_per_user_dollars` - Per-user hard limit
*   `per_user_monthly_limit_dollars` - Monthly spending limits per user
*   `admin_only_usage_pricing` - Admin-only usage pricing settings
*   `team_admin_settings` - General admin settings
*   `team_name` - Team name changes
*   `slack_default_repo` - Slack integration repository settings
*   `slack_default_branch` - Slack integration branch settings
*   `slack_default_model` - Slack integration model settings
*   `slack_share_summary` - Slack summary sharing settings
*   `slack_share_summary_in_external_channel` - External channel sharing
*   `slack_channel_repo_mappings` - Slack channel to repository mappings
*   `team_repo` - Repository actions (create, delete, update_settings)
*   `create_directory_group` - Directory group creation
*   `update_directory_group` - Directory group updates
*   `update_directory_group_permissions` - Directory group permission changes
*   `delete_directory_group` - Directory group deletion
*   `add_user_to_directory_group` - Adding users to directory groups
*   `remove_user_from_directory_group` - Removing users from directory groups
*   `privacy_mode` - Privacy Mode changes (scope: "user" or "team")
*   `team_rule` - Team rule management (create, update, delete)
*   `bugbot_team_rule` - Bugbot-specific rule management (create, update, delete)
*   `team_command` - Custom team command management (create, update, delete)

### [Searching and filtering](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#searching-and-filtering)

Filter audit logs in the dashboard by:

*   Date range
*   Event type (authentication, user management, settings)
*   Actor (specific user)

Export filtered results to CSV for analysis or compliance reports.

## [Using hooks for compliance logging](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#using-hooks-for-compliance-logging)

Audit logs track administrative actions, but some compliance requirements need logging of development activity. Use hooks to log:

### [Prompts submitted hook](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#prompts-submitted-hook)

### [Code generated hook](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#code-generated-hook)

**Important:** Be careful logging actual code or prompts. They may contain sensitive information. Log metadata (who, when, what file) rather than content when possible.

See [Hooks](https://cursor.com/docs/hooks) for hook implementation details.

## [Certifications and compliance](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#certifications-and-compliance)

Cursor maintains compliance with industry standards, including SOC 2 Type II, GDPR, and more.

Access compliance documentation through the [Trust Center](https://trust.cursor.com/) including:

*   SOC 2 reports
*   Penetration test summaries
*   Security architecture documentation
*   Data flow diagrams

## [Responsible disclosure](https://www.cursor.com/docs/enterprise/compliance-and-monitoring#responsible-disclosure)

If you discover a security vulnerability in Cursor, report it through our responsible disclosure program:

Email [security-reports@cursor.com](mailto:security-reports@cursor.com) with the following information:

1.   A detailed description of the vulnerability
2.   Steps to reproduce the issue
3.   Any relevant screenshots or proof of concept

Audit logs are available on the Enterprise plan

Contact our team to learn more about compliance features.

[Contact Sales](https://cursor.com/contact-sales?source=docs-audit-logs)
