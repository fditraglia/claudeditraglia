# Downloads & Reference Library

Guides, templates, and reference documents from my actual setup. Download, adapt, and use freely.

**A note on dates:** AI tools evolve fast. Each resource includes a date so you know how current it is. I'll update these periodically, but always check official documentation for the latest on any specific tool.

---

## Real Examples

<div class="grid cards" markdown>

-   **A Real CLAUDE.md — Annotated**

    ---

    *Updated February 2026*

    A sanitized version of my actual production CLAUDE.md — the file that runs my daily workflow. 150+ lines of working configuration with annotations explaining why each section exists and how it evolved.

    [:octicons-arrow-right-24: View](real-claude-md-example.md) · [:octicons-arrow-right-24: Related: CLAUDE.md Setup Guide](../toolkit/claude-md.md)

</div>

---

## Prompting

<div class="grid cards" markdown>

-   **Prompt Preferences Template**

    ---

    *Updated February 2026*

    A template for documenting your personal prompting style: standard sections, common constraints, preferred output formats, and roles. Paste into a ChatGPT or Claude project as standing instructions.

    [:octicons-download-16: Download](prompt-preferences-template.md) · [:octicons-arrow-right-24: Related: Prompt Engineering](../essentials/prompting.md)

-   **Prompting Best Practices Guide**

    ---

    *Updated February 2026*

    Comprehensive reference (400+ lines) covering core principles, task-specific guidance, prompt chaining, versioning, and a quality checklist. Based on Anthropic's best practices, adapted for research and professional workflows.

    [:octicons-download-16: Download](prompting-guide.md) · [:octicons-arrow-right-24: Related: Prompt Engineering](../essentials/prompting.md)

</div>

---

## Skill Building & Architecture

<div class="grid cards" markdown>

-   **Skill Design Patterns**

    ---

    *Updated February 2026*

    Extracted patterns from 20+ production skills: policy-first architecture, config/state separation, graceful degradation, phased execution, confirmation gates. Includes archetypes (simple/medium/complex), quality checklist, and performance logging conventions.

    [:octicons-download-16: Download](skill-patterns.md) · [:octicons-arrow-right-24: Related: Building Skills](../system/building-skills.md)

-   **Agents vs Skills Decision Guide**

    ---

    *Updated February 2026*

    When to use a subagent (fresh context, parallel evaluation, QA review) versus a skill (user interaction, workflow orchestration, main context). Decision framework with practical examples.

    [:octicons-download-16: Download](agents-vs-skills-guide.md) · [:octicons-arrow-right-24: Related: Agents vs Skills](../system/agents-vs-skills.md)

</div>

---

## Deep Dives

<div class="grid cards" markdown>

-   **Claude Code Under the Hood**

    ---

    *Updated February 2026*

    How Claude Code actually works: the message stack, the agentic loop, context windows and token economics, prompt patterns, MCP architecture, and annotated skill examples. 16,000 words across 7 modules. For power users who want to understand the mechanics.

    [:octicons-download-16: Download](claude-under-the-hood.md) · [:octicons-arrow-right-24: Related: Advanced](../system/index.md)

-   **Cloud Storage Organization Guide**

    ---

    *Updated February 2026*

    Step-by-step guide to auditing and organizing files across Dropbox, Google Drive, Box, and local disk using Claude Code. Based on a real multi-day workflow. Includes prompts, scripts, and decision frameworks.

    [:octicons-download-16: Download](cloud-storage-guide.md) · [:octicons-arrow-right-24: Related: Executive Assistant](../toolkit/executive-assistant.md)

</div>

---

## Decision Guides

<div class="grid cards" markdown>

-   **Tool Limitations & When to Use What**

    ---

    *Updated February 2026*

    When to use Claude Code vs Claude.ai vs ChatGPT vs Gemini vs Perplexity. What each tool does well, what it doesn't, and when to switch. A decision framework for academics and professionals.

    [:octicons-download-16: Download](tool-limitations.md)

