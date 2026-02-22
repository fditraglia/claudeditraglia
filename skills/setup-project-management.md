# Setup Project Management

*v1.0 — Initialize a project management system for a research project*

Initialize a comprehensive project management system for a research project, adapting to the project's existing structure and workflows.

## Overview

This skill sets up:
- Folder structure for AI collaboration and document management
- TODO.md (project tasks)
- PROJECT_INDEX.md (master resource catalog)
- .claude/CLAUDE.md (project-specific Claude instructions)
- Google Doc hub structure (if applicable)
- Meeting transcript workflow

## Instructions

### Phase 1: Discovery (DO THIS FIRST)

Before making ANY changes, thoroughly assess the current state:

1. **Explore existing folder structure**
   - List all folders and files in the project root
   - Note any existing organizational system
   - Identify where documents, data, code, and communications currently live

2. **Check for existing project documentation**
   - Look for README files, INDEX files, or similar
   - Check for existing .claude/ folder or CLAUDE.md
   - Look for any project management docs

3. **Identify existing tools and workflows**
   - Ask about: Google Docs, Overleaf, GitHub, Slack, WhatsApp groups
   - Check for existing meeting notes or transcript storage
   - Identify any automation already in place

4. **Assess data sensitivity**
   - Ask about IRB status and data handling requirements
   - Note if identifiable data exists and where it's stored

### Phase 2: Gap Analysis

Present findings:

```
## Current State Assessment

### Existing Structure
[What's already in place]

### Existing Documentation
[Project docs, READMEs, etc.]

### Existing Tools
[Integrations already being used]

### Gaps Identified
[What's missing]

### Potential Conflicts
[Where new structure differs from existing setup]
```

### Phase 3: Design Discussion

**STOP AND DISCUSS** before proceeding. Ask:

1. **Project type:**
   - **Quantitative RCT** — full folder structure with IRB, Survey Instruments, Field Materials
   - **Qualitative / Ethnographic** — replace IRB folder with Fieldwork (Interview Memos, Transcripts, Consent Forms)
   - **Theory / Writing** — minimal structure; may skip most folders
   - **Policy Brief / Report** — streamlined for non-academic deliverables
   - **Multi-method** — combines quantitative and qualitative structures

2. **Folder structure:** Keep existing naming or adopt numbered system?

3. **Central document hub:** Existing Google Doc or create new?

4. **Meeting transcripts:** Current storage method?

5. **Communication channels:** What team channels exist?

6. **Team and workflow:** Key team members, meeting cadence?

### Phase 4: Propose Customized Plan

Based on discussion, present a specific plan:

```
## Proposed Project Management Setup

### Folder Changes
- [Specific folders to create/rename/leave alone]

### Files to Create
1. AI_Collaboration/TODO.md
2. PROJECT_INDEX.md
3. .claude/CLAUDE.md

### Google Doc Structure
- [New doc or modify existing]

### What Will NOT Change
- [Explicitly list what stays the same]
```

**Ask for approval before proceeding.**

### Phase 5: Implementation

Only after approval:

1. **Create folder structure** (only new folders, don't reorganize without permission)

2. **Create TODO.md** with:
   - Project-specific tasks
   - Routing links to setup TODOs

3. **Create PROJECT_INDEX.md** with:
   - Project overview
   - Links to primary documents
   - Folder structure documentation

4. **Create .claude/CLAUDE.md** with:
   - Project overview
   - Communication channels
   - Key document links
   - Team roster
   - File paths and conventions
   - Project-specific workflows

5. **Create AI collaboration folders:**
   - `AI_Collaboration/Transcripts/`
   - `AI_Collaboration/Weekly_Reviews/`

6. **Link external sources:** If external sources are identified (shared drives, cloud storage, institutional repositories), offer to copy or link key files into the project structure. Confirm before moving or duplicating any files.

### Phase 6: Verification

1. Verify all created files are in correct locations
2. Check that paths in documentation are accurate
3. Present summary:

```
## Setup Complete

### Created
- [List files/folders created]

### Configured
- [List integrations set up]

### Next Steps
- [Manual steps needed]
```

## Key Principles

1. **Never assume** — Always explore before proposing changes
2. **Never overwrite** — Check for existing files before creating
3. **Never reorganize without permission** — Existing structure may have reasons
4. **Iterate** — Go back and forth until the plan is right
5. **Preserve what works** — Don't fix what isn't broken

## Arguments

`$ARGUMENTS` can include:
- `discover` — Only run Phases 1-2 (assessment, no changes)
- `plan` — Run through Phase 4 (stop before implementation)
- `full` — Complete setup with all phases
- `minimal` — Create only .claude/CLAUDE.md and essential config

## Examples

```
/setup-project-management discover
/setup-project-management plan
/setup-project-management
/setup-project-management minimal
```

## Customization Points

- **Folder structure:** Adapt the numbered folder system (01_Paper, 02_Presentations, etc.) to match your conventions
- **Document hub:** Configure for Google Docs, Notion, or other platforms
- **Team channels:** Add WhatsApp groups, Slack channels, or other communication tools
- **Data sensitivity:** Add IRB-specific handling rules for sensitive projects
