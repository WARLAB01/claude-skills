---
name: character-voice-architect
description: Create, analyze, and apply character voice profiles to strengthen manuscript characterization. Three modes - Cartographer (analyze existing voices), Alchemist (rewrite to amplify voices), Tuner (targeted voice enhancements). Features archetype-based trait picking with clickable options, per-character pulp calibration, and integration with content-fidelity-validator to prevent content injection. Supports Scrivener folders and single-file manuscripts. Triggers include "create voice profiles", "analyze character voices", "strengthen character voice", "make dialogue more distinctive", "apply voice profiles", "pulp up my prose", or requests to improve characterization consistency.
---

# Character Voice Architect

Create and apply character voice profiles to strengthen manuscript characterization without altering plot, meaning, or introducing new content.

## Three Modes

| Mode | Purpose | Output |
|------|---------|--------|
| **A: Cartographer** | Analyze existing manuscript to detect and profile character voices | Voice profiles (draft → user-refined) |
| **B: Alchemist** | Apply voice profiles to rewrite scenes with stronger characterization | Revised manuscript chunks |
| **C: Tuner** | Generate targeted voice enhancement suggestions | Fix List (noir-mystery-qa compatible) |

## Hard Safety Rules (All Modes)

- Do NOT add new characters, memories, backstory, or plot elements
- Do NOT change what characters do or what happens
- Do NOT alter the meaning of what is said—only HOW it's said
- Do NOT resolve ambiguities or add realizations not in source
- ALWAYS invoke content-fidelity-validator after rewrites (Modes B/C)
- If validation fails, log to review queue and continue (do not halt batch)

## Mode A: Voice Cartographer

Analyze manuscript to extract and profile existing character voices.

### Activation

> Ready to analyze character voices. Please provide:
> 1. Manuscript (file path or paste) — Scrivener folder or single file
> 2. Genre(s) this work spans (for archetype generation)
> 3. Any characters you want to prioritize?

### Context Management (Long Manuscripts)

This mode uses **phased context management** to handle large manuscripts without hitting context limits.

| Phase | Agent | Context Load | Output |
|-------|-------|--------------|--------|
| A1: Extraction | Subagent | Full manuscript (then discarded) | Compact sample files |
| A2: Interactive | Main agent | One sample file at a time (~2-3KB) | User selections stored |
| A3: Compilation | Main agent | Sample files + stored answers | Final V2 profiles |

**Key principle:** The full manuscript is read only once, by a delegated subagent. The main agent never loads the full corpus, only compact sample files.

**If processing 6+ characters:**
- Complete profiles for first batch (4-5 characters)
- Save to user folder
- Suggest fresh conversation for remaining characters
- Or continue with explicit context clearing between characters

---

### Phase A1: Manuscript Extraction (Delegated)

**CRITICAL:** Do not read the full manuscript directly. Delegate extraction to a subagent.

**Delegate extraction task with these instructions:**

```
You are extracting dialogue for character voice profiling.

Manuscript: [path]
Characters to profile: [list]
Genre: [genre]

STEP 1: MANUSCRIPT INTAKE

For Scrivener Folder:
- Scan for scene files (.txt, .rtf, .md)
- Build manuscript inventory (Unit_ID, POV, word count)
- Identify scene boundaries

For Single File:
- Detect chapter/scene breaks
- Segment into units
- Assign Unit_IDs

STEP 2: DIALOGUE EXTRACTION

For each unit:
1. Extract all dialogue with speaker attribution
2. Tag dialogue: [SPEAKER: Character Name] "dialogue text"
3. Collect dialogue clusters per character
4. Note surrounding action beats

STEP 3: PATTERN DETECTION

Analyze each character's dialogue corpus for:

Quantitative Markers:
- Average sentence length
- Vocabulary complexity (unique words / total words)
- Question frequency
- Profanity frequency (list specific words found)
- Contraction usage rate

Qualitative Patterns:
- Verbal tics (repeated phrases, with counts)
- Sentence structure preferences
- Response patterns (direct/evasive/deflecting)
- Emotional expression style

For POV Characters Additionally:
- Internal monologue style
- Observation priorities (what they notice first)
- Self-perception indicators
- Thought rhythm (fragmented/flowing/analytical)

STEP 4: CREATE SAMPLE FILES

For EACH character, create a sample file at:
/home/claude/voice-working/samples/[character-name]-sample.md

Each file must contain (see Sample File Template below):
1. Character role (POV/Major/Minor)
2. Total dialogue count found
3. Quantitative metrics (pre-computed)
4. Representative dialogue (10-15 best examples showing voice)
5. Internal monologue samples (5-10, POV only)
6. Detected verbal tics (phrase + 2-3 example usages)
7. Preliminary archetype suggestion based on patterns

Keep each file under 3KB. Select REPRESENTATIVE samples, not exhaustive.

STEP 5: RETURN SUMMARY

Return only:
- List of characters processed
- File paths created
- Summary statistics (dialogue counts, scene counts)
- Any issues encountered

Do NOT return the full dialogue corpus.
```

