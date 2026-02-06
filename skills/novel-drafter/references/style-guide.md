# Style Guide

Style configuration options and question flow for novel-drafter setup phase.

---

## Style Configuration Overview

Before drafting begins, establish consistent style parameters that will apply across the entire manuscript.

---

## Style Discovery Questions

Ask these questions in order. User may answer in detail or defer to defaults.

### 1. Genre and Subgenre

> What genre is this work?
>
> **Primary genre:**
> - [ ] Mystery
> - [ ] Thriller
> - [ ] Horror
> - [ ] Romance
> - [ ] Science Fiction
> - [ ] Fantasy
> - [ ] Literary Fiction
> - [ ] Crime/Noir
> - [ ] Historical
> - [ ] Other: ________
>
> **Subgenre (optional):**
> [Examples: cozy mystery, psychological thriller, urban fantasy, etc.]

**Why it matters:** Genre sets expectations for tone, pacing, and prose style. See genre conventions below.

### 2. Point of View

> What point of view will this be written in?
>
> - [ ] **First person** ("I walked into the bar...")
> - [ ] **Third person limited** ("She walked into the bar...")
> - [ ] **Third person omniscient** ("She walked into the bar, unaware that Marcus watched from the shadows...")
> - [ ] **Multiple POV** (switching between characters)
>
> If multiple POV:
> - How will POV switches be marked? (chapter breaks / scene breaks / unmarked)
> - Which characters are POV characters? [list]

**Default:** Third person limited

### 3. Tense

> What tense?
>
> - [ ] **Past tense** ("She walked into the bar...")
> - [ ] **Present tense** ("She walks into the bar...")

**Default:** Past tense

### 4. Prose Density

> How dense should the prose be?
>
> - [ ] **Spare/Minimalist** — Short sentences, minimal description, action-focused. (Hemingway, Elmore Leonard)
> - [ ] **Balanced** — Mix of description and action, moderate sentence variety. (Most commercial fiction)
> - [ ] **Lush/Descriptive** — Rich description, longer sentences, atmosphere-heavy. (Literary fiction, some fantasy)

**Default:** Balanced

### 5. Dialogue-to-Narration Ratio

> How much dialogue vs. narration?
>
> - [ ] **Dialogue-heavy** — Story told primarily through character speech, minimal narration between
> - [ ] **Balanced** — Mix of dialogue scenes and narrative passages
> - [ ] **Narration-heavy** — More internal monologue and description, dialogue punctuates

**Default:** Balanced

### 6. Tone

> What's the overall tone?
>
> - [ ] **Dark** — Heavy themes, moral ambiguity, consequences
> - [ ] **Light** — Humor, warmth, hopeful undertones
> - [ ] **Mixed** — Varies by scene, contrast between dark and light

**Default:** Mixed

### 7. Pacing Preference

> How should pacing feel?
>
> - [ ] **Fast** — Short scenes, quick cuts, propulsive momentum
> - [ ] **Measured** — Room to breathe, character moments between action
> - [ ] **Variable** — Varies by act (e.g., slow build in Act I, fast in Act III)

**Default:** Variable

### 8. Sample Passages (Optional)

> Do you have any sample passages that exemplify your desired voice?
>
> If yes, please provide 1-3 samples (from your own writing or published works you want to emulate).

Sample passages help calibrate voice more precisely than descriptors alone.

---

## Genre Conventions Reference

### Mystery

**Pacing:** Measured, with escalation toward reveal
**Prose:** Clear, detail-oriented, observational
**Dialogue:** Interrogative, subtext-heavy
**Structure:** Clue distribution, fair-play considerations
**Word count range:** 70,000-90,000

### Thriller

**Pacing:** Fast, relentless momentum
**Prose:** Lean, action-focused
**Dialogue:** Terse, high-stakes
**Structure:** Cliffhangers, ticking clocks
**Word count range:** 80,000-100,000

### Noir/Crime

**Pacing:** Variable (can be slow burn or fast)
**Prose:** Stylized, voice-driven, simile-rich
**Dialogue:** Wise-cracks, subtext, verbal sparring
**Structure:** Moral ambiguity, consequences
**Word count range:** 60,000-80,000

### Horror

**Pacing:** Slow build with intense peaks
**Prose:** Atmospheric, sensory
**Dialogue:** Sparse during tension, naturalistic
**Structure:** Dread building, release
**Word count range:** 70,000-90,000

### Romance

**Pacing:** Emotional beats drive pace
**Prose:** Emotionally rich, internal focus
**Dialogue:** Chemistry, banter, vulnerability
**Structure:** Meet-cute, complications, resolution
**Word count range:** 50,000-100,000 (varies by subgenre)

### Science Fiction

