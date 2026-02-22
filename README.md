# Claude Blattman

**A professor's guide to building AI workflows — from chatbots to self-improving systems.**

Website: [claudeblattman.com](https://claudeblattman.com)

---

## What This Is

A free, open-source resource for non-developers who want to build real AI workflows. Three paths:

1. **The Essentials** — Tools and foundations. Chatbots done right, dictation, transcription, prompt engineering.
2. **The Toolkit** — Claude Code setup, configuration, and downloadable skills. From "what is this?" to a working system.
3. **Build Your Own** — Creating custom skills, agents, and self-improving workflows.

## Who It's For

- Academics and researchers managing multiple projects
- Professionals buried in email, meetings, and coordination
- Anyone who wants to move beyond casual chatbot use

No coding background required. Everything is built with markdown and AI tools.

## Quick Start

Visit [claudeblattman.com/quickstart](https://claudeblattman.com/quickstart/) for a 5-minute exercise that demonstrates the core principles.

## Install Skills

Skills are markdown files that add slash commands to Claude Code. Install them with:

```bash
mkdir -p ~/.claude/commands
curl -o ~/.claude/commands/done.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/done.md
```

See `skills/README.md` for the full list and bundle install instructions.

## Repo Structure

```
claudeblattman/
├── docs/               # Website source (MkDocs Material)
├── skills/             # Downloadable skill files
├── agents/             # Downloadable agent files
├── templates/          # Starter templates (CLAUDE.md, goals.yaml)
├── mkdocs.yml          # Site configuration
├── CONTRIBUTING.md     # Maintenance guide
└── LICENSE             # MIT
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to edit content, add skills, and maintain the site.

## License

MIT — use anything here however you want.

---

Built by [Chris Blattman](https://chrisblattman.com). The name is a joke. The tools are real.
