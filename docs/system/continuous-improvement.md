# Continuous Improvement

Most AI setups are static. You configure once and hope it holds. The tips pipeline makes your system learn — capturing discoveries as you encounter them and converting them into concrete changes to your configuration files.

There are a hundred ways to build a continuous improvement loop. This is the one I invented for my own workflow. It's opinionated, it's specific to Gmail and Claude Code, and it may not be your style. But the principle — *capture discoveries, filter them, and turn them into config changes* — is universal. Steal the idea and build your own version if this one doesn't fit.

---

## The idea

You're reading an article on your phone. A colleague shares a Claude Code trick over coffee. You stumble on a workflow pattern at midnight. These discoveries are valuable, but they evaporate unless you capture them *and* act on them.

The tips pipeline solves this with three steps:

1. **Capture** — Email tips to yourself, tagged `@ToSelf`. Any device, any time.
2. **Curate** — `/tips-curate` fetches those emails, researches them, quality-filters, and builds a searchable log.
3. **Integrate** — `/tips-integrate` scans the log and proposes concrete changes to your CLAUDE.md, skills, and rules files.

The result: your system gets better every two weeks, driven by your own discoveries.

---

## Prerequisites

| Requirement | Notes |
|-------------|-------|
| Claude Code installed | Required for all skills |
| Gmail MCP configured | Required for `/tips-curate`. See [MCP Setup](../toolkit/mcp-setup.md). |
| Gmail account | Used for the @ToSelf label below |
| `/tips-curate` run at least once | Required before `/tips-integrate` does anything useful |

If you haven't set up Gmail MCP yet, `/tips-curate` will report "Gmail integration unavailable" on first run. Follow the [MCP Setup guide](../toolkit/mcp-setup.md) first.

---

## Setup: The @ToSelf label

Before using `/tips-curate`, you need a Gmail label so the skill knows which emails to process.

### Create the label

1. Open Gmail in your browser
2. In the left sidebar, scroll down and click **+ Create new label**
3. Name it `@ToSelf` (the `@` prefix keeps it at the top of your label list)

### Create a filter (optional but recommended)

1. In Gmail, click the search bar filter icon (right side)
2. Set **From:** to your own email address
3. Set **Subject:** to `tip` or `@toself`
4. Click **Create filter**
5. Check **Apply the label:** and select `@ToSelf`
6. Click **Create filter**

This auto-labels any email you send yourself with "tip" in the subject. You can also manually apply the label to any email — forwarded articles, newsletters you want to process later, etc.

### The mobile workflow

The filter makes capture effortless:

- **See something interesting?** Forward the article/link to yourself
- **Have a quick idea?** Email yourself with "tip" in the subject
- **Reading a thread on X?** Forward the email notification to yourself

Claude processes everything later when you run `/tips-curate`.

---

## The pipeline

### Step 1: Capture

No skill needed. Just email yourself. The @ToSelf label collects everything.

Tips can be anything: articles, X/Twitter threads, blog posts, tool announcements, workflow ideas, or even brief notes like "try using XML tags for multi-step prompts."

### Step 2: Curate (`/tips-curate`)

This skill connects to Gmail, fetches unread @ToSelf emails, and processes each one:

- **Classifies** each email as worth-reviewing, not-relevant, or needs-manual-review
- **Enriches** — for emails with URLs, fetches the linked content for deeper analysis
- **Quality-filters** — rates each tip as High, Medium, or Low based on novelty, credibility, and actionability
- **Presents recommendations** — shows you a structured report and waits for your decision

What you approve gets appended to a searchable tips log file with tags, source attribution, and a concrete action proposal.

If the skill can't extract content from a URL (paywalled, video-only, or X.com), it flags the item as "NEEDS YOUR HELP" in the review report. You can paste the content manually or type "skip."

**MCP required:** Gmail MCP (to read and mark emails).

### Step 3: Integrate (`/tips-integrate`)

This skill scans your tips log (and optionally session follow-ups and reference packs) and generates two types of proposals:

- **Direct proposals** — Ready-to-apply edits to specific config files. Shows you the current state, the proposed change, and the rationale.
- **Investigation proposals** — Items that need more research before they become edits. These get added to your to-do list as development tasks.

Every proposal gets your approval before anything changes. The skill tracks what it has already processed so it never re-proposes the same item. Investigation proposals are written to a to-do file (`~/.claude-assistant/tasks/todo-items.md`), created automatically if it doesn't exist.