**Wait for subagent to complete before proceeding to Phase A2.**

#### Sample File Template

```markdown
# Voice Sample: [CHARACTER NAME]

## Metadata
- Role: [POV / Major / Minor]
- Dialogue instances: [count]
- Scenes appeared: [count]

## Quantitative Metrics
| Metric | Value |
|--------|-------|
| Avg sentence length | X words |
| Questions | X of Y (Z%) |
| Profanity | [none/mild/moderate/heavy] — words: [list] |
| Contractions | [rate] |
| Interruptions (em-dash) | X instances |
| Trailing off (ellipsis) | X instances |

## Detected Verbal Tics
- "[tic phrase]" — X instances
  - Example: "[quote]" (Scene: X)
  - Example: "[quote]" (Scene: Y)

## Representative Dialogue

### Shows [trait/pattern]:
> "[dialogue]" — Scene: X

### Shows [trait/pattern]:
> "[dialogue]" — Scene: Y

[10-15 total samples]

## Internal Monologue (POV only)

> *[thought]* — Scene: X

[5-10 samples]

## Preliminary Archetype Assessment

Based on detected patterns, this character aligns with:
- **Primary:** [archetype] because [brief reason]
- **Possible secondary:** [archetype] because [brief reason]

User should confirm/override in interactive phase.
```

---

### Phase A2: Interactive Profile Building

**Process ONE character at a time to manage context.**

Based on declared genres, generate relevant archetypes for selection. See `references/voice-archetypes.md` for full library.

**Example for Noir/Mystery:**
- Hardboiled Detective
- Femme Fatale
- World-Weary Cop
- Nervous Witness
- Smooth Criminal
- Working Class Hero
- Wounded Romantic
- Cynical Reporter
- Hidden Poet (tough exterior, lyrical interior)

Each archetype is a menu of traits user can pick from.

**For each character:**

