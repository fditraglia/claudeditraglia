# Claude Code for Newbies

**The terminal is the biggest hurdle.** Once you get past it, everything else is learnable. You don't need to be a coder — I've never written a line of code in my life, and I built everything on this site with Claude Code.

This section takes you from zero to a working system. If you want to see what the system *does* before setting it up, start with [Skills in Action](../workflows/index.md).

---

## Two Ways to Run Claude Code

Claude Code works the same way regardless of how you run it. But the *container* you run it in makes a real difference in how comfortable the experience feels.

**Option 1: Terminal.** The text-only command line that comes with your Mac or PC. Black screen, blinking cursor. This is what the install guides walk you through, and it's all you strictly need.

**Option 2: A code editor.** A code editor is an app designed for working with files — think of it as a visual wrapper around the terminal. You get a file explorer, a text editor, and a built-in terminal all in one window. You don't need to write code to use one. Claude Code runs inside the editor's terminal, and you can watch its changes appear as color-coded highlights in real time.

| | **Terminal** | **Code Editor** |
|---|---|---|
| **What it looks like** | Black screen, blinking cursor, text only | Visual file explorer on the left, editor in the center, Claude in a side panel |
| **Learning curve** | Steeper — no visual cues, easy to feel lost | Gentler — you can see your files, click to open them, and watch Claude's edits appear |
| **Best for** | Quick one-off tasks, experienced terminal users | Longer work sessions, anyone who finds a blank terminal intimidating |

### Which code editor?

The two most popular options:

- **[VS Code](https://code.visualstudio.com/)** (free) — Microsoft's code editor. Install the Claude Code extension and you're set. This is what I use.
- **[Cursor](https://cursor.com/)** ($20/month) — A code editor built specifically around AI. It's a fork of VS Code, so it looks and works almost identically, but comes with AI features baked in — including access to Claude and other models through Cursor's own subscription. You can also run Claude Code in Cursor's terminal, so the two complement each other.

**My recommendation:** I use VS Code because it's free, simple, and does everything I need. If you're already paying for Cursor, it works great too. Either way, a code editor is **optional** — everything on this site works from a plain terminal. The install guides below start with Terminal, and you can add a code editor afterward if you want.

---

## Get Started (Do These in Order)

| Step | What You'll Do | Time |
|------|---------------|------|
| **[Install — Mac](../toolkit/install-mac.md)** | Install Claude Code on macOS. No prior Terminal experience needed. | 15 min |
| **[Install — Windows](../toolkit/install-windows.md)** | Install Claude Code on Windows. No prior PowerShell experience needed. | 15 min |
| **[Set Up "VS Code"](vscode-setup.md)** *(optional)* | Install VS Code and the Claude Code extension. My preferred way to work, but not required. | 15 min |
| **[Your CLAUDE.md](../toolkit/claude-md.md)** | Create the instruction file that makes Claude Code work *for you*. | 30 min |
| **[How Claude Code Thinks](modes.md)** | Understand the three modes that control how Claude behaves. | 5 min read |
| **[MCP Setup](../toolkit/mcp-setup.md)** | Connect Claude Code to Gmail, Google Docs, Calendar, and other services. | 30-60 min |

## Learn and Browse

| Page | What You'll Learn | Time |
|------|------------------|------|
| **[How Skills Work](../toolkit/skills-guide.md)** | What skills (slash commands) are, how to use them, and how they change your workflow. | 15 min read |
| **[Skill Library](skill-reference.md)** | All downloadable skills with installation, usage, and customization details. | Browse |

---

## Prerequisites

Before starting:

1. **Have used a chatbot** (Claude.ai or ChatGPT) at least a few times
2. **Have a paid Anthropic account** (Claude Pro at minimum; Claude Max recommended for heavy use)
3. **Be comfortable with the idea of using a terminal** — you don't need experience, but you do need willingness

If you haven't used chatbots much yet, start with [The Essentials](../essentials/index.md) first.

---

## What You'll End Up With

After working through this section:

- **Claude Code installed and authenticated** on your computer
- **VS Code configured** with the Claude Code extension (optional but recommended)
- **A CLAUDE.md file** that tells Claude about your role, projects, and preferences
- **MCP integrations** connecting Claude to your email, calendar, and documents
- **A library of skills** (slash commands) that automate recurring tasks
- **A system that improves over time** as you add skills and refine your configuration

The whole setup takes a few hours spread over a couple of sessions. The time investment pays for itself within the first week of regular use.

---

## Common Issues

If you get stuck during setup, check here before giving up:

| Problem | Fix |
|---------|-----|
| **`node: command not found`** | Close Terminal and reopen it. If that doesn't work, reinstall Node.js from [nodejs.org](https://nodejs.org). |
| **`npm: command not found`** | Same as above — npm comes with Node.js. |
| **Permission errors during install** | Use `sudo npm install -g @anthropic-ai/claude-code` and enter your Mac password. |
| **Browser doesn't open for authentication** | Copy the URL from Terminal and paste it into your browser manually. |
| **Google OAuth tokens expire every 7 days** | Your Google Cloud project is in "Testing" mode. Switch to "Production" in the [Cloud Console](https://console.cloud.google.com) → Google Auth platform → Audience. See [MCP Setup](../toolkit/mcp-setup.md) for details. |
| **MCP server not responding** | Check that all paths in `~/.claude.json` are correct and absolute. Run `claude doctor` for diagnostics. Restart Claude Code. |
| **Skills don't appear after installing** | Restart Claude Code — new skills are only loaded at startup. |
| **Claude can't see my files** | Make sure you opened a folder (`File → Open Folder` in VS Code, or `cd` to the folder before running `claude`), not just a single file. |

For more help: [GitHub Issues](https://github.com/chrisblattman/claudeblattman/issues) or [GitHub Discussions](https://github.com/chrisblattman/claudeblattman/discussions).
