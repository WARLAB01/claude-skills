---
name: canon-creator
description: Generate comprehensive, verified canon bibles from novel manuscripts. Use when the user needs to create authoritative reference documents from a completed or in-progress manuscript, including synopsis, hierarchical outline (Act/Chapter/Scene/Beat), character sheets with visual prompts, Voice Profiles (V2 format), and mystery-specific trackers (mystery registry, truth/deception lists, character awareness timelines). Auto-detects manuscript format (single file or Scrivener folder) and genre (mystery/thriller triggers additional artifacts). All extracted facts are verified against source text to prevent hallucinations. Output is formatted for use with manuscript-revision-orchestrator and character-voice-architect. Triggers include "create a canon bible", "generate canon from my manuscript", "build a story bible", "extract canon", "create character sheets from my novel", or any request to create authoritative reference documentation from fiction manuscripts.
---

# Canon Creator

Generate verified, authoritative canon bibles from novel manuscripts with zero tolerance for hallucinations or misinterpretations.

## Output Artifacts

| Artifact | Always Generated | Mystery/Thriller Only |
|----------|------------------|----------------------|
| Synopsis | ✓ | |
| Hierarchical Outline (Act/Chapter/Scene/Beat) | ✓ | |
| Main Character Sheets (with visual prompts) | ✓ | |
| **Voice Profiles (V2 format)** | **✓** | |
| Minor Character Registry | ✓ | |
| Mystery Registry | | ✓ |
| Truth/Deception/Misunderstanding List | | ✓ |
| Character Awareness Timeline | | ✓ |

## Critical Principle: Verification-First Extraction

**Every fact in the canon bible must be traceable to a specific location in the manuscript.**

This skill uses chunked verification to prevent hallucinations:
1. Extract facts with source anchors (quotes + locations)
2. Cross-reference all extractions against original text
3. Flag any claim that cannot be verified
4. User checkpoint for ambiguous items

See `references/verification-protocol.md` for detailed methodology.

## Workflow Overview

```
Phase 1: Intake & Detection
    ↓
Phase 2: Chunked Extraction (with source anchors)
    ↓
Phase 3: Verification Pass
    ↓
Phase 4: Assembly & Output
```

## Phase 1: Intake & Detection

### Step 1.1: Receive Manuscript

Accept manuscript in one of two formats:
- **Single file**: .docx, .md, .txt, or similar
- **Scrivener sync folder**: Directory containing scene files

Auto-detect format:
```python
if os.path.isdir(input_path):
    # Check for Scrivener patterns: numbered files, .txt/.rtf scenes
    format_type = "scrivener_folder"
else:
    format_type = "single_file"
```

### Step 1.2: Build Manuscript Inventory

Create inventory regardless of input format:

```markdown
## Manuscript Inventory

| Unit_ID | Source | POV | Est. Word Count | Scene Break Markers |
|---------|--------|-----|-----------------|---------------------|
| U001 | chapter-01.txt | Sarah | 2,340 | "***" at line 847 |
| U002 | chapter-01.txt | Marcus | 1,890 | EOF |
```

For single files, detect scene/chapter breaks via:
- Explicit markers: `***`, `###`, `---`
- Chapter headings: "Chapter 1", "CHAPTER ONE", etc.
- Large whitespace gaps (3+ blank lines)

### Step 1.3: Genre Detection

Scan manuscript for mystery/thriller markers. See `references/mystery-detection.md` for full marker list.

**High-confidence markers** (any 2+ triggers mystery mode):
- Investigation/detective vocabulary
- Murder, crime, or criminal activity as central plot
- Hidden information/secrets as plot drivers
- Revelation/discovery scene structures
- Multiple suspects or alibi references

**Output**:
```markdown
## Genre Detection

Primary genre signals: [list detected markers]
Mystery/Thriller mode: ENABLED | DISABLED
Confidence: High | Medium | Low

[If Medium/Low confidence, ask user to confirm]
```

### Step 1.4: User Confirmation

Before proceeding, confirm:
> I've detected:
> - Manuscript format: [single file / Scrivener folder]
> - Estimated scenes: [count]
> - Genre: [detected] — Mystery artifacts: [enabled/disabled]
>
> Proceed with canon extraction?

## Phase 2: Chunked Extraction

Process manuscript in chunks to prevent context overload. Each extraction includes **source anchors** for verification.

### Chunk Size