**Pacing:** Variable by subgenre
**Prose:** Clear world-building, technical when needed
**Dialogue:** Character voice distinct from world voice
**Structure:** Concept integration with character
**Word count range:** 80,000-120,000

### Fantasy

**Pacing:** Often measured, epic can be slow
**Prose:** Rich world-building, can be lush
**Dialogue:** Varies by setting (avoid faux-medieval)
**Structure:** World and magic system support story
**Word count range:** 90,000-150,000

### Literary Fiction

**Pacing:** Character-driven, can be slow
**Prose:** Stylistically distinctive, often dense
**Dialogue:** Naturalistic, thematic
**Structure:** Theme over plot
**Word count range:** 60,000-100,000

---

## Style Settings File Format

Store configuration in `/home/claude/draft-working/config/style.md`:

```markdown
# Style Configuration

**Generated:** [datetime]
**Manuscript:** [title]

---

## Core Settings

| Setting | Value |
|---------|-------|
| Genre | [genre] |
| Subgenre | [subgenre or "None"] |
| POV | [first/third limited/third omniscient/multiple] |
| Tense | [past/present] |
| Prose density | [spare/balanced/lush] |
| Dialogue ratio | [dialogue-heavy/balanced/narration-heavy] |
| Tone | [dark/light/mixed] |
| Pacing | [fast/measured/variable] |

---

## POV Configuration (if multiple)

| Character | POV Type | Switch Marker |
|-----------|----------|---------------|
| [name] | [1st/3rd] | [chapter/scene/unmarked] |

---

## Sample Passages

### User-provided sample 1
> [Sample text]

**Note:** [What this exemplifies]

### User-provided sample 2
> [Sample text]

**Note:** [What this exemplifies]

---

## Genre-Specific Considerations

[Notes based on selected genre from conventions above]

---

## Application Notes

- Apply [setting] by [specific guidance]
- Avoid [common pitfall for this genre]
- Emphasize [key element]
```

---

## Applying Style During Drafting

### Scene-Level Style Checklist

Before drafting each scene, verify:

- [ ] POV character established
- [ ] Tense consistent
- [ ] Prose density appropriate for scene type
- [ ] Dialogue/narration balance fits scene purpose
- [ ] Tone matches scene content

### Style Consistency Checks

At chapter checkpoints:

- [ ] No POV drift (stayed in correct character's head)
- [ ] No tense shifts (past stayed past)
- [ ] Prose density consistent
- [ ] Dialogue ratio in range
- [ ] Tone serves story

### Genre Compliance

For genre fiction, verify:

- [ ] Genre conventions respected
- [ ] Genre reader expectations met
- [ ] Genre-specific pacing maintained
- [ ] Genre vocabulary appropriate

---

## Common Style Mistakes

### POV Violations

**Head-hopping:** Jumping between character thoughts without scene break
```
✗ Sarah wondered if he was lying. Marcus knew he couldn't tell her the truth.
✓ Sarah wondered if he was lying. His face gave nothing away.
```

**Perspective breach:** POV character knows things they can't
```
✗ She didn't notice him watching from across the room. [How does she know?]
✓ She scanned the room, missing the figure in the corner shadows.
```

### Tense Shifts

**Accidental present in past narrative:**
```
✗ She walked to the door. It opens slowly. She stepped inside.
✓ She walked to the door. It opened slowly. She stepped inside.
```

### Prose Density Drift

**Getting lush when should be spare:**
```
Spare style: She entered. The room was dark. Someone had been here.
[Don't drift to]: She entered the cavernous chamber, shadows pooling in corners like 
spilled ink, the musty air thick with secrets and the unmistakable residue of recent 
occupation.
```

### Dialogue Tag Inflation

**Over-tagging:**
```
✗ "I don't know," she said nervously, her voice trembling with uncertainty.
✓ "I don't know." Her hands wouldn't stay still.
```

---

## Style Calibration by Scene Type

### Action Scenes

- Shorter sentences
- More verbs, fewer adjectives
- Dialogue sparse or absent
- Sensory focus on immediate

### Dialogue Scenes

- Balance speech with beats
- Subtext over on-the-nose
- Character voice distinct
- Pacing through exchange rhythm

### Emotional Scenes

- Interiority increases
- Sensory details support emotion
- Pace slows
- Dialogue becomes weighted

### Exposition Scenes

- Information woven into action
- Character motivation for learning
- Avoid lecture mode
- Break up with reaction beats

### Transitional Scenes

- Brief, purposeful
- Maintain momentum
- Setup without telegraphing
- Character reflection if needed

---

## Defaults Summary

If user defers all choices:

| Setting | Default |
|---------|---------|
| POV | Third person limited |
| Tense | Past |
| Prose density | Balanced |
| Dialogue ratio | Balanced |
| Tone | Mixed |
| Pacing | Variable |

Genre defaults apply additional conventions based on genre selection.
