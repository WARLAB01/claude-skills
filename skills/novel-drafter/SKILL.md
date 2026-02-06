---
name: novel-drafter
description: Generate first-draft prose from a structured outline (typically from novel-outliner). Use when the user wants to turn an outline with beat sheets into actual prose for a short story, novella, or novel. Handles style consistency, character voice profiles (V2 format), POV knowledge tracking, and automatic reveal protection for mysteries. Includes chapter/act validation checkpoints. Triggers include "draft my novel from this outline," "turn this outline into prose," "write the first draft," or requests to generate story prose from structured outlines.
---

# Novel Drafter

Generate first-draft prose from structured outlines with built-in consistency checking, character voice management, and mystery reveal protection.

## Input Requirements

This skill expects a structured outline containing:
- **Synopsis**: Overall story summary
- **Scene hierarchy**: Act → Chapter → Scene with summaries
- **Beat sheets**: Scene-by-scene narrative beats

The **novel-outliner** skill produces this exact format. Other outline formats can work if they contain equivalent information.

## Output

Single file (docx preferred, markdown fallback) containing:
- Complete first-draft prose
- Chapter/scene markers for easy navigation
- Appended validation log (issues found and resolved)

## Related Skills

| Skill | Relationship |
|-------|--------------|
| **novel-outliner** | Produces the input for this skill |
| **novel-workflow** | Reference for genre conventions, word count guidance |
| **character-voice-architect** | Provides V2 voice profiles, can refine profiles interactively |
| **canon-creator** | Can provide character data and voice profile drafts |

## Core Workflow

### Phase 1: Setup (Interactive)

This phase is conversational. Gather all necessary information before drafting.

**Step 1: Receive Outline**
- User uploads outline (from novel-outliner or equivalent)
- Validate structure: Does it have synopsis, scene hierarchy, beat sheets?
- If missing elements, ask user to provide or use novel-outliner first

**Step 2: Style Configuration**
See `references/style-guide.md` for detailed question flow.

If user hasn't specified style, ask about:
- Genre and subgenre (reference novel-workflow for conventions)
- POV type (first person, third limited, third omniscient, multiple POV)
- Tense (past, present)
- Prose density (spare/minimalist, balanced, lush/descriptive)
- Dialogue-to-narration ratio (dialogue-heavy, balanced, narration-heavy)
- Tone (dark, light, mixed)
- Pacing preference (fast, measured, variable)

User may also provide sample passages that exemplify desired voice.

**Step 3: Character Voice Profiles**

Check for existing V2 voice profiles:
- From canon-creator output
- From character-voice-architect
- User-uploaded profiles

**If V2 profiles exist:**
- Load and confirm profiles are current
- Ask if user wants to refine any profiles

**If no profiles exist:**
- Analyze outline to identify major characters:
  - POV characters (anyone with a POV scene)
  - Frequent dialogue characters (appear in multiple scenes)
- For each major character, either:
  - **Option A:** Run character-voice-architect Mode A for full interactive profile building
  - **Option B:** Create simplified profile with these questions:
    - "How does [Character] speak? Any verbal tics, vocabulary level, speech patterns?"
    - "How does [Character] think? (for POV characters) Internal monologue style?"
    - "What archetype(s) fit this character?" (show archetype menu)
    - "Pulp level (1-5) for this character?"
- Create V2 voice profile for each major character

**Note:** For complex voice work or existing manuscripts, use character-voice-architect Mode A for full interactive profile building with archetype menus and trait picking.

**Step 4: Knowledge State Initialization**
See `references/knowledge-tracking.md` for setup.

For mysteries/thrillers with hidden information:
- Identify all secrets/reveals in the outline
- Map when each reveal occurs (which scene)
- For each POV character, establish starting knowledge state
- Create knowledge progression timeline

**Step 5: Confirm Configuration**
Before drafting, summarize:
- Style settings
- Character voice profiles (brief)
- Reveal timeline (if applicable)
- Estimated output length (reference novel-workflow for genre norms)

Get user confirmation to proceed.

### Phase 2: Drafting (Automated with Checkpoints)

