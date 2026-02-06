# Extraction Patterns

Detailed templates and patterns for extracting canon data from manuscript chunks.

## Extraction Categories

1. Plot Events (→ Synopsis & Outline)
2. Character Data (→ Character Sheets)
3. Mystery Elements (→ Mystery Artifacts)
4. Voice Data (→ Voice Profiles) — see `voice-extraction-patterns.md`
5. World Building (→ Setting Reference)
6. Timeline Data (→ Timeline Tracker)

---

## 1. Plot Event Extraction

### Scene-Level Template

For each scene in the chunk:

```markdown
### Scene Extraction: [Unit_ID]

**Metadata:**
- POV Character: [name]
- Location: [specific place]
- Time: [when this occurs - relative or absolute]
- Word count: [approximate]

**Scene Summary:**
[2-3 sentences capturing what happens]

**Summary Anchor:** "[15-25 word quote that encapsulates scene]"
Location: para [X]

**Scene Beats:**

Beat 1: [What happens first]
- Anchor: "[quote]" (para X)
- Characters involved: [list]
- Stakes: [what's at risk]

Beat 2: [What happens next]
- Anchor: "[quote]" (para X)
- Characters involved: [list]
- Consequence of Beat 1: [how it follows]

[Continue for all significant beats]

**Scene Turn:**
- What changes: [state before → state after]
- Turn anchor: "[quote]" (para X)
- Type: [revelation / decision / action / reversal / escalation]

**Scene Function:**
- [ ] Advances plot
- [ ] Reveals character
- [ ] Builds world
- [ ] Plants clue/seed
- [ ] Pays off earlier setup
- [ ] Raises stakes

**Connections:**
- Sets up: [future scene/event if known]
- Pays off: [earlier scene/event if applicable]
- Conflicts with: [any continuity concerns]
```

### Beat Identification Patterns

**Action beats:** Character does something that changes the situation
```
Indicators: active verbs, physical movement, dialogue that commits
Example: "Sarah pulled her gun and kicked in the door."
```

**Revelation beats:** Character (or reader) learns something
```
Indicators: discovery verbs, reaction to information
Example: "The file confirmed what she'd suspected—Marcus had lied."
```

**Decision beats:** Character commits to a course of action
```
Indicators: decision language, turning point markers
Example: "She couldn't protect him anymore. It was time to tell the truth."
```

**Emotional beats:** Significant emotional shift
```
Indicators: emotional language, physical manifestation of feeling
Example: "The grief hit her then, a wave she couldn't hold back."
```

---

## 2. Character Data Extraction

### Per-Character Template

For each character appearance in chunk:

```markdown
### Character Extraction: [Character Name]

**Scene:** [Unit_ID]
**Role in scene:** POV | Major Supporting | Minor Supporting | Mentioned Only

---

#### Physical Appearance

| Detail | Anchor | Location |
|--------|--------|----------|
| [hair color/style] | "[quote]" | para X |
| [eye color] | "[quote]" | para X |
| [build/height] | "[quote]" | para X |
| [age indicators] | "[quote]" | para X |
| [distinguishing features] | "[quote]" | para X |
| [clothing/style] | "[quote]" | para X |

---

#### Personality/Behavior

| Trait | Evidence | Anchor | Location |
|-------|----------|--------|----------|
| [trait] | [how shown] | "[quote]" | para X |

---

#### Relationships

| Related To | Relationship Type | Evidence | Anchor |
|------------|-------------------|----------|--------|
| [character] | [type: family/romantic/professional/adversarial/etc.] | [how shown] | "[quote]" |

---

#### Backstory Revealed

| Information | Anchor | Location | Reliability |
|-------------|--------|----------|-------------|
| [backstory fact] | "[quote]" | para X | Narrator / Character claim / Flashback |

---

#### Goals/Motivations (this scene)

| Goal | Evidence | Anchor |
|------|----------|--------|
| [what they want] | [how shown] | "[quote]" |

---

#### Conflict/Tension

| Conflict | With | Type | Status |
|----------|------|------|--------|
| [what] | [whom/what] | Internal/External | Active/Resolved/Escalated |
```

### Character Identification

**Named characters:** Extract full name, any aliases/nicknames
```
Pattern: Proper nouns in dialogue attribution, introduction patterns
"Call me [Name]", "[Name] walked in", "Detective [Name]"
```

**Unnamed but significant:** Track by descriptor
```
Pattern: Repeated descriptors, significant actions
"the bartender", "the woman in red", "his contact"
Note: Flag for user to provide name or confirm tracking descriptor
```

**Mentioned only:** Characters referenced but not present
```
Pattern: Third-party references, memories, backstory
"his ex-wife", "the victim", "her old partner"
Note: Create placeholder entry for potential later appearance
```

---

## 3. Mystery Element Extraction

### Mystery Registry Entry

```markdown
### Mystery: [M-XXX] — [Brief Title]

**Type:** 
- [ ] Central plot mystery (drives main narrative)
- [ ] Subplot mystery (secondary puzzle)
- [ ] Red herring (intentional misdirection)
- [ ] Background mystery (world-building)
- [ ] Character mystery (personal secret)

**The Question:** [What the reader/characters are trying to figure out]

**First Seeded:** 
- Unit_ID: [where first hinted]
- Anchor: "[quote]"
- How seeded: [explicit question / subtle hint / dramatic irony]

**Clues Found (this chunk):**

| Clue | Found by | Unit_ID | Anchor | Fair-play? |
|------|----------|---------|--------|------------|
| [clue] | [character] | [ID] | "[quote]" | Yes/No |

**Red Herrings (this chunk):**

| Misdirection | Target suspect/theory | Unit_ID | Anchor |
|--------------|----------------------|---------|--------|
| [what misleads] | [where it points] | [ID] | "[quote]" |

**Resolution Status:**
- [ ] Unresolved (as of this chunk)
- [ ] Partially resolved: [what's known]
- [ ] Fully resolved in [Unit_ID]

**Resolution Details (if resolved):**
- Answer: [the truth]
- Revealed to: [which characters]
- Anchor: "[quote]"
```

