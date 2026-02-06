---
name: novel-workflow
description: Orchestrate novel writing across NovelCrafter, Scrivener, Dropbox, and Google Docs. Use when the user asks about writing workflow, tool setup, moving content between tools, managing revisions across chapters, NovelCrafter Codex/prompt configuration, POV-switching mystery setup, or genre craft for noir/thriller/mystery/suspense/horror. Triggers include "how should I set up NovelCrafter," "help me manage this revision," "how do I handle secrets in multi-POV," "best way to sync with Scrivener," or any question about efficiently using their writing toolchain.
---

# Novel Workflow

Orchestrate novel writing across multiple tools with specialized support for POV-switching mysteries and genre fiction.

## User's Toolchain

| Tool | Primary Use | Notes |
|------|-------------|-------|
| **NovelCrafter** | Prose drafting, AI generation | Max tier — all features available |
| **Scrivener** (Mac) | Official manuscript organization | Final destination for "done" prose |
| **Dropbox** | File storage/sync | |
| **Google Docs** | File storage, collaboration | |
| **Claude/ChatGPT** | Research, brainstorming, outlining | |

### Claude Skills Available

| Skill | Use For |
|-------|---------|
| **novel-outliner** | Consolidate multiple drafts/documents into structured outline (Synopsis → Act/Chapter/Scene hierarchy → Beat sheets). Handles 250k+ words via chunked processing. |
| **suno-songwriting** | AI music creation with Suno v5 |

## Core Principle: Search Before Advising

NovelCrafter and Scrivener update frequently. **Always web-search for current documentation** before giving specific feature advice:

- NovelCrafter: Search `site:novelcrafter.com` or `NovelCrafter [feature name]`
- Scrivener: Search `site:literatureandlatte.com` or `Scrivener Mac [feature name]`

Do not rely on potentially outdated knowledge. Search first, then advise.

## Workflow Phases

### Phase 1: Outlining
**Tools**: Word/Google Docs → Claude/ChatGPT → NovelCrafter

1. Initial outline in Word or Google Docs
2. Flesh out with Claude or ChatGPT (structure, plot holes, character arcs)
3. Transfer to NovelCrafter once outline is solid

**For complex outline consolidation**: If you have multiple drafts, partial outlines, or manuscript fragments that need consolidating into a single structured outline, use the **novel-outliner** skill. It produces:
- Synopsis
- Act/Chapter/Scene hierarchy with summaries
- Scene-by-scene beat sheets

**Handoff**: Copy/paste outline into NovelCrafter's scene structure

### Phase 2: Codex Setup (Before Drafting)
**Tool**: NovelCrafter

Critical for POV-switching mysteries. See `references/pov-secrets.md` for detailed setup.

1. Create character Codex entries with knowledge tiers
2. Set up location/object entries
3. Configure custom prompts for POV-aware generation

### Phase 3: Prose Drafting
**Tool**: NovelCrafter

1. Use AI generation for first drafts
2. Refine manually
3. Use revision prompts for cascading changes (see `references/revision-strategies.md`)

### Phase 4: Export to Scrivener
**Tool**: NovelCrafter → Scrivener

See `references/scrivener-sync.md` for efficient transfer methods.

## Reference Files

### Tool-Specific
- `references/novelcrafter-setup.md` — Codex configuration, custom prompt templates, AI generation best practices
- `references/scrivener-sync.md` — Export/import workflows, folder structures, avoiding copy/paste fatigue

### Craft & Process
- `references/pov-secrets.md` — **Read for any multi-POV mystery.** Character knowledge tiers, keeping secrets consistent across POVs
- `references/revision-strategies.md` — Managing cascading changes, find-and-fix workflows, NovelCrafter prompts for bulk updates
- `references/genre-craft.md` — Noir, thriller, mystery, suspense, horror conventions and blending strategies

## Quick Decision Tree

**"Where should I do this task?"**

| Task | Tool |
|------|------|
| Initial brainstorming / "what if" exploration | Claude or ChatGPT |
| Structural outline | Word/Docs → Claude for refinement |
| Consolidate multiple drafts into outline | **novel-outliner** skill |
| Character/world building | NovelCrafter Codex |
| First-draft prose | NovelCrafter (AI-assisted) |
| Manual prose refinement | NovelCrafter |
| Cascading revisions | NovelCrafter (custom prompts) |
| "Official" manuscript compilation | Scrivener |
| Backup/versioning | Dropbox or Google Drive |
| Research deep-dives | Claude with web search |

**"I have multiple drafts and need to consolidate them into one outline"**
→ Use **novel-outliner** skill — it handles primary/supplemental document hierarchy and produces structured beat sheets

**"I need to make a big change that affects multiple chapters"**
→ See `references/revision-strategies.md`

**"I'm writing a mystery with secrets — how do I set up NovelCrafter?"**
→ See `references/pov-secrets.md`

**"What are the conventions for [genre]?"**
→ See `references/genre-craft.md`

## When to Web Search

Always search for current documentation when user asks about:
- Specific NovelCrafter features (Codex, Chat, Sessions, export options)
- Scrivener compile settings, sync, or organization features
- Integration possibilities between tools
- "Can NovelCrafter do X?" or "How do I do X in Scrivener?"

Search pattern:
```
NovelCrafter [feature] site:novelcrafter.com
Scrivener Mac [feature] site:literatureandlatte.com
```

If official docs don't answer, broaden search to forums and user guides.