On first run, `/tips-integrate` will warn that tips have never been curated and ask whether to continue. This is expected if you haven't run `/tips-curate` yet.

**MCP required:** None. This skill is filesystem-only.

---

## Example output

### A curated tip entry

Here's what a real entry looks like in the tips log after `/tips-curate` processes it:

```markdown
## 2026-02-20

### Boris Tane's Research-Annotate-Implement Workflow [workflow] [prompting] [skill-design] [high]
- **Source:** Boris Tane (@boristane) blog post (Feb 15, 2026)
- **Insight:** 3-phase Claude Code methodology: (1) Deep research with findings
  in persistent markdown files, (2) Annotation cycle — add inline notes to
  Claude's plan correcting assumptions, rejecting approaches, injecting domain
  knowledge (repeat 1-6 times), (3) Execute with "implement it all" only after
  plan is approved. Key principle: "Never let Claude write code until you've
  reviewed a written plan."
- **Action:** Compare annotation cycle against current plan-mode workflow. The
  inline-notes-on-plan-doc pattern is more structured than chat-based iteration.
- **URL:** https://boristane.com/blog/how-i-use-claude-code/
```

### An integration proposal

When `/tips-integrate` processes that tip, it might generate:

```
────────────────────
INVESTIGATION PROPOSAL [2 of 5]
────────────────────
Source: tips
Item: Boris Tane's Research-Annotate-Implement Workflow
Task: Compare the annotation-cycle pattern (inline notes on a plan document,
  repeated 1-6 times before implementation) against current plan-mode workflow.
  Design a /plan-annotate skill or modify /review-plan to support iterative
  annotation on saved plan files.
Destination: todo-items.md (as new development task)
Rationale: Current plan mode is chat-based; structured annotation on a
  persistent document may produce better plans for complex tasks.
```

---

## When to run

| Skill | Frequency | Trigger |
|-------|-----------|---------|
| `/tips-curate` | Weekly | When you have unread @ToSelf emails. Your morning briefing can flag the count automatically. |
| `/tips-integrate` | Biweekly | After one or two curate sessions have added new entries to the log. |

You don't need to run them on a rigid schedule. The integrate skill checks when curate last ran and warns you if tips are stale.

---

## Install

Both skills are available in the [Skill Library](../setup/skill-reference.md#tips-curate-tip-curation):

- **`/tips-curate`** — requires Gmail MCP
- **`/tips-integrate`** — filesystem only, includes a reference subdirectory

See each entry in the Skill Library for installation commands.

---

## The artifact

The tips log itself is a useful reference document — a searchable, tagged collection of discoveries with source attribution. You can browse it by keyword, tag, or date.

A snapshot of my own tips log is available as a download: [Collected Tips & Research Log](../downloads/collected-tips-log.md).

---

## MCP requirements

| Skill | Gmail MCP | Other MCP |
|-------|-----------|-----------|
| `/tips-curate` | **Required** — reads and marks @ToSelf emails | None |
| `/tips-integrate` | Not needed | None — filesystem only |

You can run `/tips-integrate` without `/tips-curate` if you maintain the tips log file manually. The log format is documented in the scanning rules file included with `/tips-integrate` (see `~/.claude/commands/tips-integrate-references/scanning-rules.md` after installation).

---

## Customization

Both skills have configurable paths and behaviors:

**`/tips-curate`:**

- Tips log location (default `~/.claude-assistant/tips/collected-tips-log.md`)
- Gmail label name (default `@ToSelf`)
- Batch size (default 5)
- Quality thresholds and tag vocabulary

**`/tips-integrate`:**

- Source selection (tips, reference packs, session log — or all)
- State file location (default `~/.claude-assistant/state/integrate-state.json`)
- Target config files (CLAUDE.md, skills directory, rules directory)
- Pruning intervals (deferred items: 90 days, old change summaries: 6 months)

Edit the skill files directly to change defaults. Both files are plain markdown — find the path strings or default values in the relevant step and update them. Changes take effect on the next Claude Code restart.

---

## See also

- **[`/review-plan` — Plan Review](../workflows/first-session-skills.md#2-plan-review-review-plan)** — Stress-test any plan with structured expert critique before you build it. Pairs well with the tips pipeline: curate ideas, then review plans before implementing them.
- **[Resources & Reference Implementations](../resources.md)** — Open-source repos and frameworks that inspired this system, including chief-of-staff patterns, delegation frameworks, and community skill libraries.
- **[Skill Design Patterns](../downloads/skill-patterns.md)** — If you want to build your own skills, these patterns show how production skills are structured.
