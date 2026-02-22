# Set Up VS Code for Claude Code

**VS Code is a free code editor by Microsoft. You don't need to write code — it's just the container that makes Claude Code easier to use.**

Instead of a blank terminal, you get a visual file explorer, a text editor with syntax highlighting, and a built-in terminal where Claude Code runs. You can see your files on the left, edit them in the center, and talk to Claude on the right — all in one window.

!!! info "Prerequisite"
    **Claude Code must be installed first.** The VS Code extension is a wrapper around the CLI — it won't work without it. Complete [Install — Mac](../toolkit/install-mac.md) or [Install — Windows](../toolkit/install-windows.md) before continuing.

---

## Step 1: Download and Install VS Code

1. Go to [code.visualstudio.com](https://code.visualstudio.com/)
2. Click the big download button (it detects your operating system automatically)
3. **Mac**: Open the downloaded `.zip` file, then drag **Visual Studio Code** into your Applications folder
4. **Windows**: Run the downloaded installer and follow the prompts
5. Open VS Code — you'll see the Welcome screen:

![VS Code Welcome screen — the Start menu, recent projects, and walkthroughs](../images/vscode-welcome.png)

You'll see recent projects on the left and some Walkthroughs on the right. Don't worry about any of that yet.

---

## Step 2: Install the Claude Code Extension

1. Open the Extensions panel: press **Cmd+Shift+X** (Mac) or **Ctrl+Shift+X** (Windows)
2. Type **Claude Code** in the search box
3. Find the one published by **Anthropic** (look for the verified checkmark)
4. Click **Install**
5. Wait a few seconds — a new icon (a sparkle/star) will appear in your left sidebar

After installing, you may see a "Get started with Claude Code" walkthrough on the Welcome page. You can ignore it — the terminal approach below is more powerful.

---

## Step 3: Open a Project Folder

Claude Code works best when it has a folder to work in. This gives it context about your files.

1. Go to **File → Open Folder** (or press **Cmd+O** on Mac)
2. Pick a folder you want to work in — a research project, a course, anything with files you want Claude to help with
3. If VS Code asks "Do you trust the authors of the files in this folder?" — click **Yes, I trust the authors** (it's your own folder)

Here's what you'll see the first time you open a project:

![VS Code with a project open for the first time — Explorer on the left, Welcome tab in center, Chat panel on the right](../images/vscode-project-first-open.png)

Three things appeared: the **Explorer** (your folder structure) on the left, the Welcome tab in the center, and a **Chat** panel on the right. Let's clean this up.

---

## Step 4: Set Up Your Layout

The default layout isn't ideal. Here's how to arrange things so you can actually work:

### Close what you don't need

1. **Close the Chat panel** — click the **X** on the Chat tab on the right side. We'll use the terminal instead, which is more powerful.
2. **Close the Welcome tab** — click the **X** on that tab too. You can always revisit it later from **Help → Welcome**.

### Make sure the Explorer is visible

If the file explorer on the left isn't showing, click the **Explorer icon** in the top-left corner of the sidebar — it looks like a small stack of papers.

### Open the Terminal

This is where Claude Code will actually run.

- Go to **View → Terminal**, or press **Control + `** (the backtick key, above Tab)

A terminal panel will appear at the bottom of the window.

### Move the Terminal to the right (recommended)

I find it easier to read documents on the left and talk to Claude on the right:

1. **Right-click** on the word "TERMINAL" at the top of the terminal panel
2. Select **Panel Position → Right**

Now your layout is: Explorer on the far left, editor in the center, terminal on the right.

---

## Step 5: Open a File and Start Working

Click any file in the Explorer to open it in the editor. For example, if your project has a `PROJECT_INDEX.md` or a paper draft, click it to see the contents:

![VS Code with a project file open in the editor and terminal on the right](../images/vscode-project-with-file.png)

This is the layout you'll use daily: **files on the left, document in the center, Claude on the right**. As you develop proposals, papers, or any other documents, you can read and edit them directly in the center panel while Claude works alongside you in the terminal.

---

## Step 6: Launch Claude Code

In the terminal panel on the right, type:

```
claude
```

Claude Code will start up and show a welcome message. You're now ready to go. Some things to try:

- **Start a conversation** — just type what you want to do in plain English
- **Use `/prompt`** — if you want to paste a big block of text or do something complex, this formats it into a structured prompt before executing
- **Use `/resume`** — to pick up where you left off in a previous session

---

## Layout Summary

| Panel | Position | What It Shows |
|-------|----------|---------------|
| **Explorer** | Left sidebar | Your folder structure — always keep this visible |
| **Editor** | Center | Whatever file you click on — papers, project docs, LaTeX, markdown |
| **Terminal** | Right side | Where Claude Code runs — your main conversation interface |

**Tips:**

- **Drag panel borders** to resize. Give more room to whichever panel you're actively using.
- **Toggle the Explorer** with **Cmd+B** (Mac) or **Ctrl+B** (Windows) to give the editor more room.
- When Claude edits a file, VS Code highlights changes in green (added) and red (removed) — one of the biggest advantages over plain Terminal.
- You can open multiple terminals (click the **+** icon) to run Claude in one and regular commands in another.

---

## Troubleshooting

**"Claude Code" extension doesn't appear in search results**

- Make sure you're searching in the Extensions panel (**Cmd+Shift+X**), not the regular search
- Try searching for just "Claude" or "Anthropic"
- Restart VS Code and try again

**"Claude Code not found" or "CLI not installed" error**

- The extension requires the Claude Code CLI to be installed separately
- Go back to [Install — Mac](../toolkit/install-mac.md) or [Install — Windows](../toolkit/install-windows.md) and complete the installation
- After installing the CLI, restart VS Code

**Extension installed but no sparkle icon appears**

- Try restarting VS Code completely (Cmd+Q, then reopen)
- Check the bottom-left corner of VS Code for any error notifications

**Claude can't see my files**

- Make sure you've opened a folder (**File → Open Folder**), not just a single file
- Claude Code works within the folder you opened — it can't see files outside that folder

---

## Next Steps

With VS Code set up, continue with the rest of the setup:

1. **[Your CLAUDE.md](../toolkit/claude-md.md)** — Create the instruction file that makes Claude work for you
2. **[MCP Setup](../toolkit/mcp-setup.md)** — Connect Claude to Gmail, Google Docs, Calendar, and more
3. **[How Skills Work](../toolkit/skills-guide.md)** — Learn about slash commands that automate recurring tasks