- Default: 1 chapter or ~5,000 words
- Adjust based on scene density
- Never exceed 8,000 words per chunk

### Extraction Categories

Process each chunk for ALL applicable categories:

#### 2.1 Plot Events (→ Synopsis & Outline)

For each scene in chunk, extract:

```markdown
### Scene: [Unit_ID]

**POV**: [character name]
**Location**: [where]
**Timeline position**: [when, relative or absolute]

**Scene summary** (2-3 sentences):
[What happens]

**Source anchor**: "[15-25 word quote from scene]" (Unit_ID, para X)

**Beats**:
1. [Beat description] — Anchor: "[quote]" (para X)
2. [Beat description] — Anchor: "[quote]" (para X)
...

**Scene turn**: [What changes by scene end]
**Turn anchor**: "[quote]" (para X)
```

#### 2.2 Character Data (→ Character Sheets)

For each character appearance in chunk:

```markdown
### Character: [Name]

**Scene**: [Unit_ID]
**Role in scene**: [POV / Supporting / Mentioned]

**Physical details mentioned**:
- [detail] — Anchor: "[quote]" (Unit_ID, para X)

**Personality/behavior shown**:
- [trait] — Anchor: "[quote]" (Unit_ID, para X)

**Relationships revealed**:
- [relationship] — Anchor: "[quote]" (Unit_ID, para X)

**Backstory revealed**:
- [info] — Anchor: "[quote]" (Unit_ID, para X)

**Speech patterns/verbal tics**:
- [pattern] — Anchor: "[quote]" (Unit_ID, para X)
```

#### 2.3 Mystery Elements (if mystery mode enabled)

See `references/extraction-patterns.md` for detailed templates.

**Mysteries**:
```markdown
### Mystery: [ID] — [Brief description]

**Type**: Central plot mystery | Subplot mystery | Red herring | Unanswered question

**Seeding**:
- First hint: [description] — Anchor: "[quote]" (Unit_ID, para X)
- Additional seeds: [list with anchors]

**Clues found**:
- [clue] — Found by [character] — Anchor: "[quote]" (Unit_ID, para X)

**Resolution**:
- Resolved: Yes/No/Partial
- If resolved: [how] — Anchor: "[quote]" (Unit_ID, para X)
```

**Truths/Deceptions/Misunderstandings**:
```markdown
### [Type]: [Brief description]

**The reality**: [What is actually true]
**Reality anchor**: "[quote]" (Unit_ID, para X)

**The [deception/misunderstanding]**: [What character(s) believe]
**Belief anchor**: "[quote]" (Unit_ID, para X)

**Who believes it**: [character list]
**Who knows the truth**: [character list]
**When corrected**: [Unit_ID] or "Not corrected in manuscript"
```

**Character Awareness**:
```markdown
### Awareness Update: [Character] — [Unit_ID]

**Learns**:
- [information] — Anchor: "[quote]" (para X)

**Suspects**:
- [suspicion] — Anchor: "[quote]" (para X)

**Still doesn't know**:
- [information from earlier that character lacks]
```

#### 2.4 Voice Pattern Data (→ Voice Profiles)

For each character with 3+ dialogue instances, extract:

```markdown
### Voice Data: [Character Name]

**Dialogue Instances Analyzed:** [count]

**Speech Pattern Observations:**
- Average sentence length: [X] words
- Vocabulary register: [assessment with examples]
- Sentence structure: [patterns observed]

**Verbal Markers Found:**
- Tics/repeated phrases: "[phrase]" (count: X, locations: Unit_IDs)
- Filler words: [list with frequency]
- Profanity: [level, specific words, contexts]
- Contractions: [usage pattern]

**Sample Dialogue Cluster:**
> "[Quote 1]" — Unit_ID, para X
> "[Quote 2]" — Unit_ID, para X
> "[Quote 3]" — Unit_ID, para X
> "[Quote 4]" — Unit_ID, para X
> "[Quote 5]" — Unit_ID, para X

**Internal Voice Data (POV characters):**
- Thought style observed: [patterns]
- Observation priorities: [what they notice]
- Self-reference pattern: [how they think about themselves]

**Sample Internal Monologue:**
> "[Extended thought passage]" — Unit_ID, para X
```

### Chunk Processing Loop

```
FOR each chunk in manuscript:
    1. Load chunk text
    2. Extract all applicable categories
    3. Save extractions with source anchors to working files
    4. Update running character registry
    5. Update running mystery registry (if enabled)
    6. Update running voice pattern data
    7. Log extraction progress
NEXT chunk
```

