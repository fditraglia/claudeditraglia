# MCP Setup

!!! warning "Early Preview"
    This site is growing weekly. MCP servers and their setup procedures change frequently. Current as of February 2026.

MCP (Model Context Protocol) servers extend Claude Code's capabilities by connecting to external services. Once connected, Claude can read your email, search your documents, check your calendar, and more — directly from the terminal.

---

## What MCP Does

Without MCP, Claude Code can only work with files on your computer. With MCP:

| Integration | What Claude Can Do |
|-------------|-------------------|
| **Gmail** | Search, read, draft, and send emails |
| **Google Docs** | Read and write documents |
| **Google Sheets** | Read and write spreadsheets |
| **Google Calendar** | View schedule, create events |
| **Google Drive** | Search and access files |
| **WhatsApp** | Read messages and conversations |
| **Zotero** | Search your reference library |
| **Apple apps** | Access Notes, Reminders, Calendar, Contacts |

You don't need all of these. Start with whichever service you use most (Gmail is usually the highest-value starting point) and add others as needed.

---

## How MCP Configuration Works

MCP servers are configured in a JSON file that tells Claude Code how to connect to each service:

| File | Purpose |
|------|---------|
| `~/.claude.json` | Active MCP configuration (Claude reads this) |

Each MCP server entry specifies a command to run and any required credentials (API keys, OAuth tokens).

---

## Google Workspace (Recommended First)

This single server provides access to Gmail, Google Docs, Sheets, Calendar, Drive, and Tasks. It's the highest-value MCP integration for most users.

**Repository:** [taylorwilsdon/google_workspace_mcp](https://github.com/taylorwilsdon/google_workspace_mcp)

### Prerequisites

- **Python** (3.10+) and **uv** (Python package manager)
- **Google Cloud Console** account (free)

### Setup Steps

**1. Install uv** (if you don't have it):
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**2. Clone and install the server:**
```bash
cd ~
git clone https://github.com/taylorwilsdon/google_workspace_mcp
cd google_workspace_mcp
uv sync
```

**3. Create Google OAuth credentials:**

This is the most involved step. You need to create a "project" in Google Cloud Console and enable API access.

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (or use an existing one)
3. Enable these APIs (search for each in the API Library):
   - Gmail API
   - Google Drive API
   - Google Docs API
   - Google Sheets API
   - Google Calendar API
   - Google Tasks API
4. Go to **Credentials** > **Create Credentials** > **OAuth client ID**
5. Application type: **Desktop app**
6. Download the client ID and secret

!!! tip "Testing vs Production mode"
    By default, your Google Cloud project is in "Testing" mode, which means OAuth tokens expire after 7 days and you'll need to re-authenticate weekly. To fix this, go to **Google Auth platform > Audience** in the Cloud Console and switch to "Production." This makes tokens persist indefinitely.

**4. Add to your Claude configuration:**

Add this to `~/.claude.json` under `mcpServers`:

```json
{
  "mcpServers": {
    "google_workspace": {
      "type": "stdio",
      "command": "/path/to/uv",
      "args": [
        "run", "--directory", "/path/to/google_workspace_mcp",
        "main.py", "--tools", "drive", "docs", "sheets", "gmail", "calendar", "tasks"
      ],
      "env": {
        "GOOGLE_OAUTH_CLIENT_ID": "your-client-id.apps.googleusercontent.com",
        "GOOGLE_OAUTH_CLIENT_SECRET": "your-client-secret",
        "OAUTHLIB_INSECURE_TRANSPORT": "1",
        "USER_GOOGLE_EMAIL": "your-email@gmail.com"
      }
    }
  }
}
```

Replace the paths and credentials with your actual values. To find your `uv` path: `which uv`.

**5. Restart Claude Code** and test:

```
> Search my Gmail for emails from last week
```

If Claude can read your email, the connection is working.

### Known Limitations

- Cannot create Google Doc tabs (must create manually)
- Cannot apply heading styles in Docs (use font size + bold instead)
- No suggesting mode / track changes
- Uses significant context (~26K tokens for all tools). If you hit context limits, enable only the tools you need by adjusting the `--tools` argument.

---

## WhatsApp

Read messages and search conversation history.

**Repository:** Look for `whatsapp-mcp` on GitHub (several implementations exist, using Baileys library or WhatsApp Web bridge).

### Setup Overview

1. Clone the repository and install dependencies (`npm install`)
2. Run the server once — it will display a QR code
3. Scan the QR code with your phone's WhatsApp app
4. Add to `~/.claude.json`

### Known Issues

- Session drops when your laptop sleeps — you'll need to re-scan the QR code
- Chat metadata can be stale — always fetch messages directly rather than relying on chat lists

---

## Zotero (Reference Management)

Search your Zotero library and retrieve citations.

**Package:** `mcp-zotero` (npm)

### Setup

1. Get your API key from [zotero.org/settings/keys](https://www.zotero.org/settings/keys)
2. Find your user ID on the same page

Add to `~/.claude.json`:

```json
"zotero": {
  "type": "stdio",
  "command": "npx",
  "args": ["mcp-zotero"],
  "env": {
    "ZOTERO_API_KEY": "your-api-key",
    "ZOTERO_USER_ID": "your-user-id"
  }
}
```

---

## Apple Apps (Mac Only)

Access Notes, Calendar, Contacts, Reminders, Messages, and Mail through Apple's native apps.

**Package:** `apple-mcp` (runs via Bun)

### Setup

```bash
# Install Bun first
curl -fsSL https://bun.sh/install | bash
```

Add to `~/.claude.json`:

```json
"apple-mcp": {
  "type": "stdio",
  "command": "/path/to/.bun/bin/bunx",
  "args": ["--no-cache", "apple-mcp@latest"],
  "env": {}
}
```

Replace `/path/to/` with your actual home directory path.

---

## Granola (Meeting Transcripts)

Access meeting notes and summaries from Granola.

### Setup

Requires Python 3.12+. Check the [Granola MCP GitHub repo](https://github.com/granola-ai/granola-mcp-server) for current installation instructions.

**Key limitation:** MCP provides summaries only, not full transcripts. For full transcripts, export from the Granola app to a local folder and point Claude Code at those files.

---

## Multi-Machine Setup

If you use Claude Code on multiple computers:

### What syncs (via your cloud folder):
- CLAUDE.md (your personal instructions)
- skills/commands folder
- MCP server *configuration* (the JSON)

### What stays local (per machine):
- OAuth tokens (you authenticate once per machine)
- MCP server code repositories (clone on each machine)
- `~/.claude.json` (the active config file)

### Setting Up a New Machine

1. Clone/install MCP server repositories on the new machine
2. Copy your MCP configuration to `~/.claude.json`
3. Update paths in the config to match the new machine
4. Restart Claude Code — first use will prompt for OAuth authentication

---

## Troubleshooting

**Google auth expired:** Delete the credentials file in the MCP server folder (usually `~/.google_workspace_mcp/credentials/`) and re-authenticate on next use.

**WhatsApp session dropped:** Re-run the server command and scan the QR code again.

**MCP server not responding:**
1. Check if the server command runs manually in your terminal
2. Verify all paths in `~/.claude.json` are correct and absolute
3. Restart Claude Code

**Context limits hit quickly:** Run `claude doctor` to check MCP tool context usage. Disable unused servers or reduce the `--tools` list to reclaim context space.

---

## What's Next

With MCP configured:

1. **[Learn about skills](skills-guide.md)** — Automated workflows that use your MCP connections
2. **[Browse the Skill Library](skill-library.md)** — Pre-built skills with MCP integration
