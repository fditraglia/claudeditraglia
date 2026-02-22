# Contributing to Claude Blattman

This guide is primarily for site maintainers, but contributions from others are welcome too.

---

## How the Site Works

The site is built with [MkDocs Material](https://squidfork.github.io/mkdocs-material/). Content is written in Markdown files inside the `docs/` folder. Every push to `main` automatically deploys the site via GitHub Actions (~2 minutes).

**The workflow:**
1. Edit a markdown file in `docs/`
2. Commit and push to `main`
3. Site updates automatically

That's it. No build step, no deploy command, no special tools required.

---

## Editing Content

### Using GitHub's Web Editor (Easiest)

1. Navigate to the file on GitHub
2. Click the pencil icon (Edit this file)
3. Make your changes
4. Write a commit message describing what you changed
5. Click "Commit changes"

The site will rebuild and deploy automatically.

### Using a Local Clone (More Powerful)

```bash
git clone https://github.com/chrisblattman/claudeblattman.git
cd claudeblattman

# Optional: preview locally
pip install mkdocs-material
mkdocs serve
# Open http://localhost:8000

# Make changes, then push
git add -A
git commit -m "Description of changes"
git push
```

---

## Adding a New Page

1. Create a new `.md` file in the appropriate `docs/` subdirectory
2. Add the page to the `nav:` section of `mkdocs.yml`
3. Commit both files

### Page Template

Every content page should start with:

```markdown
# Page Title

!!! warning "Early Preview"
    This site is growing weekly. Current as of [MONTH YEAR].

[Page content here]
```

Update the "current as of" date when you make substantive changes.

---

## Adding a New Skill to the Library

1. **Sanitize the skill** (see Sanitization Checklist below)
2. Save the generic version to `skills/[skill-name].md`
3. Add a section to `docs/toolkit/skill-library.md` following the existing format:
   - What it does
   - MCP dependencies
   - Installation instructions
   - Full skill file in a code block
   - Customization points
4. Update `mkdocs.yml` if adding a new page (not needed if just adding to skill-library.md)
5. Commit and push

---

## Adding a Resource

Append to `docs/resources.md` following the existing format:

```markdown
| [Resource Name](URL) | One-line description | YYYY-MM |
```

---

## Sanitization Checklist

**Run all four passes before pushing any skill-related changes.**

### Pass 1 — Personal Identifiers

Search for and remove any personal names, phone numbers, email addresses, or institutional details that shouldn't be public.

```bash
grep -riE "specific_names|phone_numbers|personal_emails" docs/ skills/ agents/ templates/
```

### Pass 2 — Hardcoded Paths

```bash
grep -riE "~/Dropbox|/Users/|specific_project_paths" docs/ skills/ agents/ templates/
```

Replace with generic paths like `~/Documents/` or `~/.claude/`.

### Pass 3 — Project-Specific References

```bash
grep -riE "specific_project_names|grant_names|study_locations" docs/ skills/ agents/ templates/
```

Replace with generic examples.

### Pass 4 — Manual Read-Through

Read every file in `skills/` and `agents/` end-to-end. Automated grep catches patterns but misses context (e.g., examples using real project details).

---

## Style Guidelines

- **Be concise.** Short sentences, short paragraphs.
- **Use tables** for structured information.
- **Use admonitions** for warnings, tips, and notes:
  ```markdown
  !!! tip "Pro tip"
      Content here.

  !!! warning "Heads up"
      Content here.
  ```
- **Include "current as of" dates** on any page with time-sensitive information.
- **Link generously** between pages — help readers find related content.
- **Match the voice** — accessible, direct, slightly informal. Not corporate, not condescending.

---

## Responding to GitHub Discussions

Check [Discussions](https://github.com/chrisblattman/claudeblattman/discussions) weekly for new questions. When responding:

- Be helpful and specific
- Link to relevant pages on the site
- If a question reveals missing documentation, create an issue or add the content
- Escalate to Chris if the question is about research methodology, tool recommendations, or site direction

---

## Maintenance Schedule

| Frequency | Task |
|-----------|------|
| Weekly | Check GitHub Discussions for new questions |
| Monthly | Add new resources from collected tips |
| Per skill update | Sanitize, push generic version, update skill library page |
| Quarterly | Review all content for staleness, update "current as of" dates |
