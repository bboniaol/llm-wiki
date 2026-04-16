# Braintrust online scoring / score production traces via r.jina.ai

- Original URL: https://www.braintrust.dev/docs/evaluate/score-online
- Capture method: r.jina.ai mirror
- Captured at: 2026-04-16

---

Title: Score production traces - Braintrust

URL Source: https://www.braintrust.dev/docs/evaluate/score-online

Markdown Content:
Online scoring evaluates production traces automatically as they’re logged, running evaluations asynchronously in the background to provide continuous quality monitoring without affecting your application’s latency or performance.This enables you to:

*   Monitor quality continuously across all production traffic
*   Catch regressions immediately when they occur
*   Evaluate at scale without manual intervention
*   Get insights into real user interactions and edge cases

## Create scoring rules

Online scoring rules are defined at the project level and specify which scorers to run, how often, and on which logs. Once configured, these rules automatically evaluate production traces as they arrive.

*   UI 
*   SDK 

In the Braintrust UI, create a scoring rule in project settings, when setting up a scorer, when testing a scorer, or from the scorers list.

*   **Project settings**: Go to **Settings >[Automations](https://www.braintrust.dev/app/~/configuration/automations)** and click **+ Create rule**.See [Manage projects](https://www.braintrust.dev/docs/admin/projects#set-up-online-scoring) for more details.
*   **Scorer setup**: When creating or editing a scorer, click **Automations** and either select an existing scoring rule or create a new rule. This workflow allows you to configure both the scorer and its scoring rules together.See [Write scorers](https://www.braintrust.dev/docs/evaluate/write-scorers) for more details.
*   **Scorer testing**: When testing a scorer with logs in the **Run** section, filter logs to find relevant examples, then click **Automations** to create a new online scoring rule with filters automatically prepopulated from your current log filters. This enables rapid iteration from logs to scoring rules.See [Test with logs](https://www.braintrust.dev/docs/evaluate/write-scorers#test-with-logs) for more details.
*   **Scorers list**: On the [**Scorers**](https://www.braintrust.dev/app/~/scorers) page, select one or more scorers and click **Create automation** to open the rule creation dialog with the selected scorers pre-filled.See [Write scorers](https://www.braintrust.dev/docs/evaluate/write-scorers) for more details.

Create scorers using the SDK, then configure online scoring rules in the UI:

1.   [Write and push your scorer](https://www.braintrust.dev/docs/evaluate/write-scorers#create-scorers) to Braintrust.
2.   In the UI, go to **Settings**>**Project**>**Automations**.
3.   Click **+ Create rule**, select your scorer, and configure when it runs.

## Rule parameters

Configure each rule with:

*   **Rule name**: Unique identifier.
*   **Description**: Explanation of the rule’s purpose.
*   **Project**: Select which project the rule belongs to. When creating from a scorer page, you can choose any project.
*   **Scorers**: Choose from [autoevals](https://github.com/braintrustdata/autoevals) or custom scorers from the current project or any other project in your organization. When creating from a scorer page, the current scorer is automatically selected.
*   **Sampling rate**: Percentage of logs to evaluate (e.g., 10% for high-volume apps).
*   **Scope**: Choose the evaluation scope:
    *   **Trace** (default): Evaluates entire execution traces. The scorer runs once per trace and can access all spans and conversation history via `trace.getThread()` and `trace.getSpans()`. Use trace scope for [trace-level scorers](https://www.braintrust.dev/docs/evaluate/write-scorers#score-traces) that assess multi-turn conversations or multi-step workflows.
    *   **Span**: Evaluates individual spans. Each matching span is scored independently.

*   **Apply to spans** (span scope only): When using span scope, choose which spans to score:
    *   Root spans toggle: Score root spans (top-level spans with no parent)
    *   Span names: Score spans with specific names (comma-separated list)

If both are enabled, spans matching either criterion are scored. If neither is enabled, all spans that pass the SQL filter are scored.
*   **SQL filter**: Filter spans based on input, output, metadata, etc., using a [SQL filter clause](https://www.braintrust.dev/docs/reference/sql#filter).

## View scoring results

Scores appear automatically in your logs. Each scored span shows:

*   Score value (0-1 or 0-100 depending on scorer)
*   Scoring span containing evaluation details
*   Scorer name that generated the result

![Image 1: Scoring span](https://mintcdn.com/braintrust/e0-dTi9KCLeMOpZ4/images/cookbook/assets/Realtime/scoring-span.png?fit=max&auto=format&n=e0-dTi9KCLeMOpZ4&q=85&s=9bd610b169cf14f2ab57775781c5a867)

## Score manually

To apply scorers to historical logs:

*   **Specific logs**: Select logs and use **Score** to apply chosen scorers
*   **Individual logs**: Open any log and use **Score** in the trace view
*   **Filtered logs**: Filter logs to narrow your view, then use **Score existing logs** under **Automations** to apply scorers to recent logs matching your filters

## Best practices

**Choose sampling rates wisely**: High-volume applications should use lower rates (1-10%) to manage costs. Low-volume or critical applications can use higher rates (50-100%) for comprehensive coverage.**Complement offline evaluation**: Use online scoring to validate experiment results in production, monitor deployed changes, and identify new test cases from real interactions.**Consider scorer costs**: LLM-as-a-judge scorers have higher latency and costs than code-based alternatives. Factor this into your sampling rate decisions.**Choose the right scope**: Use span scope for evaluating individual operations or outputs. Use trace scope for evaluating multi-turn conversations, overall workflow completion, or when your scorer needs access to the full execution context.

## Troubleshoot issues

### Low or inconsistent scores

*   Review scorer logic to ensure criteria match expectations.
*   Verify scorers receive the expected data structure.
*   Test scorer behavior on controlled inputs.
*   Make LLM-as-a-judge criteria more specific.

### Missing scores

*   Check **Apply to spans** settings to ensure correct span types are targeted (root spans or specific span names).
*   Verify logs pass the SQL filter clause. Confirm your logs’ data (input, output, metadata) matches the filter criteria.
*   Confirm sampling rate isn’t too low for your traffic volume.
*   Ensure API key or service token has proper permissions (Read and Update on project and project logs). If using scorers from other projects, ensure permissions on those projects as well.
*   Verify span data is complete when `span.end()` is called: 
    *   Online scoring triggers when `span.end()` is called (or automatically when using `wrapTraced()` in TypeScript or `@traced` decorator in Python)
    *   The SQL filter clause evaluates only the data present at the moment `span.end()` is called
    *   If a span is updated after calling `end()` (e.g., logging output after ending), the update won’t be evaluated by the filter. For example, if your filter requires `output IS NOT NULL` but output is logged after `span.end()`, the span won’t be scored

## Next steps

*   [Create dashboards](https://www.braintrust.dev/docs/observe/dashboards) to monitor score trends
*   [Build datasets](https://www.braintrust.dev/docs/annotate/datasets) from scored production traces
*   [Run experiments](https://www.braintrust.dev/docs/evaluate/run-evaluations) to validate scoring criteria
*   Learn about [creating scorers](https://www.braintrust.dev/docs/evaluate/write-scorers)
