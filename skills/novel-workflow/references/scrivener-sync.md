# Scrivener Integration & Sync

Getting content from NovelCrafter to Scrivener efficiently, maintaining organization, and avoiding copy/paste fatigue.

## Before You Start: Search Current Docs

```
site:literatureandlatte.com Scrivener Mac [feature]
Scrivener 3 [feature] tutorial
```

Features and menus change between versions — verify current UI.

## The Copy/Paste Problem

Current workflow: Copy from NovelCrafter → Paste into Scrivener

**Pain points:**
- Tedious for many scenes
- Easy to miss scenes or paste into wrong place
- Formatting can get mangled
- No tracking of what's been transferred

## Recommended Workflow: Export + Import

### Option 1: Scene-by-Scene (Current Reality)

Until better integration exists, optimize the manual process:

**In NovelCrafter:**
1. Complete and polish a chapter (all scenes)
2. Export chapter as single document (if feature available) OR
3. Copy scene-by-scene with clear markers

**In Scrivener:**
1. Create matching folder structure first (Act → Chapter → Scene)
2. Paste into correct scene document
3. Mark as transferred in your tracking system

**Tracking System:**
Maintain a simple checklist (in Notes app, spreadsheet, or Scrivener itself):
```
□ Scene 1.1.1 - transferred [date]
□ Scene 1.1.2 - transferred [date]  
□ Scene 1.1.3 - in progress
□ Scene 1.2.1 - not started
```

### Option 2: Batch Export (Check NovelCrafter Features)

**Search**: `NovelCrafter export` to see current export options.

If NovelCrafter supports exporting to:
- **.docx**: Export → Import into Scrivener via File > Import > Files
- **.txt with scene markers**: Import and split in Scrivener
- **Markdown**: Import and convert

**Scrivener Import Tips:**
- File > Import > Import and Split: Can split a single doc into multiple scenes based on separator (like `###`)
- Drag and drop .docx files directly into binder
- Import into a "Staging" folder first, then organize

### Option 3: Folder Sync (Advanced)

Scrivener has folder sync capability:
1. Set up a sync folder (in Dropbox)
2. Scrivener syncs documents to/from this folder
3. Edit in external app, changes sync back

**Potential workflow:**
- Export from NovelCrafter to the sync folder
- Scrivener pulls in changes

**Caveat:** Search current Scrivener docs for folder sync limitations — this feature has quirks around formatting and file naming.

## Scrivener Project Structure

### Recommended Binder Organization

```
[Project Name]
├── Manuscript
│   ├── Act 1
│   │   ├── Chapter 1.1: [Title]
│   │   │   ├── Scene 1.1.1
│   │   │   ├── Scene 1.1.2
│   │   │   └── Scene 1.1.3
│   │   └── Chapter 1.2: [Title]
│   │       └── ...
│   ├── Act 2
│   │   └── ...
│   └── Act 3
│       └── ...
├── Characters
│   ├── [Character sheets - mirror NovelCrafter Codex]
├── Locations  
│   └── ...
├── Research
│   └── [Reference materials]
├── Outline
│   └── [Exported outline from novel-outliner skill]
└── Trash
```

### Matching NovelCrafter Structure

Keep scene numbering consistent:
- NovelCrafter Scene "1.1.1" = Scrivener document "Scene 1.1.1"
- Use Scrivener labels/status to track: Draft, Revised, Final

### Status Workflow

Use Scrivener's Status field:
- **To Do**: Scene exists in outline, not yet written
- **First Draft**: Transferred from NovelCrafter, unrevised
- **Revised Draft**: Manual revisions complete
- **Final**: Ready for compile

## Avoiding Duplicate Work

### Rule: NovelCrafter for Drafting, Scrivener for Compilation

- Write and revise prose in NovelCrafter
- Only transfer to Scrivener when a scene/chapter is "done enough"
- Do final polish and compile in Scrivener
- Don't try to keep both in sync during active drafting

### When to Transfer

Transfer when:
- A chapter is complete (all scenes drafted)
- You've done at least one revision pass
- You're confident major structural changes are done

Don't transfer:
- Scene-by-scene as you draft (too much overhead)
- Before you've resolved known issues
- If you're still experimenting with structure

## Handling Revisions After Transfer

**If you need to revise something already in Scrivener:**

Option A: Revise in Scrivener directly (minor changes)
Option B: Revise in NovelCrafter, re-export, replace in Scrivener (major rewrites)

**For Option B**, use Scrivener's Snapshots:
1. Take snapshot of current version in Scrivener (Documents > Snapshots > Take Snapshot)
2. Paste new version from NovelCrafter
3. Snapshot preserved if you need to compare/revert

## Compile Basics

When manuscript is complete, Scrivener compiles to final format:
- File > Compile
- Choose format (PDF, ePub, docx, etc.)
- Set front matter, chapter headings, formatting

**Search**: `Scrivener 3 compile` for current detailed tutorials.

## Backup Strategy

### Local Backups
- Scrivener: Preferences > Backup (automatic backups)
- Set backup location to Dropbox or Google Drive

### Version Milestones
At major milestones:
1. Compile to .docx
2. Save with date: `[Title]_v1_2026-01-12.docx`
3. Store in Dropbox/Drive

### NovelCrafter + Scrivener Both
- Export from NovelCrafter periodically
- Scrivener project backed up separately
- Neither replaces the other for backup purposes