**Initialize Working Directory**
Before drafting, run the initialization script:
```bash
python3 scripts/init_draft_dir.py [num_acts] [chapters_per_act]
```
Default: 3 acts, 4 chapters each. Adjust based on outline structure.

To add character voice profile templates:
```bash
python3 scripts/init_draft_dir.py --add-character "Character Name"
```

Process scene-by-scene, with validation at chapter and act boundaries.

**Scene Drafting Process**

For each scene:
1. Load scene beats from outline
2. Identify POV character and their current knowledge state
3. Apply style settings and character voice profile (V2 format)
4. Draft prose from beats
5. Run reveal protection check (see `references/knowledge-tracking.md`)
6. If early reveal detected → rewrite avoiding the reveal, log what was avoided
7. Save to working file

**Chapter Checkpoint**

After completing each chapter:
1. Run validation (see `references/validation-checkpoints.md`)
2. Generate consistency report:
   - Characters who appeared
   - Timeline verification (does time flow correctly?)
   - Knowledge state changes (what did POV characters learn?)
   - Reveals: what was revealed, what was protected
   - **Voice consistency: did characters maintain their profiles?**
3. Auto-correct any issues found
4. Log issues and corrections
5. Continue to next chapter

**Act Checkpoint**

After completing each act:
1. Run full act validation
2. Extended consistency report:
   - All chapter reports summarized
   - Arc progression check (does the act accomplish its purpose?)
   - Pacing assessment
   - Character appearance frequency
   - **Voice drift check: any characters deviating from profiles?**
3. Log and continue

### Phase 3: Assembly

After all scenes drafted:

1. Compile all chapter working files into single document
2. Add chapter/scene markers for navigation
3. Append validation log as appendix
4. Export to docx (preferred) or markdown
5. Save to `/mnt/user-data/outputs/`
6. Present to user

## Working Directory Structure

```
/home/claude/draft-working/
├── config/
│   ├── style.md              # Style settings
│   ├── characters/           # V2 Voice profiles per character
│   │   ├── [character-1].voice.md
│   │   └── [character-2].voice.md
│   └── knowledge-states.md   # POV knowledge tracking
├── act-1/
│   ├── chapter-1.1/
│   │   ├── scene-1.1.1.md    # Drafted prose
│   │   ├── scene-1.1.2.md
│   │   └── chapter-report.md # Validation report
│   └── chapter-1.2/
│       └── ...
├── act-2/
│   └── ...
├── validation-log.md         # Running log of all issues/corrections
└── final/
    └── draft.md              # Assembled output
```

## Reference Files

- `references/style-guide.md` — Style questions, configuration options, genre conventions integration
- `references/character-voice.md` — V2 voice profile format, consistency checking during drafting
- `references/knowledge-tracking.md` — POV knowledge states, reveal protection, early-reveal detection
- `references/validation-checkpoints.md` — Chapter/act validation checklists, consistency reports

## Reveal Protection System

For mysteries, thrillers, and stories with hidden information:

1. **Map reveals**: Before drafting, identify when each secret is revealed
2. **Track knowledge**: Each POV character has a knowledge state that updates scene-by-scene
3. **Check during drafting**: Before a POV character can think/notice/react to something, verify they know it
4. **Auto-prevent**: If a line would reveal information early, rewrite it
5. **Log**: Record what was prevented and why

Example:
```
Scene 2.3.1 (April POV):
PREVENTED: Internal thought referencing guilt about the murder
REASON: Reader should not know April is the killer until Scene 4.2.3
REPLACEMENT: Redirected internal monologue to anxiety about the investigation
```

## Word Count Guidance

Word count varies by genre and format. If unsure, the skill will:
1. Reference novel-workflow's genre-craft.md for typical lengths
2. Ask user about target length
3. Calibrate scene prose length accordingly

**General ranges:**
- Short story: 1,000-7,500 words
- Novelette: 7,500-17,500 words
- Novella: 17,500-40,000 words
- Novel: 40,000-100,000+ words

Scene length is derived from total target ÷ number of scenes.