## Phase 3: Verification Pass

After all chunks processed, verify every extraction.

### Verification Protocol

For each extracted fact:

1. **Locate source anchor** in original manuscript
2. **Confirm quote exists** at stated location (fuzzy match allowed for minor whitespace/punctuation differences)
3. **Verify claim matches quote** — Does the extracted fact accurately represent what the quote says?

### Verification Outcomes

| Outcome | Action |
|---------|--------|
| **VERIFIED** | Fact confirmed, include in canon |
| **ANCHOR_NOT_FOUND** | Quote not found at location — flag for manual review |
| **CLAIM_MISMATCH** | Quote exists but doesn't support claim — flag for manual review |
| **AMBIGUOUS** | Quote supports multiple interpretations — flag for user decision |

### Verification Report

```markdown
## Verification Report

Total facts extracted: [count]
Verified: [count] ([%])
Flagged for review: [count]

### Flagged Items

#### ANCHOR_NOT_FOUND
- [Fact]: [claimed anchor] — [Unit_ID, para X]
  Suggested action: [locate correct anchor / remove fact]

#### CLAIM_MISMATCH
- [Fact]: [anchor found but doesn't match]
  Original quote: "[actual quote]"
  Suggested action: [revise fact / remove fact]

#### AMBIGUOUS
- [Fact]: [quote supports multiple readings]
  Possible interpretations: [list]
  USER DECISION REQUIRED
```

### User Checkpoint

Present verification report and ask:
> Verification complete. [X] facts verified, [Y] flagged for review.
>
> [Show flagged items]
>
> How would you like to handle flagged items?
> 1. Review each individually
> 2. Remove all flagged items from canon
> 3. Include flagged items with "[UNVERIFIED]" marker

## Phase 4: Assembly & Output

### Step 4.1: Compile Canon Document

Assemble all verified extractions into single mega-document using template in `assets/canon-template.md`.

**Document Structure**:
```markdown
# [TITLE] — Canon Bible
Generated: [date]
Source: [manuscript filename/folder]
Verification: [X/Y facts verified]

---

## 1. Synopsis
[Compiled from scene summaries, 500-1000 words]

## 2. Hierarchical Outline

### Act I: [Title]
[Act summary, 2-3 sentences]

#### Chapter 1: [Title]
[Chapter summary, 1-2 sentences]

##### Scene 1.1: [Brief descriptor]
- **POV**: [character]
- **Location**: [where]
- **Timeline**: [when]
- **Summary**: [2-3 sentences]
- **Beats**:
  1. [beat]
  2. [beat]
- **Turn**: [what changes]

[Continue for all scenes/chapters/acts]

## 3. Character Registry

### Main Characters

#### [Character Name]
[Full character sheet — see references/character-sheet-template.md]

**Visual Prompt (Grok/ChatGPT Image)**:
[Generated prompt for character visualization]

**Voice Profile Reference**: `voice-profiles/[character-name].voice.md`

[Repeat for each main character]

### Minor Characters
| Name | Role | First Appearance | Key Details |
|------|------|------------------|-------------|
| [name] | [role] | [Unit_ID] | [1-2 details] |

## 4. Voice Profiles

[V2 voice profiles for all major characters — see voice-profiles/ folder]

## 5. Mystery Artifacts [IF MYSTERY MODE]

### 5.1 Mystery Registry
[All mysteries with seeding, clues, resolution status]

### 5.2 Truths, Deceptions, and Misunderstandings
[Categorized list with belief holders and correction points]

### 5.3 Character Awareness Timeline
[Timeline showing when each major character learns key information]

---

## Appendix: Source Anchors
[Full list of all anchors for cross-reference]

## Appendix: Verification Log
[Summary of verification pass results]
```

### Step 4.2: Generate Visual Prompts

For each main character, generate visual prompts using the **visual-prompt-generator** skill.

Integration:
1. Compile character's physical description from all anchored extractions
2. Pass to visual-prompt-generator with:
   - Platform targets: Grok Imagine, ChatGPT Images
   - Style: Character reference sheet
   - Include: All verified physical details
   - Exclude: Any unverified or ambiguous details

### Step 4.3: Generate Voice Profiles

For each main character, generate V2 voice profiles:

