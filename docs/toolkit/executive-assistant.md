# Building an AI Executive Assistant

*Reading time: 5 minutes*

This page describes how to assemble Claude Code's individual capabilities — MCP integrations, skills, and persistent context — into something that functions as an executive assistant: a system that manages your inbox, tracks your projects, processes your meetings, and drafts your communications.

<div class="narrative-block" markdown>

:material-book-open-page-variant:{ .narrative-icon } *I started with 5,000 unread emails and used "unread" as my to-do list. A day and a half later, I had six.*
{ .narrative-teaser }

??? quote "Read the full story (4 min)"

    I started with about 5,000 unread emails going back years. This was partly because I used my unread mails like a to-do list. Any tasks that needed to be done or email that needed to be responded to, I left it unread until I got around to it. It worked well enough — I'm more on top of email than most — but the backlog was a constant low-grade source of stress. I always knew it was an inadequate system of organization. I just never had a better option.

    **The first fix was not about email — it was about reminders.** I wasn't using Google Tasks or Apple Reminders at all, which in retrospect was a mistake. After researching and testing both, I chose Apple Reminders for the flexibility and Siri integration. The key insight: emails that create to-do items should become reminders, not stay unread. That's what the triage-inbox skill does — it converts actionable emails into reminders and gets everything else out of the way.

    **The triage skill took the most iteration.** I did deep research on best practices, had Claude analyze my actual inbox patterns, and we went back and forth on filter systems. The biggest lift was distinguishing the fundamental things I had to see and respond to (which stay in my inbox) from everything else (newsletters, announcements, school emails) that I can review once a day or skip entirely.

    A word of advice if you're building something like this: this is where it helps to understand planning mode and to have Claude critically evaluate its own plans from different perspectives. I had to keep a close eye on false positives and false negatives — important emails getting auto-archived, or junk still cluttering my inbox.

    **The folder system evolved organically.** Newsletters, announcements, family, school — each got its own category. Anyone with school-aged children knows the volume: long, detailed emails where 95% is irrelevant and 5% is critical. One of my next projects is a skill that extracts just the essential information from school emails.

    **Maintenance is small and shrinking.** A few weeks in, I still occasionally train it — usually when a type of email shows up for the first time, or something that only arrives monthly. I give feedback during my daily check-in, and the system learns. It takes less attention every week.

    **The honest time savings?** Maybe an hour or two per week of direct time. Substantial, but not the main benefit. The real value is psychological. Knowing I'm on top of things. Knowing nothing will get lost. The occasional exhilaration of reaching actual inbox zero. I don't get sucked into newsletters first thing in the morning anymore. I'm more focused during the day and less likely to fall into email before bed.

    I wouldn't call inbox triage my biggest time saver. But it might be the single biggest *stress* saver. The psychological weight of knowing everything is captured in an iron-clad system of reminders — and that the check-in skill helps triage those reminders too — is pretty terrific.

</div>

---

## What "Executive Assistant" Means Here

Not a single skill or product. A *system* built from components:

| Component | What It Does | How It's Built |
|-----------|-------------|----------------|
| **Inbox triage** | Categorizes email by priority and type | Skill + Gmail MCP |
| **Meeting processing** | Extracts decisions and action items from transcripts | Skill + Granola/transcripts |
| **Project tracking** | Maintains status across multiple projects | CLAUDE.md + Google Docs MCP |
| **Communication drafting** | Writes emails, messages, and updates in your voice | CLAUDE.md voice config + skills |
| **Schedule management** | Checks calendar, identifies conflicts | Calendar MCP |

Each component works independently. You don't need all of them. Start with whichever solves your biggest pain point.

---

## The Honest Assessment

Before you invest setup time, here's what you should know:

**What works well:** Email triage saves real time once your rules are dialed in. Meeting extraction turns messy transcripts into structured records. Session capture creates institutional memory that persists across sessions. Communication drafting is faster than writing from scratch, especially with voice training.

**What's still rough:** Calendar management is read-mostly — creating and modifying events works but isn't as smooth as reading. Cross-platform coordination (e.g., linking an email to a calendar event to a project doc) requires explicit instructions each time. Voice training takes iteration — Claude won't perfectly match your style on day one. The initial setup takes hours — it's an investment that pays off over weeks, not immediately.

**The meta-point:** No skill or configuration is perfect on first try. The value comes from **iterative improvement**: use it, notice what's wrong, fix it, repeat. After a month of regular use, the system works meaningfully better than it did on day one.

---

## Prerequisites

To build EA capabilities, you need:

1. **Claude Code installed and configured** ([Install guide](install-mac.md))
2. **CLAUDE.md with your role, preferences, and projects** ([Setup guide](claude-md.md))
3. **At least Gmail MCP configured** ([MCP guide](mcp-setup.md))
4. **A few skills installed** ([Skill Library](skill-library.md))

---

## The Building Blocks

### 1. Inbox Triage

