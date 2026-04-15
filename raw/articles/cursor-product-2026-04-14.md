Title: Cursor · Agent

URL Source: https://www.cursor.com/product

Markdown Content:
# Cursor · Agent

[Skip to content](https://www.cursor.com/product#main)

[Cursor](https://www.cursor.com/home)

*   [Product](https://www.cursor.com/product)↓

    *   [Agents](https://www.cursor.com/product)
    *   [Code Review](https://www.cursor.com/bugbot)
    *   [Cloud↗](https://cursor.com/agents)
    *   [Tab](https://www.cursor.com/product/tab)
    *   [CLI](https://www.cursor.com/cli)
    *   [Marketplace↗](https://cursor.com/marketplace)

*   [Enterprise](https://www.cursor.com/enterprise)
*   [Pricing](https://www.cursor.com/pricing)
*   [Resources](https://www.cursor.com/changelog)↓

    *   [Changelog](https://www.cursor.com/changelog)
    *   [Blog](https://www.cursor.com/blog)
    *   [Docs](https://www.cursor.com/docs)
    *   [Community](https://www.cursor.com/community)
    *   [Help↗](https://cursor.com/help)
    *   [Workshops](https://www.cursor.com/workshops)
    *   [Forum↗](https://forum.cursor.com/)
    *   [Careers](https://www.cursor.com/careers)

*   Product→
*   [Enterprise](https://www.cursor.com/enterprise) 
*   [Pricing](https://www.cursor.com/pricing) 
*   Resources→

[Sign in](https://www.cursor.com/dashboard)[Contact Contact sales](https://www.cursor.com/contact-sales?source=navbar)[Download](https://www.cursor.com/download)

1.   Agents

# Turn ideas into code

Delegate implementation to focus on higher-level direction.

[Download for macOS ⤓](https://api2.cursor.sh/updates/download/golden/darwin-universal/cursor/3.1)

[Try mobile agent →](https://www.cursor.com/agents)

This element contains an interactive demo for sighted users. It's a demonstration of Cursor's IDE showing AI-powered coding assistance features. The interface is displayed over a subtle, solid brand background.

Cursor

Get Cursor

In Progress 3

Build Landing Page

Reading docs

Analyze Tab vs Agent Usage Patterns

Fetching data

Plan Mission Control

Generating plan

Ready for Review 3

PyTorch MNIST Experiments

10m

PyTorch MNIST Experiments

Set up Cursor Rules for Dashboard

30m

Set up Cursor Rules for Dashboard

Bioinformatics Tools

45m

+135-21·Bioinformatics Tools

feature-prd.md

presence.ts

Plans feature-prd.md

Composer 2 Build

# Mission Control Interface

A grid view of all open windows as scaled previews, allowing quick selection to bring any window to front.

## Trigger

Menu item in MenuBar.tsx (View > Mission Control), hotkey F3, or double-tap desktop.

## View Behavior

Overlay existing windows into a grid of live previews with spring-based layout animations and shared element transitions.

3 Tasks

Add multiplayer mode to useAppStore.ts

Create a new MissionControlView.tsx component

Update AppManager.tsx to apply expose modes.

Add a task, ⌘K to generate...

Plan Mission Control

let's build a mission control interface, similar to the expose-style window manager on macOS

Thought 4s

Read AppManager.tsx

Searching expose patterns

Plan Composer 2

## Understands your codebase, no matter the size

Cursor deeply learns your codebase before writing a single line.

## Multiple models

Subagents run in parallel to explore your codebase, with each one using the best model for the task.

[Learn more →](https://www.cursor.com/docs/context/subagents)

Started 4 subagents

Set up model architecture

Editing files•Opus-4.6

Mission Control Interface

Building dashboard•Composer 2

Add evaluation metrics

Writing tests•GPT 5.2 Codex

Implement training loop with AMP

Pending • Gemini 3 Pro

## Codebase indexing

A custom embedding model gives agents best-in-class recall across large codebases.

[Learn more →](https://www.cursor.com/docs/context/semantic-search)

How does the payment flow handle failed transactions?

*   Searched payment retry logic 
*   Read checkout/PaymentService.ts 
*   Read lib/stripe/webhooks.ts 
*   Read db/transactions.ts 
*   Grepped handleFailedPayment 

## Team rules

Teach Cursor your preferences, from team conventions to specific architectural decisions.

[Learn more →](https://www.cursor.com/docs/context/rules)

Interactive demo with multiple windows showing Cursor's AI-powered features. The interface is displayed over a subtle, solid brand background.

---

description: Notion-inspired block architecture

globs: components/blocks/**/*

---

# Notion Block System

## Patterns

-Use Block components for all content types

-Keyboard navigation with ↑↓ to move between blocks

-Real-time collaboration via CRDT operations

-Animations use 150ms ease-out timing

-Spacing follows 4px grid: 4, 8, 12, 16, 24

-Command palette triggered with /

## Spans the full development lifecycle

Cursor supports every phase from planning to writing to reviewing code.

## Plan

For complex tasks, Cursor asks clarifying questions, builds a plan, then executes in the background.

[Learn more →](https://www.cursor.com/docs/agent/modes#plan)

How should Mission Control be opened?

1 Gesture (swipe up with 3 fingers)

2 Keyboard shortcut (e.g. CMD+F3)

3 Both keyboard and button

Skip

Continue

Add follow-up...

Plan

## Design

Visually edit any page by selecting an element to instantly rewrite, resize, or move it.

[Learn more →](https://www.cursor.com/docs/agent/browser)

Acme Labs

Software creation is changing. We are a group of researchers, engineers, and technologists inventing at the edge of what's useful and possible.

We have much to learn, try, and build.

[Join our team →](https://www.cursor.com/product#)

Tagline<span>

Shorten Tagline

Agent Composer 2

## Debug

Cursor instruments your code and uses real execution data to pinpoint the fix.

[Learn more →](https://www.cursor.com/docs/agent/modes#debug)

Chart tooltips freeze when hovering over data points.

Checked server output

Added console logs

Took screenshot

Read ChartRenderer.tsx

Found it: stale closure in the hover handler.

Tooltip.tsx+3-1

Fixed. Tooltips should update smoothly now.

## Equipped to do real engineering

Cursor edits files, runs terminal commands, searches the web, and more.

## Terminal

Run shell commands directly from Cursor, from builds to tests to installs. Sandboxed by default.

[Learn more →](https://www.cursor.com/docs/agent/terminal)

build this project

Read package.json

Ran terminal command

$npm run build

> acme-app@2.1.0 build /Users/dev/acme-app

▲ Next.js 15.1.0 (Turbopack)

Creating an optimized production build...

Compiling (1847 modules)

Collecting page data...

Generating static pages (48/48)

Finalizing page optimization...

✓ Compiled successfully in 3.8s

Build complete. Ready to deploy?

## Add context

Point Cursor at exactly what matters with @-mentions and image uploads for reference.

[Learn more →](https://www.cursor.com/docs/context/mentions)

Make drawer.tsx use vaul.emilkowal.ski and match our brand

Agent Composer 2

## Git & checkpoints

See how your code has evolved, and roll back to a previous snapshot anytime.

[Learn more →](https://www.cursor.com/docs/agent/overview#checkpoints)

Set up Next.js project

Jan 8

Add Google OAuth

Jan 12

Build canvas editor

Jan 18

Add multiplayer

Yesterday

Improve performance

3h ago

Add keyboard shortcuts

1h ago

Ship to production

Now

## Extend with tools and knowledge

Give Cursor your existing context, and add custom capabilities.

## Plugins

Browse and install community-built plugins to extend Cursor with new capabilities.

[Learn more →](https://www.cursor.com/docs/context/skills)

/add-plugin

Agent Composer 2

Add plugin

Slack Messaging Kit

Figma Visual Editor

Notion Workspace Integration

Linear Agent Excellence

GitHub Actions Suite

## Skills

Add domain knowledge to let Cursor discover and run specialized prompts and code.

[Learn more →](https://www.cursor.com/docs/context/skills)

let's /apply-notion-styleguide and /

Agent Composer 2

Skills

/fix-merge-conflicts

Resolve git conflicts automatically

/code-review

Analyze code for issues and improvements

/apply-notion-styleguide

Format code to match team standards

/pr

Create a pull request with summary

/test

Generate unit tests for selected code

## MCP

Connect external tools and data sources like GitHub and Figma directly to Cursor.

[Learn more →](https://www.cursor.com/docs/context/mcp)

![Image 1](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Fmisc%2Fasset-50ffc1473a64f3b6ee74.png&w=3840&q=70)![Image 2](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Fmisc%2Fasset-3ac50061b7174e3b941e.png&w=3840&q=70)

![Image 3](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Fmisc%2Fasset-a8b297cd3acacb16cb9e.png&w=3840&q=70)

## Everywhere you work

One agent across every surface.

## Desktop

Manual to agentic coding, in one familiar editor.

[Download →](https://www.cursor.com/download)

Interactive demo with multiple windows showing Cursor's AI-powered features. The interface is displayed over a subtle, solid brand background.

let's add a spotlight-style search

Read App.tsx, Menu.tsx

Searched⌘K shortcut handlers

Edited Search.tsx

Done. Press ⌘K to search files, actions, and settings.

Ask Cursor to plan or build anything

Agent Composer 2

## CLI

Run agents in any terminal or script.

[Learn more →](https://www.cursor.com/docs/cli/overview)

Interactive demo with multiple windows showing Cursor's AI-powered features. The interface is displayed over a subtle, solid brand background.

Cursor Agent

~/cursor/cursor-web

Analyze Tab vs Agent Usage Patterns

Help me understand how teams split their focus between the tab view and the agents panel across our workspaces.

⬢

T h o u g h t 7 s

⬢

R e v i e w e d w o r k s p a c e u s a g e e x p o r t s a n d h i s t o r i c a l e n g a g e m e n t n o t e s

I'll build an analytics toolkit that highlights tab versus agent adoption and switching behavior:

summary.py+150-0

Next I'll normalize the interaction labels and add session tagging so product can filter specific cohorts:

segmentation.py+94-0

Time to stitch everything together with a report helper that combines the key metrics:

report.py+40-0

I'll add tests to lock in the behaviour using a representative sample from last week's export:

test_usage.py+90

All set! We now track focus share, switching rates, and rolling engagement so PMs can compare tab-first and agent-first workflows in seconds.

→

Codex 5.3 High Fast

/ for commands · @ for files

## Other Surfaces

Start agents from GitHub, Slack, Linear, JetBrains IDEs, and more.

[Learn more →](https://www.cursor.com/docs/integrations/github)

Interactive demo with multiple windows showing Cursor's AI-powered features. The interface is displayed over a subtle, solid brand background.

![Image 4](https://www.cursor.com/marketing-static/_next/image?url=%2Fmarketing-static%2Fusers%2Fleerob.png&w=64&q=70&dpl=dpl_Q7Vn5XMQQNUibqWmuWsHhcFMT8hv)

leerob 5m ago

@cursor can you review this PR?

![Image 5](https://www.cursor.com/marketing-static/_next/image?url=%2Fmarketing-static%2Ficon-192x192.png&w=64&q=70&dpl=dpl_Q7Vn5XMQQNUibqWmuWsHhcFMT8hv)

cursor bot reviewed 3m ago

src/vs/workbench/composer/browser/components/ComposerUnifiedDropdown.tsx

3292

-

 {selectedMode().keybinding}

3293

+

 {composerOpenModeToggleKeybinding()}

Bug: Function Returns Object Instead of String (Logic bug)

The `composerOpenModeToggleKeybinding` is a function that needs to be called to get its value. This makes the condition always truthy.

Fix in Cursor Fix in Web

## Web & Mobile

Run cloud agents from your browser or phone.

[Learn more →](https://www.cursor.com/docs/cloud-agent/web-and-mobile)

Agent Dashboard

![Image 6](https://www.cursor.com/marketing-static/users/swhitmore.png)

Today

Vercel streaming SDK functionality

Analyzing codebase·dashboard-ui

Model selector dropdown

Planning next moves·stripe-landing

Implement agent window

2 models·agent-ui

Fix send button functionality

2 Files+26-12·agent-ui

This Week

Fix send button functionality

2 Files+26-12·agent-ui

Implement user authentication

3 Files+45-8·auth-system

Design responsive layout

5 Files+30-3·frontend

Set up database schema

4 Files+35-2·database

Create API endpoints

6 Files+50-5·backend

Ask Cursor to build, plan, fix...

## Trusted by the world's best developers

> Watching a dozen agent branches merge every day has become normal, and that freed-up velocity shows up everywhere from release cadence to bug-backlog burn-down. Cursor isn't a convenience add-on; it's a scale-multiplier for the whole org.

![Image 7](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Fcody-de-arkland-avatar.jpeg&w=96&q=70)

Cody De Arkland Senior Director, Sentry

> I will never not be amazed to be merging PRs while riding Peloton. I'm never touching a laptop again.

![Image 8](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Fnick-dobos-avatar.jpeg&w=96&q=70)

Nick Dobos Prompt Engineer, The Browser Company

> Leave it to the folks at Cursor to bring out the absolute most from the models. GPT-5.2 is an incredibly hard-working model, but to get it to work for a whole week is crazy. Building a whole browser is even crazier!

![Image 9](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Fsherwin-wu-avatar.jpg&w=96&q=70)

Sherwin Wu Head of Engineering, OpenAI

> Coding agents like Cursor have become the killer app for AI. Not only do coding agents increase the speed at which code is created, they also improve code quality.

![Image 10](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Falexis-le-quoc-avatar.webp&w=96&q=70)

Alexis Lê-Quôc CTO& Co-Founder, Datadog

> Cursor has helped me not only be more productive but also more curious and confident to explore new problem spaces. It's genuinely become an indispensable tool in my daily workflow.

![Image 11](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Flathesh-karkera-avatar.jpeg&w=96&q=70)

Lathesh Karkera Software Engineer, eBay

> More than 70% of our engineers now use Cursor, and we've seen meaningful gains in day-to-day development, faster execution on large-scale migrations, increased rate of debugging, and even faster onboarding.

![Image 12](https://www.cursor.com/marketing-static/_next/image?url=https%3A%2F%2Fptht05hbb1ssoooe.public.blob.vercel-storage.com%2Fassets%2Favatars%2Fjames-reggio-avatar.jpeg&w=96&q=70)

James Reggio CTO, Brex

## Recent highlights

[Securely indexing large codebases By securely reusing a teammate's existing index, we cut time-to-first-query from hours to seconds on the largest repos. Research·Jan 27, 2026](https://www.cursor.com/blog/secure-codebase-indexing)[Scaling long-running autonomous coding We've been experimenting with running coding agents autonomously for weeks at a time. Research·Jan 14, 2026](https://www.cursor.com/blog/scaling-agents)[Dynamic context discovery As models improve as agents, we've found success by providing fewer details up front, making it easier for the agent to pull relevant context on its own. Research·Jan 6, 2026](https://www.cursor.com/blog/dynamic-context-discovery)[View more posts →](https://www.cursor.com/blog)

## Changelog

[3.1 Apr 13, 2026 Tiled Layout and Upgraded Voice Input in the Agents Window](https://www.cursor.com/changelog/3-1)

[Apr 8, 2026 Bugbot Learned Rules and MCP Support](https://www.cursor.com/changelog/04-08-26)

[3.0 Apr 2, 2026 New Cursor Interface](https://www.cursor.com/changelog/3-0)

[Mar 25, 2026 Self-hosted Cloud Agents](https://www.cursor.com/changelog/03-25-26)

[See what's new in Cursor →](https://www.cursor.com/changelog)

## Try Cursor now.

[Download for macOS ⤓](https://api2.cursor.sh/updates/download/golden/darwin-universal/cursor/3.1)

[Try mobile agent →](https://www.cursor.com/agents)

### Product

*   [Agents](https://www.cursor.com/en-US/product)
*   [Enterprise](https://www.cursor.com/en-US/enterprise)
*   [Pricing](https://www.cursor.com/en-US/pricing)
*   [Code Review](https://www.cursor.com/en-US/bugbot)
*   [Tab](https://www.cursor.com/en-US/product/tab)
*   [CLI](https://www.cursor.com/en-US/cli)
*   [Cloud Agents](https://www.cursor.com/agents)
*   [Marketplace↗](https://cursor.com/marketplace)

### Resources

*   [Download](https://www.cursor.com/en-US/download)
*   [Changelog](https://www.cursor.com/en-US/changelog)
*   [Docs](https://www.cursor.com/docs)
*   [Learn↗](https://cursor.com/learn)
*   [Forum↗](https://forum.cursor.com/)
*   [Help↗](https://cursor.com/help)
*   [Workshops](https://www.cursor.com/en-US/workshops)
*   [Status↗](https://status.cursor.com/)

### Company

*   [Careers](https://www.cursor.com/en-US/careers)
*   [Blog](https://www.cursor.com/en-US/blog)
*   [Community](https://www.cursor.com/en-US/community)
*   [Students](https://www.cursor.com/en-US/students)
*   [Brand](https://www.cursor.com/en-US/brand)
*   [Future](https://www.cursor.com/en-US/future)
*   [Anysphere↗](https://anysphere.inc/)

### Legal

*   [Terms of Service](https://www.cursor.com/en-US/terms-of-service)
*   [Privacy Policy](https://www.cursor.com/en-US/privacy)
*   [Data Use](https://www.cursor.com/en-US/data-use)
*   [Security](https://www.cursor.com/en-US/security)

### Connect

*   [X↗](https://x.com/cursor_ai)
*   [LinkedIn↗](https://www.linkedin.com/company/cursorai)
*   [YouTube↗](https://www.youtube.com/@cursor_ai)

© 2026 [Anysphere, Inc.](https://anysphere.inc/)🛡 [SOC 2 Certified](https://www.cursor.com/en-US/security)

🖥☉☾

🌐English↓

*   English✓
*   简体中文
*   日本語
*   繁體中文
*   Español
*   Français
*   Português
*   한국어
*   Deutsch