1. Compile voice pattern data from all extraction chunks
2. Identify archetype alignment based on patterns
3. Calculate pulp level from prose style in source
4. Generate draft profile with:
   - All anchored observations
   - Detected patterns
   - Sample dialogue cluster
   - Sample internal monologue (POV only)
5. Mark as "DRAFT - requires user refinement via character-voice-architect"

**Output:** `voice-profiles/[character-name].voice.md` per character

**Integration note:** These draft profiles can be loaded directly into character-voice-architect Mode A for interactive refinement, or used as-is for light voice work.

### Step 4.4: Format for Revision Orchestrator

Ensure output is compatible with manuscript-revision-orchestrator as a **Canon** source:

- Clear section headers for easy reference
- Anchored facts with Unit_ID references matching manuscript inventory
- Consistent formatting for find/grep operations
- Priority markers if user wants to rank canon sections
- Voice profiles formatted for use as "Voice" source type

### Step 4.5: Save and Present

1. Save to `/mnt/user-data/outputs/[manuscript-name]-canon.md`
2. Save voice profiles to `/mnt/user-data/outputs/voice-profiles/`
3. Present files to user
4. Offer:
   > Canon bible generated. Would you like me to:
   > - Refine voice profiles interactively with character-voice-architect?
   > - Generate a separate character visualization document?
   > - Export mystery artifacts as standalone tracker?
   > - Create a condensed "quick reference" version?

## Reference Files

- `references/extraction-patterns.md` — Detailed templates for each extraction category
- `references/mystery-detection.md` — Genre markers and mystery mode triggers
- `references/verification-protocol.md` — Full verification methodology and edge cases
- `references/character-sheet-template.md` — Main character sheet structure
- `references/outline-hierarchy.md` — Summarization standards for each outline level
- `references/voice-extraction-patterns.md` — Patterns for extracting voice data

## Related Skills

| Skill | Relationship |
|-------|--------------|
| **character-voice-architect** | Voice profiles serve as input for voice refinement |
| **manuscript-revision-orchestrator** | Canon output serves as Canon source input |
| **visual-prompt-generator** | Generates character visualization prompts |
| **noir-mystery-qa** | Can QA-check scenes using canon as reference |
| **novel-drafter** | Canon can inform drafting of new scenes |

## Working Directory Structure

```
/home/claude/canon-working/
├── config/
│   └── detection-results.md      # Genre detection, format detection
├── inventory/
│   └── manuscript-inventory.md   # Unit inventory
├── extractions/
│   ├── chunk-001/
│   │   ├── plot-events.md
│   │   ├── character-data.md
│   │   ├── voice-data.md         # Voice pattern extraction
│   │   └── mystery-elements.md   # If mystery mode
│   ├── chunk-002/
│   │   └── ...
│   └── ...
├── compiled/
│   ├── synopsis.md
│   ├── outline.md
│   ├── characters/
│   │   ├── [character-name].md
│   │   └── ...
│   ├── voice-profiles/           # V2 voice profiles
│   │   ├── [character-name].voice.md
│   │   └── ...
│   ├── mystery-registry.md       # If mystery mode
│   ├── truth-deception.md        # If mystery mode
│   └── awareness-timeline.md     # If mystery mode
├── verification/
│   ├── verification-log.md
│   └── flagged-items.md
└── output/
    ├── [manuscript-name]-canon.md
    └── voice-profiles/
        └── [character-name].voice.md
```

## Error Handling

### Manuscript Too Large
If manuscript exceeds reasonable processing limits (>200k words):
- Process in phases (Act I first, then Act II, etc.)
- Maintain running state between sessions
- Offer to generate partial canon for completed sections

### Ambiguous Scene Breaks
If scene/chapter boundaries are unclear:
- Ask user to confirm detected breaks
- Offer to proceed with best-guess boundaries
- Flag boundary uncertainty in output

### Character Name Variants
If same character appears with multiple names/nicknames:
- Build alias registry during extraction
- Ask user to confirm alias mappings
- Consolidate all aliases in character sheets

### Timeline Ambiguity
If timeline is non-linear or unclear:
- Extract relative positions ("before X", "after Y")
- Flag absolute timeline gaps
- Offer to generate timeline reconstruction as separate artifact

### Insufficient Voice Data
If character has fewer than 3 dialogue instances:
- Flag as insufficient data for voice profile
- Generate partial profile marked "LOW CONFIDENCE"
- Recommend using archetype defaults in character-voice-architect
