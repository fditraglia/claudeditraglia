# Resources

A curated collection of the resources, tools, and reference implementations that shaped this project. Each entry includes a brief summary of what's useful and why I found it worth your time.

Thanks to [Anup Malani](https://www.law.uchicago.edu/faculty/malani) for being my first tutor on the basics — he's the one who got me started with Claude Code and showed me what was possible.

---

## Reference Implementations

These are the projects and posts that most influenced how I built my system. If you want to see how other people are doing this, start here.

### Boris Tane — How I Use Claude Code

[:octicons-link-external-16: boristane.com](https://boristane.com/blog/how-i-use-claude-code/)

A developer's opinionated workflow with Claude Code. The Research → Plan → Annotate → Implement structure he describes became the backbone of how I think about multi-step tasks. His use of persistent markdown files as shared state between Claude and the user directly influenced my CLAUDE.md approach. Well-written and confident — one of the first posts that made me think this was more than a toy.

### Pedro Sant'Anna — Claude Code My Workflow

[:octicons-link-external-16: psantanna.com](https://psantanna.com/claude-code-my-workflow/)

The closest thing to what I'm building, but for econometrics. Pedro is an academic (economics) who built an ambitious system with 10 agents and 19 commands. His MEMORY.md pattern for persistent learning across sessions was an early influence. His research-specific slash commands showed me what was possible. Fair warning: the complexity can be overwhelming for beginners — I deliberately kept my system simpler.

### Mike Murchison — Claude Chief of Staff

[:octicons-link-external-16: GitHub](https://github.com/mimurchison/claude-chief-of-staff)

A four-pillar structure (Communicate, Learn, Deepen Relationships, Achieve Goals) for using Claude as an executive assistant. The Goals.yaml as a single source of truth, the `/gm` morning briefing command, and the idea of CLAUDE.md as "your AI operating system" all shaped my approach. My `/morning-brief` and `/checkin` skills descend directly from this repo.

### Dave Killeen — Dex

[:octicons-link-external-16: GitHub](https://github.com/davekilleen/Dex)

An extension of Murchison's Chief of Staff pattern that adds structured pillars (`pillars.yaml`), session learnings capture, and usage logging. If Murchison's repo is the architecture, Dex is the operational layer. I used it alongside the original when designing my session capture (`/done`) and goal alignment (`/goals-review`) skills. Discovered February 2026.

### Ethan Mollick — One Useful Thing

[:octicons-link-external-16: oneusefulthing.org](https://www.oneusefulthing.org/)

Ethan's blog is the gold standard for writing about AI for non-technical professionals. His Models / Apps / Harnesses framework helped me think about where different tools fit. Key insight that stuck with me: "the shift from chatbot to agent is the most important change since ChatGPT launched." If you read one person on AI and work, make it Ethan.

---

## Official Documentation

### Claude Code

[:octicons-link-external-16: docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-code)

The official setup, configuration, and usage guide. Start here if you're installing Claude Code for the first time. Covers CLAUDE.md, MCP integrations, slash commands, and the permission model. The docs have improved significantly — they're now genuinely useful as a reference.

### Anthropic Prompt Engineering Guide

[:octicons-link-external-16: docs.anthropic.com](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)

Anthropic's own guide to writing effective prompts. More technical than what I cover in my [Essentials section](essentials/prompting.md), but worth reading if you want to understand the mechanics. I adapted several patterns from here into my prompt formatting skills.

### MCP (Model Context Protocol)

[:octicons-link-external-16: modelcontextprotocol.io](https://modelcontextprotocol.io/)

The protocol that lets Claude Code talk to Gmail, Google Calendar, Google Docs, and other services. Understanding MCP is essential if you want to build integrations beyond what I've packaged. The spec is well-documented; the ecosystem is growing fast.

### MkDocs Material

[:octicons-link-external-16: squidfunk.github.io](https://squidfunk.github.io/mkdocs-material/)

The framework this site is built with. If you want to build something similar — a documentation site for your own tools or research — Material is the best option I've found. Free, well-maintained, and the configuration is all YAML (no JavaScript required).

---

## Tools Used on This Site

### AI Assistants

| Tool | What I use it for | Link |
|------|------------------|------|
| **Claude** | Primary AI — Claude Code for workflows, Claude.ai for conversations | [claude.ai](https://claude.ai) |
| **ChatGPT** | Deep Research for literature reviews and web synthesis | [chat.openai.com](https://chat.openai.com) |
| **Perplexity** | Citation-heavy factual lookups, sourced answers | [perplexity.ai](https://www.perplexity.ai/) |
| **Gemini** | Google Sheets work, video/audio analysis | [gemini.google.com](https://gemini.google.com/) |

### Productivity Tools

| Tool | What it does | Why I use it | Link |
|------|-------------|-------------|------|
| **Wispr Flow** | Dictation everywhere on Mac | I dictate most of my Claude Code input. 3-5x faster than typing for long instructions. | [wispr.flow](https://www.wispr.flow/) |
| **Granola** | Meeting transcription | Runs silently in the background. Transcripts feed into my meeting-to-action-item pipeline. | [granola.ai](https://www.granola.ai/) |
| **Zotero** | Reference management | Connected to Claude via MCP. I can search my library and pull citation details from the terminal. | [zotero.org](https://www.zotero.org/) |

### Infrastructure

| Tool | Role in this project | Link |
|------|---------------------|------|
| **GitHub** | Version control, hosting, collaboration | [github.com/chrisblattman/claudeblattman](https://github.com/chrisblattman/claudeblattman) |
| **GitHub Pages** | Free site hosting, auto-deploys on push | [pages.github.com](https://pages.github.com/) |
| **GitHub Actions** | CI/CD — builds and deploys the site | Configured in `.github/workflows/deploy.yml` |

---

## Further Reading

Resources I've found useful for thinking about AI in research and professional work.

| Resource | Why it's worth reading |
|----------|----------------------|
| [Simon Willison's Blog](https://simonwillison.net/) | The most technically literate and honest AI blog. Simon builds tools and explains what works without hype. |
| [AI for Economists (AEA)](https://www.aeaweb.org/resources/ai) | The American Economic Association's hub for AI resources in economics research. |
| [Claude Code projects on GitHub](https://github.com/topics/claude-code) | Community projects, extensions, and configurations tagged with "claude-code" on GitHub. |
| [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) | Active subreddit for Claude users. Good for troubleshooting and discovering new patterns. |
| [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Curated index of Claude Code skills, hooks, slash commands, and CLAUDE.md patterns. The closest thing to a package manager catalog for the ecosystem. |
| [LangChain Executive AI Assistant](https://github.com/langchain-ai/executive-ai-assistant) | Production-ready Gmail-monitoring AI agent framework. Their "draft-only" pattern and human-in-the-loop review influenced how I built inbox triage. |

---

## Contributing

Found a resource that should be here? Have a correction? Open an issue or start a discussion on [GitHub](https://github.com/chrisblattman/claudeblattman/discussions).
