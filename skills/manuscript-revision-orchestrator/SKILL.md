---
name: manuscript-revision-orchestrator
description: Orchestrate extensive manuscript reviews and rewrites with structured change tracking and content fidelity validation. Use when performing comprehensive manuscript revisions that require (1) integrating multiple reference sources (revision memos, canon bibles, timelines, trackers, voice profiles), (2) applying changes in controlled chunks to prevent context overruns, (3) validating edits against source priorities and detecting content injection, or (4) maintaining continuity across complex multi-file manuscripts. Integrates with content-fidelity-validator to prevent unauthorized additions. Triggers include "revise my manuscript", "apply these edits to my novel", "edit my book using these notes", "revision pass", "manuscript rewrite", or any request combining reference documents with an editable manuscript target.
---

# Manuscript Revision Orchestrator

Structured workflow for manuscript revision that minimizes missed issues, prevents accidental errors (continuity breaks, timeline conflicts, character inconsistencies, structural drift, **content injection**), and avoids context overruns through chunking and compact progress tracking.

## Workflow Overview

```
MODE A: Intake & Priorities → MODE B: Planning → MODE C: Editing → MODE D: Validation
         (no editing)          (no editing)       (chunked)        (per-chunk QA)
                                                      ↓
                                            Content Fidelity Validator
                                                      ↓
                                            [PASS] → MODE D
                                            [FAIL] → Log to review, continue
```

## Non-Negotiable Rules (All Modes)

- Do NOT rewrite for style, clarity, or flow unless a logged change explicitly requires it
- Do NOT add scenes, characters, or plot events unless Change Instructions explicitly require it
- **Do NOT add memories, backstory, reflections, or realizations unless explicitly required**
- **All rewrites MUST pass content-fidelity-validator before acceptance**
- If a change cannot be confidently mapped to a unit: output `QUESTION:` with minimal questions, then STOP
- Never exceed the chosen chunk size
- Stop after each chunk is processed and validated

## MODE A: Intake & Priorities

**Label every response:** `[MODE A — Intake & Priorities]`

Run these questions IN ORDER. Do nothing else until all are answered.

### 0. Folder Access

> Please grant Cowork access to the folders I need. Provide macOS paths for:
> - (a) the editable manuscript target (file or folder)
> - (b) any reference documents/folders
>
> If you prefer, grant access to a single root folder and I'll work within it.

### 1. Reference Materials Classification

> List each reference document or folder as:
> `Path | Label | 1-line description`
>
> Labels:
> - **Change Instructions** = documents explicitly telling us what to change (PDF comments, revision memos, tracked changes, notes)
> - **Canon** = documents defining facts/structure (timeline, canon bible, character/scene trackers)
> - **Voice** = character voice profiles (from character-voice-architect)
> - **Unknown** = not sure yet

### 2. Edit Target Definition

> Confirm the manuscript to be edited:
> - Path to editable source (file or folder)
> - Unit boundary: scene files / chapters / other
> - File types and naming pattern (if folder)

### 3. Priority Ordering

State: "All Change Instructions are automatically higher priority than Canon and Voice."

Then ask:
> How should canon and voice sources be prioritized?
> - Option A: You rank them (1,2,3…)
> - Option B: I propose an order for approval
> - Option C: Default order (Canon > Voice)
>
> If two Change Instruction sources conflict, which wins? (Or should "newest wins"?)

### 4. Chunk Size

> Choose a chunk size to minimize overruns:
> - 1 scene (safest)
> - 2–3 scenes
> - 1 chapter
> - Custom

### 5. Output Format

> For each edited chunk, do you want:
> - (A) Revised text only
> - (B) Revised text + Applied Changes checklist + QA notes (recommended)

### 6. Fidelity Validation Mode

> For content-fidelity-validator, choose behavior:
> - (A) **Batch mode** (recommended): Failed chunks logged to review queue, processing continues
> - (B) **Strict mode**: Failed chunks halt processing until resolved
>
> Note: Fidelity validation catches unauthorized additions (new characters, memories, backstory, reflections). This is separate from QA validation in MODE D.

---

## MODE B: Planning

**Label every response:** `[MODE B — Planning]`

**No editing occurs in this mode.**

Produce these artifacts BEFORE any editing:

### 1. Source Register

| Source_ID | Path | Label | Priority | Scope | Notes |
|-----------|------|-------|----------|-------|-------|
| S1 | /path/to/file | Change Instructions | 1 | global | 1–2 bullets |
| VP-Darnell | /path/to/voice-profile | Voice | 5 | per-character | Pulp level 4 |

### 2. Manuscript Inventory

Build from the editable target (not from PDFs):

| Unit_ID | File Name | POV | Time/Date | Location | Characters | 2-sentence Summary |
|---------|-----------|-----|-----------|----------|------------|-------------------|

### 3. Change Log v1 (Discovery)

For each discovered change:

```
Change_ID: C001
Unit_ID: U03
Anchor quote: "1–2 lines from the editable manuscript unit"
Problem: What's wrong
Required change: Imperative, minimal instruction
Source_ID + anchor: S1, page 3 / "quoted line from reference"
Acceptance check: How to verify the change was applied correctly
```

### 4. Change Log v2 (Surgical Operations)

Convert v1 into explicit edit operations per Unit_ID:

```
Unit_ID: U03
Operations:
  - REPLACE: "old text" → "new text" [C001]
  - ADD after "anchor text": "new content" [C002]
  - REMOVE: "text to delete" [C003]
  - VOICE_ENHANCE: "anchor text" per profile [VP-CharacterName] [C004]
Do not touch: [specific elements to preserve]
Verification checks: [how to confirm]
Fidelity scope:
  - Authorized additions: [list what CAN be added, e.g., "sensory details", "action beats"]
  - NOT authorized: new characters, new backstory, new memories, new realizations
```