The highest-value starting point for most people. Instead of scanning hundreds of emails, Claude categorizes them and tells you what needs attention.

**How it works:**
- Claude searches your Gmail using MCP
- Applies categorization rules (from your CLAUDE.md or a skill file)
- Presents a prioritized summary: urgent, needs response, FYI, can ignore

**What you need:**
- Gmail MCP configured
- Rules for how *you* categorize email (put these in CLAUDE.md or a dedicated skill)

**Example interaction:**
```
> Triage my inbox from the last 24 hours. Flag anything from
  collaborators or about upcoming deadlines. Skip newsletters
  and automated notifications.
```

Over time, you encode your triage rules into a skill so you can just type `/triage` instead of writing the prompt each time.

!!! quote "Field note"
    My first version had too many categories. I kept refining edge cases instead of triaging email. I collapsed to a few broad buckets — urgent, needs response, FYI, skip — and accuracy jumped. Start broad. You can always split later. The other thing: watch for false negatives in the first week. I almost missed an email from a funder because the filter thought it was a newsletter. Review what's being auto-archived until you trust it.

### 2. Meeting Processing

After every meeting, Claude extracts the important parts.

**How it works:**
- You provide a transcript (from Granola, Zoom, or manual notes)
- Claude extracts: decisions made, action items, open questions, key discussion points
- Results go to a project meeting log or Google Doc

**What you need:**
- Meeting transcripts (Granola MCP, or exported transcript files)
- A project folder or Google Doc to store the results

!!! quote "Field note"
    Meetings were the second thing I automated, after inbox triage. The value isn't the transcript — it's never having to remember what was decided. I now run a skill after every meeting that extracts decisions, action items, and open questions, then appends them to the project's meeting log. The key design choice: meetings go at the TOP of the log in reverse chronological order, so the most recent context is always first.

### 3. Project Tracking

Claude maintains awareness of your projects through persistent context.

**How it works:**
- Your CLAUDE.md lists active projects with brief status
- Project-specific CLAUDE.md files (in each project folder) contain detailed context
- Skills like `/done` capture session decisions and follow-ups
- Weekly reviews pull together updates across projects

**What you need:**
- Well-maintained CLAUDE.md (global + per-project)
- Session capture habit (run `/done` at end of work sessions)

### 4. Communication Drafting

Claude writes emails, messages, and updates that sound like you.

**How it works:**
- Your CLAUDE.md includes voice and tone preferences
- Claude drafts based on context (who you're writing to, what about)
- You review and approve before sending

**What you need:**
- Voice/tone guidelines in CLAUDE.md (e.g., "Direct, friendly, no corporate jargon")
- Gmail MCP for drafting and sending

### 5. Schedule Management

Claude checks your calendar and helps manage time.

**How it works:**
- Calendar MCP reads your Google Calendar
- Claude identifies conflicts, suggests meeting times, summarizes your day

**What you need:**
- Google Calendar MCP configured

---

## How to Get Started

### Week 1: Inbox + Meeting Processing

These two give the fastest payoff. Set up:

1. Gmail MCP (if not already done)
2. Try manual inbox triage: ask Claude to "scan my last 20 emails and categorize them"
3. After your next meeting, give Claude the transcript and ask for extraction

### Week 2: Capture + Context

Build the persistence layer:

1. Install the `/done` skill from the [Skill Library](skill-library.md)
2. Run `/done` at the end of each work session
3. Review your session log after a week — notice what's useful

### Week 3: Customize + Automate

Turn successful patterns into skills:

1. If your inbox triage prompt works well, save it as a skill
2. Add voice/tone preferences to CLAUDE.md for email drafting
3. Set up project-specific CLAUDE.md files for your main projects

---

## What I Wish I'd Known

!!! tip "Lessons from building this system"

    - **Start with reminders, not email rules.** The biggest payoff was converting my "unread = to-do" habit into actual reminders. Everything else followed from that.
    - **Start with broad categories, not detailed ones.** Fewer buckets, higher accuracy. You can split later.
    - **Watch the first week carefully.** False negatives (important emails getting auto-archived) are worse than false positives. Review what's being filtered until you trust it.
    - **Use planning mode for complex skills.** Have Claude critically evaluate its own triage plans from different perspectives before you run them on real email.
    - **Real time savings: 1-2 hours/week.** But the real value is psychological — the stress of a chaotic inbox disappearing is worth more than the hours.
    - **Maintenance shrinks over time.** Early on I gave daily feedback. Now it's every few days, and mostly for new senders the system hasn't seen before.
    - **No skill is perfect on first try.** The value comes from iterative improvement — use it, notice what's wrong, fix it, repeat. After a month it works meaningfully better than day one.

---

## Further Reading

- **[Skill Library](skill-library.md)** — Download skills for inbox triage, session capture, and more
- **[Build Your Own](../system/index.md)** — Learn to create and refine your own skills
- **[CLAUDE.md Guide](claude-md.md)** — Configure your persistent context
