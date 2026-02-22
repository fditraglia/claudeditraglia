# Building an AI Executive Assistant

!!! warning "Early Preview"
    This site is growing weekly. Current as of February 2026.

This page describes how to assemble Claude Code's individual capabilities — MCP integrations, skills, and persistent context — into something that functions as an executive assistant: a system that manages your inbox, tracks your projects, processes your meetings, and drafts your communications.

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

### 2. Meeting Processing

After every meeting, Claude extracts the important parts.

**How it works:**
- You provide a transcript (from Granola, Zoom, or manual notes)
- Claude extracts: decisions made, action items, open questions, key discussion points
- Results go to a project meeting log or Google Doc

**What you need:**
- Meeting transcripts (Granola MCP, or exported transcript files)
- A project folder or Google Doc to store the results

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

## The Honest Assessment

### What Works Well

- **Email triage** saves real time once your rules are dialed in
- **Meeting extraction** turns messy transcripts into structured records
- **Session capture** creates institutional memory that persists across sessions
- **Communication drafting** is faster than writing from scratch, especially with voice training

### What's Still Rough

- **Calendar management** is read-mostly — creating and modifying events works but isn't as smooth as reading
- **Cross-platform coordination** (e.g., linking an email to a calendar event to a project doc) requires explicit instructions each time
- **Voice training** takes iteration — Claude won't perfectly match your style on day one
- **The initial setup takes hours** — it's an investment that pays off over weeks, not immediately

### The Meta-Point

No skill or configuration is perfect on first try. The value of the EA system comes from **iterative improvement**: use it, notice what's wrong, fix it, repeat. After a month of regular use and refinement, the system works meaningfully better than it did on day one.

This is the [Build Your Own](../system/index.md) philosophy in practice.

---

## Further Reading

- **[Skill Library](skill-library.md)** — Download skills for inbox triage, session capture, and more
- **[Build Your Own](../system/index.md)** — Learn to create and refine your own skills
- **[CLAUDE.md Guide](claude-md.md)** — Configure your persistent context