### Truth/Deception/Misunderstanding Entry

```markdown
### [Type]: [T/D/M-XXX] — [Brief Title]

**Type:**
- [ ] Truth (actual fact, known to some)
- [ ] Deception (intentional lie)
- [ ] Misunderstanding (unintentional false belief)

---

**The Reality:**
[What is actually true]

**Reality Anchor:** "[quote]"
Location: [Unit_ID], para X
Reliability: Narrator-confirmed / Character-claim / Inferred

---

**The [Deception/Misunderstanding/Hidden Truth]:**
[What character(s) believe OR what is being hidden]

**Belief Anchor:** "[quote]"
Location: [Unit_ID], para X

---

**Belief Holders:**
| Character | Believes | Since | Anchor |
|-----------|----------|-------|--------|
| [name] | [what they think] | [Unit_ID] | "[quote]" |

**Truth Holders:**
| Character | Knows | Since | Anchor |
|-----------|-------|-------|--------|
| [name] | [the truth] | [Unit_ID] | "[quote]" |

---

**Correction Status:**
- [ ] Not yet corrected
- [ ] Corrected in [Unit_ID] for [characters]
- [ ] Partially corrected: [details]

**Correction Anchor (if applicable):** "[quote]"
```

### Character Awareness Entry

```markdown
### Awareness Update: [Character] — [Unit_ID]

**Scene context:** [1 sentence on what's happening]

---

**LEARNS (confirmed new knowledge):**

| Information | Source | Anchor | Confidence |
|-------------|--------|--------|------------|
| [what learned] | [how/from whom] | "[quote]" | High/Medium/Low |

---

**SUSPECTS (new suspicions, unconfirmed):**

| Suspicion | Basis | Anchor | Accuracy |
|-----------|-------|--------|----------|
| [what suspects] | [why] | "[quote]" | Correct/Incorrect/Partial |

---

**STILL DOESN'T KNOW:**
[List key information this character lacks that reader/other characters know]

---

**BELIEVES FALSELY:**
[List any false beliefs this character holds, with reference to T/D/M entry]
```

---

## 4. World Building Extraction

### Setting Details

```markdown
### Setting: [Location Name]

**First appearance:** [Unit_ID]
**Type:** City / Building / Room / Outdoor / Vehicle / Other

**Physical Description:**

| Detail | Anchor | Location |
|--------|--------|----------|
| [detail] | "[quote]" | para X |

**Atmosphere/Mood:**
[How it feels]
Anchor: "[quote]"

**Significant objects:**

| Object | Significance | Anchor |
|--------|--------------|--------|
| [object] | [why it matters] | "[quote]" |

**Connected locations:**
[How this place relates to others in the story]
```

### World Rules

```markdown
### World Rule: [Rule/Fact]

**Category:** Social / Legal / Physical / Historical / Cultural

**Statement:** [The rule or fact about this world]

**Anchor:** "[quote]"
Location: [Unit_ID], para X

**Implications:** [How this affects the story]

**Consistency check:** [Any other mentions to cross-reference]
```

---

## 5. Timeline Extraction

### Event Timeline Entry

```markdown
### Timeline Entry: [Event]

**Absolute time:** [If stated: date, time]
**Relative time:** [Relation to other events]

**Event:** [What happens]
**Anchor:** "[quote]"
**Location:** [Unit_ID], para X

**Characters involved:** [list]
**Location:** [where]

**Duration:** [How long event takes, if stated]

**Sequence markers:**
- Before: [what comes before]
- After: [what comes after]
- During: [what happens simultaneously]
```

### Timeline Conflict Detection

```markdown
### TIMELINE CONFLICT: [Brief description]

**Conflict:** [Description of impossibility]

**Evidence A:**
- Event: [event 1]
- Time stated: [when]
- Anchor: "[quote]" ([Unit_ID])

**Evidence B:**
- Event: [event 2]
- Time stated: [when]
- Anchor: "[quote]" ([Unit_ID])

**Why conflict:** [Explanation of impossibility]

**Possible resolutions:**
1. [Resolution option 1]
2. [Resolution option 2]

**USER DECISION REQUIRED**
```

---

## Extraction Process Flow

```
For each chunk:

1. FIRST PASS: Plot events
   - Identify scene boundaries
   - Extract scene summaries
   - Identify beats
   - Note scene turns

2. SECOND PASS: Characters
   - List all characters present
   - Extract new physical details
   - Extract new personality evidence
   - Extract relationship information
   - Extract backstory reveals

3. THIRD PASS: Mystery elements (if enabled)
   - Log new clues
   - Log new deceptions/misunderstandings
   - Update character awareness
   - Check fair-play status

4. FOURTH PASS: World and timeline
   - Extract setting details
   - Extract world rules
   - Build timeline entries
   - Check for conflicts

5. VERIFICATION
   - Verify all anchors exist
   - Check for claim mismatches
   - Flag ambiguities
   - Generate chunk report
```

---

## Quality Checklist

Before completing chunk extraction:

- [ ] Every fact has an anchor
- [ ] All anchors are 15-25 words
- [ ] All anchors include location (Unit_ID, para X)
- [ ] No inferences presented as facts
- [ ] Ambiguities flagged
- [ ] Character names consistent
- [ ] Timeline entries don't conflict
- [ ] Mystery clues tagged for fair-play
