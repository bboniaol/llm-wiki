# Langfuse evaluation overview via r.jina.ai

- Original URL: https://langfuse.com/docs/evaluation/overview
- Capture method: r.jina.ai mirror
- Captured at: 2026-04-16

---

Title: Evaluation of LLM Applications - Langfuse

URL Source: https://langfuse.com/docs/evaluation/overview

Markdown Content:
# Evaluation of LLM Applications - Langfuse

We value your privacy

We use cookies to enhance your browsing experience, serve personalised ads or content, and analyse our traffic. By clicking "Accept All", you consent to our use of cookies.

Customise Reject All Accept All

Customise Consent Preferences![Image 1](https://cdn-cookieyes.com/assets/images/close.svg)

We use cookies to help you navigate efficiently and perform certain functions. You will find detailed information about all cookies under each consent category below.

The cookies that are categorised as "Necessary" are stored on your browser as they are essential for enabling the basic functionalities of the site. ...Show more

Necessary Always Active

Necessary cookies are required to enable the basic features of this site, such as providing secure log-in or adjusting your consent preferences. These cookies do not store any personally identifiable data.

*   Cookie __Secure-next-auth.csrf-token.EU 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __Secure-next-auth.callback-url.EU 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __Secure-next-auth.csrf-token.US 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __Secure-next-auth.callback-url.US 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __cf_bm 
*   Duration 1 hour 
*   Description This cookie, set by Cloudflare, is used to support Cloudflare Bot Management.  

*   Cookie __hssrc 
*   Duration session 
*   Description This cookie is set by Hubspot whenever it changes the session cookie. The __hssrc cookie set to 1 indicates that the user has restarted the browser, and if the cookie does not exist, it is assumed to be a new session. 

*   Cookie __hssc 
*   Duration 1 hour 
*   Description HubSpot sets this cookie to keep track of sessions and to determine if HubSpot should increment the session number and timestamps in the __hstc cookie. 

*   Cookie _cfuvid 
*   Duration session 
*   Description Calendly sets this cookie to track users across sessions to optimize user experience by maintaining session consistency and providing personalized services 

*   Cookie yt.innertube::nextId 
*   Duration Never Expires 
*   Description YouTube sets this cookie to register a unique ID to store data on what videos from YouTube the user has seen. 

*   Cookie yt.innertube::requests 
*   Duration Never Expires 
*   Description YouTube sets this cookie to register a unique ID to store data on what videos from YouTube the user has seen. 

*   Cookie yt-remote-connected-devices 
*   Duration Never Expires 
*   Description YouTube sets this cookie to store the user's video preferences using embedded YouTube videos. 

*   Cookie ytidb::LAST_RESULT_ENTRY_KEY 
*   Duration Never Expires 
*   Description The cookie ytidb::LAST_RESULT_ENTRY_KEY is used by YouTube to store the last search result entry that was clicked by the user. This information is used to improve the user experience by providing more relevant search results in the future. 

*   Cookie yt-remote-device-id 
*   Duration Never Expires 
*   Description YouTube sets this cookie to store the user's video preferences using embedded YouTube videos. 

*   Cookie yt-remote-session-name 
*   Duration session 
*   Description The yt-remote-session-name cookie is used by YouTube to store the user's video player preferences using embedded YouTube video. 

*   Cookie yt-remote-fast-check-period 
*   Duration session 
*   Description The yt-remote-fast-check-period cookie is used by YouTube to store the user's video player preferences for embedded YouTube videos. 

*   Cookie yt-remote-session-app 
*   Duration session 
*   Description The yt-remote-session-app cookie is used by YouTube to store user preferences and information about the interface of the embedded YouTube video player. 

*   Cookie yt-remote-cast-available 
*   Duration session 
*   Description The yt-remote-cast-available cookie is used to store the user's preferences regarding whether casting is available on their YouTube video player. 

*   Cookie yt-remote-cast-installed 
*   Duration session 
*   Description The yt-remote-cast-installed cookie is used to store the user's video player preferences using embedded YouTube video. 

*   Cookie cookieyes-consent 
*   Duration 1 year 
*   Description CookieYes sets this cookie to remember users' consent preferences so that their preferences are respected on subsequent visits to this site. It does not collect or store any personal information about the site visitors. 

*   Cookie __Secure-next-auth.csrf-token.HIPAA 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __Secure-next-auth.callback-url.HIPAA 
*   Duration session 
*   Description Description is currently not available. 

*   Cookie __Secure-ROLLOUT_TOKEN 
*   Duration 6 months 
*   Description Description is currently not available. 

*   Cookie __Secure-YEC 
*   Duration past 
*   Description Description is currently not available. 

*   Cookie VISITOR_PRIVACY_METADATA 
*   Duration 6 months 
*   Description YouTube sets this cookie to store the user's cookie consent state for the current domain.  

*   Cookie VISITOR_INFO1_LIVE 
*   Duration 6 months 
*   Description A cookie set by YouTube to measure bandwidth that determines whether the user gets the new or old player interface. 

Functional

- [x] 

Functional cookies help perform certain functionalities like sharing the content of the website on social media platforms, collecting feedback, and other third-party features.

*   Cookie inkeepUsagePreferences_userId 
*   Duration 1 year 
*   Description Description is currently not available. 

Analytics

- [x] 

Analytical cookies are used to understand how visitors interact with the website. These cookies help provide information on metrics such as the number of visitors, bounce rate, traffic source, etc.

*   Cookie ph_phc_zkMwFajk8ehObUlMth0D7DtPItFnxETi3lmSvyQDrwB_posthog 
*   Duration 1 year 
*   Description Description is currently not available. 

*   Cookie __hstc 
*   Duration 6 months 
*   Description Hubspot set this main cookie for tracking visitors. It contains the domain, initial timestamp (first visit), last timestamp (last visit), current timestamp (this visit), and session number (increments for each subsequent session). 

*   Cookie hubspotutk 
*   Duration 6 months 
*   Description HubSpot sets this cookie to keep track of the visitors to the website. This cookie is passed to HubSpot on form submission and used when deduplicating contacts. 

*   Cookie YSC 
*   Duration session 
*   Description YSC cookie is set by Youtube and is used to track the views of embedded videos on Youtube pages. 

Performance

Performance cookies are used to understand and analyse the key performance indexes of the website which helps in delivering a better user experience for the visitors.

No cookies to display.

Advertisement

Advertisement cookies are used to provide visitors with customised advertisements based on the pages you visited previously and to analyse the effectiveness of the ad campaigns.

No cookies to display.

Uncategorised

Other uncategorised cookies are those that are being analysed and have not been classified into a category as yet.

No cookies to display.

Reject All Save My Preferences Accept All

[Langfuse just got faster →Langfuse just got faster – read about Fast Preview (v4) →](https://langfuse.com/docs/v4)

[![Image 2: Langfuse Logo](https://langfuse.com/langfuse-wordart-white.svg)![Image 3: Langfuse Logo](https://langfuse.com/langfuse-wordart.svg)](https://langfuse.com/)

[Hiring in Europe and SF Looking for GOATS!](https://langfuse.com/careers)

Product Resources[Docs](https://langfuse.com/docs)[Changelog](https://langfuse.com/changelog)[Pricing](https://langfuse.com/pricing)

Product

[Overview](https://langfuse.com/docs)[LLM Observability](https://langfuse.com/docs/observability/overview)[Prompt Management](https://langfuse.com/docs/prompt-management/overview)[Evaluation](https://langfuse.com/docs/evaluation/overview)[Metrics](https://langfuse.com/docs/metrics/overview)

Resources

Docs

Self Hosting

Guides

Integrations

FAQ

Handbook

[Changelog](https://langfuse.com/changelog)[Pricing](https://langfuse.com/pricing)

Library

Security & Compliance

[](https://x.com/langfuse)[25K](https://github.com/langfuse/langfuse "GitHub Repository")[Get Demo](https://langfuse.com/talk-to-us)[App Sign Up](https://us.cloud.langfuse.com/)

[](https://langfuse.com/)

[Docs](https://langfuse.com/docs)[Integrations](https://langfuse.com/integrations)[Self Hosting](https://langfuse.com/self-hosting)[Guides](https://langfuse.com/guides)[AI Engineering Library](https://langfuse.com/library)

[Overview](https://langfuse.com/docs)[Example Project](https://langfuse.com/docs/demo)[Ask AI](https://langfuse.com/docs/ask-ai)
Get Started

[Start Tracing](https://langfuse.com/docs/observability/get-started)[Use Prompt Management](https://langfuse.com/docs/prompt-management/get-started)[Set up Evals](https://langfuse.com/docs/evaluation/overview)
Products

Observability

Prompt Management

Evaluation

Platform

Metrics

API & Data Platform

Administration

[Security & Guardrails](https://langfuse.com/docs/security-and-guardrails)
More

[Glossary](https://langfuse.com/docs/glossary)[Roadmap](https://langfuse.com/docs/roadmap)[Langfuse Fast Preview: Faster and Observations-First](https://langfuse.com/docs/v4)[Docs MCP Server](https://langfuse.com/docs/docs-mcp)

SDK & API References

[Security & Compliance ↗](https://langfuse.com/security)[Support ↗](https://langfuse.com/support)

[](https://github.com/langfuse/langfuse-docs)

Set up Evals Evaluation Overview

Docs[Set up Evals](https://langfuse.com/docs/evaluation/overview)

Copy page

# [Evaluation Overview](https://langfuse.com/docs/evaluation/overview#evaluation-overview)

Evals give you a repeatable check of your LLM application's behavior. You **replace guesswork with data**.

They also help you **catch regressions before you ship a change**. You tweak a prompt to handle an edge case, run your eval, and immediately see if it affected the behavior of your application in unintended ways.

[**Watch this walkthrough**](https://langfuse.com/watch-demo?tab=evaluation) of Langfuse Evaluation and how to use it to improve your LLM application.

## [Getting Started](https://langfuse.com/docs/evaluation/overview#getting-started)

If you're new to LLM evaluation, start by exploring the [Concepts](https://langfuse.com/docs/evaluation/core-concepts) page. There's a lot to uncover, and going through the concepts before diving in will speed up your learning curve.

Once you know what you want to do, you can:

*   [Create a dataset](https://langfuse.com/docs/evaluation/experiments/datasets) to measure your LLM application's performance consistently
*   [Run an experiment](https://langfuse.com/docs/evaluation/core-concepts#experiments) get an overview of how your application is doing
*   [Set up a live evaluator](https://langfuse.com/docs/evaluation/evaluation-methods/llm-as-a-judge) to monitor your live traces

Looking for something specific? Take a look under _Evaluation Methods_ and _Experiments_ for guides on specific topics.

## [GitHub Discussions](https://langfuse.com/docs/evaluation/overview#github-discussions)

[How to evaluate existing traces?](https://github.com/orgs/langfuse/discussions/9552 "Langfuse Support: How to evaluate existing traces?")[Ability to View Score Comments in LangFuse UI](https://github.com/orgs/langfuse/discussions/9504 "Langfuse Support: Ability to View Score Comments in LangFuse UI")[Update dataset scores](https://github.com/orgs/langfuse/discussions/9377 "Langfuse Support: Update dataset scores")[Dataset Experiment via SDK](https://github.com/orgs/langfuse/discussions/9376 "Langfuse Support: Dataset Experiment via SDK")[CreateScoreRequest.DatasetRunId not working?](https://github.com/orgs/langfuse/discussions/9363 "Langfuse Support: CreateScoreRequest.DatasetRunId not working?")[How to fetch the traces using custom fields ingested in dashboard?](https://github.com/orgs/langfuse/discussions/9352 "Langfuse Support: How to fetch the traces using custom fields ingested in dashboard?")[Is it possible for LLM-as-a-Judge to produce a categorical answer?](https://github.com/orgs/langfuse/discussions/9325 "Langfuse Support: Is it possible for LLM-as-a-Judge to produce a categorical answer?")[How to link an AI-as-judge eval to a specific observation in Langfuse Cloud](https://github.com/orgs/langfuse/discussions/9248 "Langfuse Support: How to link an AI-as-judge eval to a specific observation in Langfuse Cloud")[Given a sessionId, how can i fetch the scores associated with that session ( not its traces)](https://github.com/orgs/langfuse/discussions/9160 "Langfuse Support: Given a sessionId, how can i fetch the scores associated with that session ( not its traces)")[Scores – limitations and improvement suggestions](https://github.com/orgs/langfuse/discussions/9125 "Langfuse Support: Scores – limitations and improvement suggestions")[API - /scores not respecting value when operator '='](https://github.com/orgs/langfuse/discussions/8770 "Langfuse Support: API - /scores not respecting value when operator '='")[How to get experiment run scores programmatically?](https://github.com/orgs/langfuse/discussions/8590 "Langfuse Support: How to get experiment run scores programmatically?")[Scoring using span object or using trace id doesn't seem to work in remote runs for dataset evaluations](https://github.com/orgs/langfuse/discussions/8556 "Langfuse Support: Scoring using span object or using trace id doesn't seem to work in remote runs for dataset evaluations")[Getting scores efficiently via API for analytics purposes](https://github.com/orgs/langfuse/discussions/8520 "Langfuse Support: Getting scores efficiently via API for analytics purposes")[How to Recalculate Total Score on Dashboard After Updating User-Defined Model?](https://github.com/orgs/langfuse/discussions/8375 "Langfuse Support: How to Recalculate Total Score on Dashboard After Updating User-Defined Model?")[How to filter by Categorical Scores in custom dashboard?](https://github.com/orgs/langfuse/discussions/8356 "Langfuse Support: How to filter by Categorical Scores in custom dashboard?")[Using scores in data sets from the SDK?](https://github.com/orgs/langfuse/discussions/6016 "Langfuse Support: Using scores in data sets from the SDK?")[Deleting Metrics for Langfuse](https://github.com/orgs/langfuse/discussions/5849 "Langfuse Support: Deleting Metrics for Langfuse")[Score function](https://github.com/orgs/langfuse/discussions/5257 "Langfuse Support: Score function")[Support for Metric Calculation (Precision@K, Recall@K) and Adding Custom Metrics Use Case Overview](https://github.com/orgs/langfuse/discussions/5215 "Langfuse Support: Support for Metric Calculation (Precision@K, Recall@K) and Adding Custom Metrics Use Case Overview")[How to update a score?](https://github.com/orgs/langfuse/discussions/4178 "Langfuse Support: How to update a score?")[Filter Categorical Score Values](https://github.com/orgs/langfuse/discussions/3797 "Langfuse Support: Filter Categorical Score Values")[Configuring Evaluation with "Correctness" Template & Python Code Invocation](https://github.com/orgs/langfuse/discussions/3410 "Langfuse Support: Configuring Evaluation with \"Correctness\" Template & Python Code Invocation")[Getting all traces logged in a timerange for custom scoring](https://github.com/orgs/langfuse/discussions/2481 "Langfuse Support: Getting all traces logged in a timerange for custom scoring")[Scoring a trace after the LLM chain returns](https://github.com/orgs/langfuse/discussions/1610 "Langfuse Support: Scoring a trace after the LLM chain returns")[Update/delete score using python sdk](https://github.com/orgs/langfuse/discussions/1486 "Langfuse Support: Update/delete score using python sdk")[Request feature: allow Scores to be able to filter with trace's "Release"](https://github.com/orgs/langfuse/discussions/9594 "Langfuse Ideas: Request feature: allow Scores to be able to filter with trace's \"Release\"")[feat(experiment-compare): highlighting or ability to sort by detected differences between scores would be nice for locating significant changes](https://github.com/orgs/langfuse/discussions/9574 "Langfuse Ideas: feat(experiment-compare): highlighting or ability to sort by detected differences between scores would be nice for locating significant changes")[Aggregate boolean scores as success ratio](https://github.com/orgs/langfuse/discussions/9543 "Langfuse Ideas: Aggregate boolean scores as success ratio")[Add UPDATE (PATCH) method for Score Configs in Python SDK v3 and DELETE endpoint in API](https://github.com/orgs/langfuse/discussions/9453 "Langfuse Ideas: Add UPDATE (PATCH) method for Score Configs in Python SDK v3 and DELETE endpoint in API")[Allow getting evaluator ID from score Object created by LLM-as-a-Judge evaluator](https://github.com/orgs/langfuse/discussions/9446 "Langfuse Ideas: Allow getting evaluator ID from score Object created by LLM-as-a-Judge evaluator")[Given a sessionId, if we can FETCH the scores ( via api/sdk) associated with that session ( not its traces)](https://github.com/orgs/langfuse/discussions/9166 "Langfuse Ideas: Given a sessionId, if we can FETCH the scores ( via api/sdk) associated with that session ( not its traces)")[Python SDK: Pass ScoreConfig instead of config_id when creating scores](https://github.com/orgs/langfuse/discussions/8623 "Langfuse Ideas: Python SDK: Pass ScoreConfig instead of config_id when creating scores")[[Langfuse Cloud] Missing SessionId and Author in exported Scores](https://github.com/orgs/langfuse/discussions/8346 "Langfuse Ideas: [Langfuse Cloud] Missing SessionId and Author in exported Scores")[Score Configs: Allow editing the categories of a categorical score](https://github.com/orgs/langfuse/discussions/8259 "Langfuse Ideas: Score Configs: Allow editing the categories of a categorical score")[UI-LLM as a Jury](https://github.com/orgs/langfuse/discussions/8195 "Langfuse Ideas: UI-LLM as a Jury")[Enable Immediate Score Management for User Feedback](https://github.com/orgs/langfuse/discussions/7686 "Langfuse Ideas: Enable Immediate Score Management for User Feedback")[Filter by scores in session view](https://github.com/orgs/langfuse/discussions/7528 "Langfuse Ideas: Filter by scores in session view")[Support break lines on evaluation run tooltip hint](https://github.com/orgs/langfuse/discussions/7452 "Langfuse Ideas: Support break lines on evaluation run tooltip hint")[Support new lines when storing / displaying score comments](https://github.com/orgs/langfuse/discussions/6473 "Langfuse Ideas: Support new lines when storing / displaying score comments")[Evaluator: Filter for Scores](https://github.com/orgs/langfuse/discussions/6236 "Langfuse Ideas: Evaluator: Filter for Scores")[Code-based custom evaluators](https://github.com/orgs/langfuse/discussions/6087 "Langfuse Ideas: Code-based custom evaluators")[More scoring configurations on UI](https://github.com/orgs/langfuse/discussions/5719 "Langfuse Ideas: More scoring configurations on UI")[chart request - mirror score functionality but after filtering within trace or observation panes](https://github.com/orgs/langfuse/discussions/5426 "Langfuse Ideas: chart request - mirror score functionality but after filtering within trace or observation panes")[UI/UX: Scores Analytics - reduce interaction friction](https://github.com/orgs/langfuse/discussions/5365 "Langfuse Ideas: UI/UX: Scores Analytics - reduce interaction friction")[Update scores via the UI even if they have been created via the API](https://github.com/orgs/langfuse/discussions/5261 "Langfuse Ideas: Update scores via the UI even if they have been created via the API")[ui: ability to highlight scores](https://github.com/orgs/langfuse/discussions/4617 "Langfuse Ideas: ui: ability to highlight scores")[Sessions Table: Scores Column](https://github.com/orgs/langfuse/discussions/4120 "Langfuse Ideas: Sessions Table: Scores Column")[Scores: Conditional Annotation](https://github.com/orgs/langfuse/discussions/3842 "Langfuse Ideas: Scores: Conditional Annotation")[Scores: support for recording multiple choice selection as score value](https://github.com/orgs/langfuse/discussions/3840 "Langfuse Ideas: Scores: support for recording multiple choice selection as score value")[Source code versioning and automatic statistics caluclation from scores](https://github.com/orgs/langfuse/discussions/3412 "Langfuse Ideas: Source code versioning and automatic statistics caluclation from scores")[Optionally set timestamp when creating a score](https://github.com/orgs/langfuse/discussions/3194 "Langfuse Ideas: Optionally set timestamp when creating a score")[Session-level scores](https://github.com/orgs/langfuse/discussions/2728 "Langfuse Ideas: Session-level scores")[Scoring dataset runs, e.g. precision, recall, f-value](https://github.com/orgs/langfuse/discussions/2511 "Langfuse Ideas: Scoring dataset runs, e.g. precision, recall, f-value")[Adding userId / author to score (custom metadata)](https://github.com/orgs/langfuse/discussions/2469 "Langfuse Ideas: Adding userId / author to score (custom metadata)")[Add string data type in score config](https://github.com/orgs/langfuse/discussions/2402 "Langfuse Ideas: Add string data type in score config")[API to delete scores](https://github.com/orgs/langfuse/discussions/1133 "Langfuse Ideas: API to delete scores")

Support Ideas

Upvotes[New](https://github.com/orgs/langfuse/discussions/new/choose)

*   9 votes [Update/delete score using python sdk](https://github.com/orgs/langfuse/discussions/1486)msanand•3/25/2024•2 Resolved   
*   4 votes [Filter Categorical Score Values](https://github.com/orgs/langfuse/discussions/3797)alabrashJr•10/17/2024•3 Resolved   
*   3 votes [How to get experiment run scores programmatically?](https://github.com/orgs/langfuse/discussions/8590)anuras•8/18/2025•1 Resolved   
*   3 votes [Support for Metric Calculation (Precision@K, Recall@K) and Adding Custom Metrics Use Case Overview](https://github.com/orgs/langfuse/discussions/5215)srimantacse•1/27/2025•2 Resolved   
*   2 votes [Scores – limitations and improvement suggestions](https://github.com/orgs/langfuse/discussions/9125)enricchust•9/14/2025•1 Resolved   
*   2 votes [Scoring using span object or using trace id doesn't seem to work in remote runs for dataset evaluations](https://github.com/orgs/langfuse/discussions/8556)flabbergastedbd•8/15/2025•1   
*   1 votes [How to evaluate existing traces?](https://github.com/orgs/langfuse/discussions/9552)brnamaia•10/6/2025•73   

*   [Previous](https://langfuse.com/docs/evaluation/overview)

*   [1](https://langfuse.com/docs/evaluation/overview)
*   [2](https://langfuse.com/docs/evaluation/overview)
*   [3](https://langfuse.com/docs/evaluation/overview)
*   [4](https://langfuse.com/docs/evaluation/overview)

*   [Next](https://langfuse.com/docs/evaluation/overview)

Discussions last updated: 10/17/2025, 6:07:09 AM (4339 hours ago)

* * *

Was this page helpful?

Yes No

[Support](https://langfuse.com/support)

[Use Prompt Management Previous Page](https://langfuse.com/docs/prompt-management/get-started)[Overview Open source application tracing and observability for LLM apps. Capture traces, monitor latency, track costs, and debug issues across OpenAI, LangChain, LlamaIndex, and more.](https://langfuse.com/docs/observability/overview)

### On this page

[Evaluation Overview](https://langfuse.com/docs/evaluation/overview#evaluation-overview)[Getting Started](https://langfuse.com/docs/evaluation/overview#getting-started)[GitHub Discussions](https://langfuse.com/docs/evaluation/overview#github-discussions)

[Question? Give us feedback →](https://github.com/langfuse/langfuse-docs/issues/new?title=Feedback+for+%22Overview%22&labels=feedback)[Edit this page on GitHub](https://github.com/langfuse/langfuse-docs/edit/main/content/docs/evaluation/overview.mdx)

Contributors

[![Image 4: Lotte Verheyden](https://langfuse.com/_next/image?url=%2Fimages%2Fpeople%2Flotteverheyden.jpg&w=64&q=75) Lotte Verheyden Developer Relations](https://github.com/Lotte-Verheyden)[![Image 5: Jannik Maierhöfer](https://langfuse.com/_next/image?url=%2Fimages%2Fpeople%2Fjannikmaierhoefer.jpg&w=64&q=75) Jannik Maierhöfer Growth Engineer](https://github.com/jannikmaierhoefer)[![Image 6: Abdallah Abedraba](https://langfuse.com/_next/image?url=%2Fimages%2Fpeople%2Faabedraba.jpeg&w=64&q=75) Abdallah Abedraba Developer Advocate](https://github.com/aabedraba)... and 4 more

Product

*   [Observability](https://langfuse.com/docs/observability/overview)
*   [Prompt Management](https://langfuse.com/docs/prompt-management/overview)
*   [Evaluation](https://langfuse.com/docs/evaluation/overview)
*   [Metrics](https://langfuse.com/docs/metrics/overview)
*   [Playground](https://langfuse.com/docs/prompt-management/features/playground)
*   [Pricing](https://langfuse.com/pricing)
*   [Enterprise](https://langfuse.com/enterprise)

Developers

*   [Documentation](https://langfuse.com/docs)
*   [Self-Hosting](https://langfuse.com/self-hosting)
*   [SDKs](https://langfuse.com/docs/observability/sdk/overview)
*   [Integrations](https://langfuse.com/integrations)
*   [API Reference](https://langfuse.com/docs/api-and-data-platform/overview)
*   [Status](https://status.langfuse.com/)
*   [Talk to Us](https://langfuse.com/talk-to-us)

Resources

*   [Blog](https://langfuse.com/blog)
*   [Changelog](https://langfuse.com/changelog)
*   [Roadmap](https://langfuse.com/docs/roadmap)
*   [Interactive Demo](https://langfuse.com/docs/demo)
*   [Users](https://langfuse.com/users)
*   [AI Engineering Library](https://langfuse.com/library)
*   [Guides & Cookbooks](https://langfuse.com/guides)

Company

*   [About Us](https://langfuse.com/about)
*   [Careers](https://langfuse.com/careers)
*   [Press](https://langfuse.com/press)
*   [Security](https://langfuse.com/security)
*   [Support](https://langfuse.com/support)
*   [Open Source](https://langfuse.com/handbook/chapters/open-source)

© 2022-2026 Langfuse GmbH / Finto Technologies Inc.

[Terms](https://langfuse.com/terms)[Privacy](https://langfuse.com/privacy)[Imprint](https://langfuse.com/imprint)[Cookie Policy](https://langfuse.com/cookie-policy)

[](https://github.com/langfuse/langfuse)[](https://langfuse.com/discord)[](https://x.com/langfuse)[](https://www.youtube.com/@langfuse)[](https://www.linkedin.com/company/langfuse/)