1. **Read** `/samples/[character-name]-sample.md` (only this character's file)
2. **Present** draft findings:
   - Quantitative metrics (from sample file)
   - Detected patterns (from sample file)
   - Representative quotes (2-3 only in presentation)
   - Preliminary archetype assessment
3. **Interactive Q&A** using clickable format (see below)
4. **Store** user's selections
5. **Proceed** to next character

**Do NOT re-read previous character samples during this phase.**

**If context feels slow (>4 characters processed):**
- Compile profiles for completed characters immediately
- Save to user folder
- Offer to continue in fresh conversation

#### Interactive Profile Template

For each major character, present options using clickable format:

```markdown
## Voice Profile: [Character Name]

Based on analysis of [X] dialogue instances across [Y] scenes.

### Detected Patterns
- Average sentence length: [X] words
- Vocabulary register: [assessment]
- Verbal tics found: "[phrase 1]", "[phrase 2]"
- Profanity level: [none/mild/moderate/heavy]

### Archetype Alignment

Which archetype(s) best fit this character's voice?

**Primary Archetype:**
- [ ] Hardboiled Detective — Terse, cynical, observational
- [ ] World-Weary Cop — Tired, procedural, seen-it-all
- [ ] Working Class Hero — Direct, practical, loyalty-driven
- [ ] Wounded Romantic — Guarded exterior, vulnerable interior
- [ ] Hidden Poet — Tough talk hiding lyrical soul
- [ ] Other: [describe]

**Secondary Influence (optional):**
- [ ] Add Cynical Reporter traits (probing questions, skepticism)
- [ ] Add Smooth Criminal traits (charm, misdirection)
- [ ] Add Nervous Witness traits (hedging, fear responses)
- [ ] None

### Trait Selection

From your chosen archetype(s), which specific traits apply?

**Speech Patterns:**
- [ ] Clipped sentences (5-8 words typical)
- [ ] Complete but economical (10-15 words)
- [ ] Expansive when comfortable, terse under pressure
- [ ] Run-on when nervous, controlled otherwise

**Vocabulary:**
- [ ] Blue-collar vernacular
- [ ] Professional/technical jargon: [specify field]
- [ ] Educated but deliberately casual
- [ ] Code-switching (formal in public, casual in private)

**Verbal Tics:**
- [ ] Keep detected: "[tic 1]", "[tic 2]"
- [ ] Add: [user can specify]
- [ ] Remove: [user can specify]

**Profanity Calibration:**
- [ ] None (clean)
- [ ] Mild (damn, hell)
- [ ] Moderate (shit, bastard)
- [ ] Heavy (unrestricted)
- [ ] Contextual: [specify triggers]

**Emotional Expression:**
- [ ] Suppressed (shows through action, not words)
- [ ] Deflected through humor
- [ ] Deflected through anger
- [ ] Direct but controlled
- [ ] Volatile

### POV-Specific (if applicable)

**Internal Voice Style:**
- [ ] More articulate than speech
- [ ] Less articulate than speech (action-oriented thinker)
- [ ] Same register as speech
- [ ] Shifts based on emotional state

**Self-Deprecating Humor:**
- [ ] Frequent — wry commentary on own situation
- [ ] Occasional — stress response
- [ ] Rare — only in safe contexts
- [ ] None

**Observation Priority:**
- [ ] Threats/exits first
- [ ] People's faces/emotions first
- [ ] Physical environment first
- [ ] Inconsistencies/details first

### Pulp Calibration

Set voice intensity (1-5):

1 = Clean, professional prose
2 = Light genre flavor
3 = Balanced noir/pulp
4 = Strong pulp voice
5 = Full Chandler (similes, wise-cracks, spare poetry)

Current setting: [ 1 ] [ 2 ] [ 3 ] [ 4 ] [ 5 ]
```

### Phase A3: Profile Compilation

After all interactive Q&A is complete for a batch of characters:

**For each character with completed selections:**

1. **Read** sample file one more time
2. **Generate** V2 profile using:
   - Pre-computed metrics from sample file
   - User's archetype selections
   - User's trait selections
   - User's pulp calibration
   - Representative examples from sample file
3. **Create** example rewrites showing voice in action
4. **Save** to `/home/claude/voice-working/profiles/[character-name].md`
5. **Copy** to user's manuscript folder (if specified)

**Output:** `voice-profiles/[character-name].md` for each profiled character

**If more characters remain:**
- Suggest starting fresh conversation
- Provide list of completed vs. remaining characters
- Sample files persist for continuation

---

## Mode B: Voice Alchemist

Apply approved voice profiles to rewrite manuscript with stronger characterization.

### Activation

> Ready to apply voice profiles. Please confirm:
> 1. Voice profiles to use (from Cartographer or uploaded)
> 2. Manuscript to process
> 3. Chunk size preference (scene / chapter)
> 4. Output format (revised text only / with change highlights)

### Phase B1: Setup

1. Load voice profiles
2. Load manuscript inventory
3. Identify which characters appear in which scenes
4. Plan processing order

### Phase B2: Chunk Processing

For each chunk:

**Step 1: Context Loading**
- Load chunk text
- Load voice profiles for characters present
- Load any relevant style constraints

**Step 2: Voice Enhancement**

Apply voice profile to:
- **Dialogue:** Rewrite to match character's speech patterns, vocabulary, verbal tics
- **Internal monologue (POV):** Adjust thought style, observation priorities, self-perception
- **Action beats:** Align with character's emotional expression style
- **Dialogue tags:** Minimize per voice profile preferences

**Constraints:**
- Preserve ALL plot events
- Preserve ALL information conveyed
- Preserve emotional trajectory
- Do NOT add memories, backstory, realizations

**Step 3: Fidelity Validation**

Invoke content-fidelity-validator:
- Original: chunk before rewrite
- Revised: chunk after rewrite
- Authorized: voice enhancement only (no new content)

**If PASS:** Accept chunk, continue
**If FAIL:** Log to review queue, mark with inline annotations, continue

**Step 4: Output**

```markdown
## Chunk: [Unit_ID]

### Characters Present
[List with voice profile references]

### Revised Text
[Full rewritten chunk]

### Voice Enhancements Applied
- [Character A]: [specific changes made]
- [Character B]: [specific changes made]

### Fidelity Status
[PASS / FAIL — see review queue]
```

### Phase B3: Batch Summary

After all chunks processed:

```markdown
# Voice Alchemist Batch Summary

**Session:** [datetime]
**Manuscript:** [name]
**Profiles Applied:** [list]

## Processing Results
- Chunks processed: [total]
- Fidelity PASS: [count]
- Fidelity FAIL (in review queue): [count]

## Voice Enhancement Summary
| Character | Chunks Affected | Key Patterns Applied |
|-----------|-----------------|---------------------|
| [Name] | [X] | [summary] |

## Review Required
[X] chunks flagged for content injection. See `fidelity-review-queue.md`.

## Output Location
Revised manuscript: [path]
```

---

## Mode C: Voice Tuner

Generate targeted Fix List for voice enhancement opportunities.

### Activation

> Ready to generate voice enhancement suggestions. Please provide:
> 1. Voice profiles (from Cartographer or uploaded)
> 2. Target scenes/chapters
> 3. Specific concerns? (e.g., "Darnell needs more profanity under stress")

### Phase C1: Voice Injection Point Detection

Scan target text for opportunities:

**Dialogue Opportunities:**
- Generic dialogue that could be more distinctive
- Missing verbal tics where expected
- Vocabulary mismatches with profile
- Emotional moments lacking voice color

**Internal Monologue Opportunities (POV):**
- Flat internal voice
- Missing self-deprecating humor (if profiled)
- Observation mismatches (noticing wrong things first)
- Thought rhythm inconsistencies

**Action Beat Opportunities:**
- Generic action beats that could show character
- Missing emotional expression patterns
- Dialogue tags that could be action beats

### Phase C2: Generate Fix List

Output in noir-mystery-qa compatible format:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIX ID: V01-F01
SEVERITY: Medium
SCENE: [filename or Unit_ID]
LOCATION: "[5-25 word quote]" (para X)
ISSUE TYPE: Voice Consistency
CHARACTER: [Name]
PROFILE REF: [trait from profile being violated/underused]
WHY: [1-3 sentences explaining the voice opportunity]
SAFE FIX:
  - [stepwise instruction]
  - Guardrails: preserve meaning, no new content
MICRO-REWRITE:
  Original: "[current text]"
  Suggested: "[voice-enhanced version]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Phase C3: Validation

For each suggested micro-rewrite:
- Run content-fidelity-validator
- Mark any that fail validation
- Provide safer alternatives

---

## Voice Profile Format (V2)

This format supersedes novel-drafter's original voice profile template.

```markdown
# Voice Profile: [CHARACTER NAME]
Version: 2.0
Generated: [datetime]
Source: [manuscript name]

## Quick Reference
| Field | Value |
|-------|-------|
| Role | [POV / Major Supporting / Minor] |
| Archetype(s) | [Primary] + [Secondary influence] |
| Pulp Level | [1-5] |
| Profanity | [none/mild/moderate/heavy/contextual] |

---

## Speech Patterns

### Structure
- Sentence length: [X words typical, Y under stress]
- Complexity: [simple/compound/complex]
- Fragments: [frequent/occasional/rare]
- Questions: [interrogative/rhetorical/rare]

### Vocabulary
- Register: [formal/casual/technical/vernacular]
- Jargon domain: [if applicable]
- Forbidden words: [words this character would never use]
- Signature words: [words they overuse]

### Verbal Markers
- Tics: "[phrase 1]", "[phrase 2]"
- Filler: [um/uh/well/like/none]
- Profanity: [specific words, triggers]
- Contractions: [always/sometimes/never]

### Response Patterns
- Under pressure: [terse/verbose/deflecting]
- When lying: [over-detail/under-detail/redirect]
- When emotional: [suppress/explode/deflect humor]

---

## Internal Voice (POV Only)

### Thought Style
- Articulation: [more/less/same as speech]
- Structure: [analytical/emotional/fragmented/flowing]
- Self-address: [first person/second person/name]

### Observation Priority
1. [What they notice first]
2. [What they notice second]
3. [What they tend to miss]

### Self-Perception
- Self-image: [how they see themselves]
- Blind spots: [what they don't see about themselves]
- Humor: [self-deprecating level, triggers]

---

## Emotional Expression

### Default State
- Baseline: [calm/anxious/guarded/etc.]
- Mask: [what they project vs feel]

### Under Stress
- Physical tells: [specific mannerisms]
- Verbal shifts: [how speech changes]
- Internal shifts: [how thoughts change]

### Specific Triggers
| Trigger | Response |
|---------|----------|
| [situation] | [specific response pattern] |

---

## Pulp Calibration

**Level: [1-5]**

### At This Level, Apply:
- Simile frequency: [none/occasional/frequent]
- Wise-crack frequency: [none/occasional/frequent]
- Prose sparseness: [standard/lean/bone-dry]
- Poetic touches: [none/subtle/bold]

### Example at Current Level:
**Before (Level 1):**
> "The bar was dark and smelled of beer."

**After (Level [X]):**
> "[Rewritten at selected pulp level]"

---

## Sample Dialogue

### Characteristic Lines
> "[Line 1 showing voice]" — [Unit_ID]
> "[Line 2 showing voice]" — [Unit_ID]
> "[Line 3 showing voice]" — [Unit_ID]

### Internal Monologue Sample (POV)
> "[Sample thought showing internal voice]" — [Unit_ID]

---

## Voice Contrast

Distinct from [other character] because:
- [Specific contrast point 1]
- [Specific contrast point 2]

---

## Application Notes

When applying this profile:
- [Specific guidance for this character]
- [Common pitfalls to avoid]
- [Integration notes with other characters]
```

---

## Manuscript Handling

### Scrivener Folders

- Navigate folder structure
- Identify scene files by naming patterns
- Preserve file organization
- Write revised files alongside originals (or overwrite per user preference)

### Single Files (Word/Markdown)

- Detect scene/chapter breaks
- Process as chunks
- Output single revised file or chunked files

### Output Options

1. **In-place revision:** Overwrite original files
2. **Parallel output:** Create `-revised` versions alongside originals
3. **Single compiled file:** Assemble all chunks into one document

---

## Integration Points

### canon-creator

- Can receive character data from canon-creator's character sheets
- Enhances Voice & Communication section with full V2 profile
- Exports profiles back to canon for reference

### manuscript-revision-orchestrator

- Voice profiles become a "Canon" source type
- Voice enhancement becomes an authorized change category
- Fidelity validation integrated into MODE C→D

### noir-mystery-qa

- Mode C output is compatible with Fix List format
- Can run voice QA as part of larger QA workflow
- Voice consistency added to evaluation categories

### content-fidelity-validator

- Automatically invoked after every rewrite
- Batch processing continues on failure
- Review queue collects all flagged chunks

---

## Working Directory

```
/home/claude/voice-working/
├── config/
│   ├── genres.md                # Declared genres
│   └── session-settings.md      # Chunk size, output prefs
├── samples/                     # Phase A1 output (compact, ~2-3KB each)
│   └── [character-name]-sample.md
├── analysis/
│   ├── dialogue-corpus/
│   │   └── [character-name].md  # Full extracted dialogue (subagent only)
│   └── pattern-detection.md     # Detected patterns
├── archetypes/
│   └── generated-archetypes.md  # Genre-specific archetypes
├── profiles/
│   └── [character-name].md      # Finalized voice profiles (V2)
├── processing/
│   ├── [unit-id]-original.md
│   ├── [unit-id]-revised.md
│   └── chunk-log.md
├── review/
│   └── fidelity-review-queue.md # Failed validations
└── output/
    ├── revised-manuscript/
    └── batch-summary.md
```

---

## Reference Files

- `references/voice-archetypes.md` — Full archetype library by genre
- `references/pulp-calibration.md` — Examples at each pulp level
- `references/voice-profile-v2-spec.md` — Complete V2 format specification