-   **Collected Tips & Research Log**

    ---

    *Updated February 2026*

    Curated log of 20+ deep research findings on prompting, agents, context management, and emerging patterns. Each entry includes source, insight, and action item. **Produced by the [`/tips-curate` pipeline](../system/continuous-improvement.md).**

    [:octicons-download-16: Download](collected-tips-log.md)

</div>

---

## Templates

Starter configuration files for setting up your own system. All are in the [GitHub repository](https://github.com/chrisblattman/claudeblattman/tree/main/templates).

| Template | Purpose |
|----------|---------|
| [CLAUDE.md Template](https://github.com/chrisblattman/claudeblattman/blob/main/templates/claude-md-template.md) | Starter configuration for Claude Code |
| [Email Policy Template](https://github.com/chrisblattman/claudeblattman/blob/main/templates/email-policy-template.md) | Rules for email triage autonomy |
| [Calendar Policy Template](https://github.com/chrisblattman/claudeblattman/blob/main/templates/calendar-policy-template.md) | Calendar management policies |
| [Triage Config Template](https://github.com/chrisblattman/claudeblattman/blob/main/templates/triage-config-template.md) | Email classification rules |
| [Goals Template](https://github.com/chrisblattman/claudeblattman/blob/main/templates/goals-yaml-template.yaml) | Quarterly goal tracking format |

---

## Tax Workflow Resources

Resources from the [Tax Season Case Study](../tax-workflow/index.md). Checklists, templates, and architecture patterns for document-heavy workflows.

<div class="grid cards" markdown>

-   **Academic Tax Document Checklist**

    ---

    *Updated February 2026*

    Comprehensive checklist of tax documents by income type, with "does this apply to you?" filters for each career stage (grad student, postdoc, assistant professor, senior faculty). Covers W-2s, 1099s, deductions, and international reporting triggers.

    [:octicons-arrow-right-24: View](../tax-workflow/reference/academic-tax-basics.md) · [:octicons-arrow-right-24: Related: Tax Workflow](../tax-workflow/index.md)

-   **Pre-Flight Privacy Checklist**

    ---

    *Updated February 2026*

    One-page checklist of security decisions to make before using AI tools for sensitive personal tasks. Covers data flow awareness, SSN/bank exclusion rules, tool requirements, and post-season cleanup planning.

    [:octicons-arrow-right-24: View](../tax-workflow/before-you-start/privacy-and-setup.md#pre-flight-privacy-checklist) · [:octicons-arrow-right-24: Related: Privacy & Setup](../tax-workflow/before-you-start/privacy-and-setup.md)

-   **Workflow Architecture Patterns**

    ---

    *Updated February 2026*

    Seven transferable patterns extracted from the tax workflow: Collection-Compilation-Review pipeline, tracking checklists, guided interviews, threshold gates, three-tier classification, historical comparison, and entry guides. Applicable to expense reports, grant management, insurance claims, and more.

    [:octicons-arrow-right-24: View](../tax-workflow/build-your-own/architecture-patterns.md) · [:octicons-arrow-right-24: Related: Build Your Own](../tax-workflow/build-your-own/starter-templates.md)

-   **Starter Templates**

    ---

    *Updated February 2026*

    Five downloadable skill skeletons: Document Collector, Compilation with Guided Interview, Multi-Period Review, Tracking Checklist, and Privacy Policy template. Generic versions of the tax skills, ready to adapt for non-tax domains.

    [:octicons-arrow-right-24: View](../tax-workflow/build-your-own/starter-templates.md)

-   **Post-Season Cleanup Checklist**

    ---

    *Updated February 2026*

    What to delete, archive, and rotate after filing. Covers conversation history, downloaded documents, generated spreadsheets, and credential rotation. One page you can print and check off.

    [:octicons-arrow-right-24: View](../tax-workflow/reference/when-to-get-help.md) · [:octicons-arrow-right-24: Related: Privacy & Setup](../tax-workflow/before-you-start/privacy-and-setup.md)

</div>

---

## Keeping These Current

These resources reflect my setup as of the dates shown. AI tools change fast — what works today may have better approaches tomorrow. I review and update these periodically. If something seems outdated, [let me know](mailto:claudeblattman+feedback@gmail.com).