**STOP after Change Log v2. Wait for user to say "Begin Editing" before modifying any manuscript text.**

---

## MODE C: Editing

**Label every response:** `[MODE C — Editing | Unit: {Unit_ID}]`

### Per-Chunk Process

1. Edit ONLY the selected chunk
2. Apply ONLY Change Log v2 items for that Unit_ID(s)
3. **Run content-fidelity-validator:**
   - Original: chunk before edit
   - Revised: chunk after edit
   - Authorized: operations from Change Log v2
   - **If PASS:** Continue to step 4
   - **If FAIL (batch mode):** Log to fidelity-review-queue.md, mark chunk with inline annotations, continue
   - **If FAIL (strict mode):** Output failure details, STOP
4. Output:
   - Revised text (full unit)
   - Applied Changes checklist (referencing Change_IDs)
   - **Fidelity Status: PASS | FAIL (see review queue)**
   - Open Issues (only if blocked)
   - Updated PROJECT MEMORY
   - Updated PROGRESS LOG
5. **STOP**

---

## MODE D: Validation

**Label every response:** `[MODE D — Validation | Unit: {Unit_ID}]`

After each chunk edit, validate against:
- Relevant Change Instructions in scope
- Highest-priority Canon constraints (timeline/CSV rows for the unit)
- **Voice profile constraints (if voice enhancement was applied)**
- Decisions recorded in PROJECT MEMORY

Output:
```
QA Result: PASS | FAIL
[If FAIL: exact mismatches + Change_IDs needed to resolve]

Fidelity Result: PASS | FAIL
[If FAIL: X injection(s) detected, see fidelity-review-queue.md]
```

**STOP**

---

## Content Fidelity Validation

### Integration with content-fidelity-validator

After each chunk edit in MODE C, invoke content-fidelity-validator:

```
Input:
- original_text: [chunk before edit]
- revised_text: [chunk after edit]
- authorized_changes: [operations from Change Log v2]

Output:
- FIDELITY_PASS: Chunk contains only authorized changes
- FIDELITY_FAIL: Unauthorized additions detected
```

### Batch Mode Behavior (Default)

When fidelity validation fails:
1. Log failed chunk to `fidelity-review-queue.md`
2. Mark chunk in output with inline annotations: `««INJECTION:TYPE content»»`
3. Continue processing remaining chunks
4. Include fidelity summary in batch completion report

### Strict Mode Behavior

When fidelity validation fails:
1. Output detailed failure report
2. List all detected injections
3. STOP processing
4. Await user decision: resolve and retry, or switch to batch mode

### Fidelity Review Queue Format

```markdown
# Fidelity Review Queue

Session: [datetime]
Mode: [batch/strict]
Total chunks: [X]
Passed: [Y]
Failed: [Z]

---

## Failed Chunk: [Unit_ID]

### Injection Details
[output from content-fidelity-validator]

### User Action Required
- [ ] Approve as-is
- [ ] Reprocess without injections
- [ ] Manual edit

---
```

### Post-Session Review

After batch processing completes:
1. Present fidelity summary
2. Offer to open review queue
3. User can approve/reject individual chunks
4. Rejected chunks can be reprocessed with stricter constraints

---

## Source Priority Logic

1. Change Instructions outrank Canon and Voice by default
2. Canon priority follows user's ranking
3. Voice profiles follow Canon unless user specifies otherwise
4. Unknown sources are ignored until classified
5. Conflicts:
   - Between Change Instructions: ask once, record decision, proceed
   - Between Canon sources: follow user's ranking
   - Between Voice and Canon: Canon wins unless user specifies

---

## Memory Management (Anti-Overrun Protocol)

Maintain and update EVERY chunk:

### PROJECT MEMORY (~800 tokens max)

```
## Source Register
[Source_ID → path + label + priority]

## Conflict Decisions
[Logged resolutions]

## Global Constraints
[Names/spellings, dates, locations, "do not change" rules]

## Voice Profiles Active
[Character → profile reference → pulp level]

## Open Questions
[Unresolved items]
```

### PROGRESS LOG (~300 tokens max)

```
## Completed
[Unit_IDs + Change_IDs applied]

## Fidelity Status
[Unit_IDs with PASS/FAIL status]

## Remaining
[Unit_IDs pending]

## New Issues
[Conflicts/mapping issues/fidelity failures discovered this chunk]
```

### Context Loading Per Chunk

Include ONLY:
- Current chunk text
- Relevant excerpts from highest-priority sources for that chunk
- Voice profiles for characters in chunk (if voice enhancement authorized)
- PROJECT MEMORY
- PROGRESS LOG

Do NOT carry forward full manuscript text.

---

## Scrivener Sync Folder Defaults

When edit target is a folder of scene files:
- Treat each scene file as a Unit_ID
- Preserve file names and ordering
- Never rename files unless explicitly instructed
- Preserve formatting/paragraph structure

---

## Related Skills

| Skill | Relationship |
|-------|--------------|
| **content-fidelity-validator** | Validates chunks during MODE C |
| **character-voice-architect** | Provides voice profiles as source |
| **canon-creator** | Provides canon as source |
| **noir-mystery-qa** | Can QA-check scenes post-revision |

---

## Quick Reference

| Mode | Editing Allowed | Key Deliverable | Stop Point |
|------|-----------------|-----------------|------------|
| A | No | Completed intake answers | After all 6 questions |
| B | No | Change Log v2 | After v2, await "Begin Editing" |
| C | Yes (chunk only) | Revised chunk + checklist + fidelity status + memory update | After each chunk |
| D | No | QA PASS/FAIL + Fidelity PASS/FAIL | After each validation |
