# Knowledge Tracking

POV knowledge state management and reveal protection for mysteries and thrillers.

---

## Purpose

In stories with hidden information, readers and characters learn things at specific moments. This system:

1. Tracks what each POV character knows at any given point
2. Prevents characters from acting on information they don't have
3. Protects reveals by blocking premature disclosure
4. Maintains mystery integrity through the drafting process

---

## Knowledge State Model

### The Three Knowledge Pools

```
┌─────────────────────────────────────────┐
│           READER KNOWLEDGE              │
│  (What the reader knows at this point)  │
├─────────────────────────────────────────┤
│         CHARACTER KNOWLEDGE             │
│ (What this POV character knows/suspects)│
├─────────────────────────────────────────┤
│            STORY TRUTH                  │
│   (What is actually true in the story)  │
└─────────────────────────────────────────┘
```

**Dramatic irony:** Reader knows more than character
**Suspense:** Reader knows danger character doesn't
**Mystery:** Reader and character learn together
**Twist:** Reader and character had incomplete/wrong information

### Knowledge Categories

**KNOWS:** Character has this information confirmed
- Source: saw it, was told reliably, experienced it
- Can act on this information
- Can think about this information

**SUSPECTS:** Character has reason to believe but not confirm
- Source: inference, unreliable witness, partial information
- Can act cautiously on this
- Can wonder about this

**DOESN'T KNOW:** Character lacks this information
- Cannot act on it
- Cannot think about it specifically
- Can have vague unease without specifics

**BELIEVES FALSELY:** Character holds incorrect information
- Will act on false belief
- Revelation creates moment when truth emerges

---

## Setup: Knowledge State Initialization

### Step 1: Identify Secrets/Reveals

From the outline, list all hidden information:

```markdown
## Secrets Registry

### Secret: S-001 — [Brief description]
**The truth:** [What is actually true]
**Reveal scene:** [Unit_ID where revealed]
**Type:** Whodunit / Howdunit / Whydunit / Hidden relationship / Hidden past / Other

### Secret: S-002 — [Brief description]
[Continue for all secrets]
```

### Step 2: Map Initial Knowledge States

For each POV character, establish what they know at story start:

```markdown
## Initial Knowledge States

### [Character A] — Starting Knowledge

**KNOWS:**
- [Fact 1]
- [Fact 2]

**SUSPECTS:**
- [Suspicion 1]

**DOESN'T KNOW:**
- S-001: [The secret]
- S-002: [Another secret]

**BELIEVES FALSELY:**
- [False belief, if any]

---

### [Character B] — Starting Knowledge
[Continue for each POV character]
```

### Step 3: Create Reveal Timeline

Map when each secret is revealed to whom:

```markdown
## Reveal Timeline

| Secret | Revealed to | In Scene | How |
|--------|-------------|----------|-----|
| S-001 | Reader | U-023 | Dramatic irony (shown before protagonist knows) |
| S-001 | [Character A] | U-045 | Discovery |
| S-002 | Reader + [Character B] | U-034 | Confession |
```

---

## Per-Scene Knowledge Check

### Before Drafting Each Scene

1. **Load current knowledge state** for POV character
2. **Check secrets registry** — is anything revealed this scene?
3. **Note knowledge asymmetry** — does reader know more than character?

### During Drafting

For each internal thought or observation:

```
Is [POV character] thinking about [topic]?
    │
    ├─► Does [POV character] KNOW this? ─► YES ─► OK to include
    │
    ├─► Does [POV character] SUSPECT this? ─► YES ─► OK as uncertainty
    │
    └─► Does [POV character] NOT KNOW this? ─► BLOCKED ─► Cannot include
```

### After Drafting Each Scene

Update knowledge states:

```markdown
## Knowledge Update: [Unit_ID]

### [POV Character] learns:
- [New fact] — Source: [how learned]

### [POV Character] now suspects:
- [New suspicion] — Basis: [what prompted]

### [POV Character] still doesn't know:
- [Important gap]
```

---

## Reveal Protection System

### Early Reveal Detection

Scan drafted text for knowledge violations:

**Pattern 1: Direct statement of unknown**
```
BLOCKED: She knew Marcus had killed his brother.
REASON: S-003 not revealed until U-045
```

**Pattern 2: Thinking about unrevealed specifics**
```
BLOCKED: The memory of that night at the warehouse haunted her.
REASON: Character doesn't know about warehouse until U-034
```

**Pattern 3: Acting on unknown information**
```
BLOCKED: She drove straight to Marcus's cabin.
REASON: Character doesn't know about cabin until U-028
```

**Pattern 4: Noticing unrevealed details**
```
BLOCKED: She noticed the scar on his wrist—the one from that night.
REASON: Scar significance not revealed until U-056
```

### Allowed References

**Vague unease (no specifics):**
```
OK: Something about his story didn't sit right, though she couldn't say what.
```

**General suspicion (without unrevealed basis):**
```
OK: She didn't trust him. Couldn't explain why, but her instincts said run.
```

**Noticing without understanding:**
```
OK: She noticed a scar on his wrist but looked away before he caught her staring.
```

### Rewrite Strategies

When a blocked line is detected, rewrite to preserve dramatic intent without violating knowledge:

**Original (blocked):**
```
Sarah thought about the murder weapon hidden in Marcus's desk.
```

**Rewrite options:**

Option A — Remove entirely:
```
Sarah's mind raced, but she couldn't focus.
```

Option B — Make vague:
```
Something about Marcus's office made her uneasy. What was he hiding?
```

Option C — Redirect to known information:
```
Sarah remembered Marcus's reaction when she'd mentioned the case. Too casual. Too quick to change the subject.
```

---

## Knowledge State File Format

Maintain in `/home/claude/draft-working/config/knowledge-states.md`:

```markdown
# Knowledge State Tracker

**Manuscript:** [title]
**Last updated:** [datetime]
**Current scene:** [Unit_ID]

---

## Secrets Registry

### S-001: [Title]
- **Truth:** [The actual truth]
- **Reveal scene:** [Unit_ID]
- **Reader learns:** [Unit_ID]
- **[Character A] learns:** [Unit_ID]
- **[Character B] learns:** [Unit_ID or "Never"]

[Continue for all secrets]

---

## Current Character States

### [Character A] — as of [Unit_ID]

**KNOWS:**
- [Fact 1]
- [Fact 2]
- [Learned in U-XXX: new fact]

**SUSPECTS:**
- [Suspicion 1]

**DOESN'T KNOW:**
- S-001, S-003

**BELIEVES FALSELY:**
- [False belief]

---

### [Character B] — as of [Unit_ID]
[Continue for each POV character]

---

## Reveal Log

| Scene | Character | Secret | Type | Notes |
|-------|-----------|--------|------|-------|
| U-023 | Reader | S-001 | Dramatic irony | Reader sees Marcus hide the gun |
| U-034 | Sarah | S-002 | Discovery | Sarah finds the letter |
| U-045 | Sarah | S-001 | Confrontation | Marcus confesses |

---

## Pending Reveals

| Secret | Scheduled | Character(s) | Setup required |
|--------|-----------|--------------|----------------|
| S-003 | U-056 | All | Need to plant seed in U-040 |
```

---

## Validation Checkpoints

### Scene-Level Validation

After drafting each scene:

- [ ] POV character only acts on known information
- [ ] POV character only thinks about known/suspected information
- [ ] Reader doesn't learn secrets before scheduled reveal
- [ ] Knowledge updates logged

### Chapter-Level Validation

After each chapter:

- [ ] All character knowledge states current
- [ ] No early reveals detected
- [ ] Dramatic irony maintained where intended
- [ ] Suspicions building appropriately

### Act-Level Validation

After each act:

- [ ] Major reveals occurred at planned points
- [ ] Character knowledge progresses logically
- [ ] Reader knows appropriate amount for story stage
- [ ] No plot holes from knowledge violations

---

## Common Knowledge Errors

### Error 1: The Convenient Realization

**Problem:** Character suddenly "realizes" something with no basis
```
✗ It hit her then—Marcus had been at the warehouse that night.
[But she has no reason to think this]
```

**Fix:** Establish basis for realization or cut it

### Error 2: The Psychic POV

**Problem:** POV character knows other character's thoughts
```
✗ She saw the guilt in his eyes. He was remembering how he'd killed her.
[She can't know what he's remembering]
```

**Fix:** Only show observable behavior
```
✓ She saw something in his eyes. Guilt? Fear? He looked away too quickly.
```

### Error 3: The Leaky Internal Monologue

**Problem:** Character thinks about unrevealed facts
```
✗ The secret had weighed on her for years—knowing what Marcus had done.
[But she doesn't know yet]
```

**Fix:** Replace with vague unease or appropriate thoughts

### Error 4: The Author's Voice Intrusion

**Problem:** Narration reveals information POV character doesn't have
```
✗ She walked past the desk where the murder weapon was hidden.
[Third limited POV shouldn't know this if character doesn't]
```

**Fix:** Keep narration limited to POV character's knowledge

### Error 5: The Premature Suspicion

**Problem:** Character suspects correctly too early without basis
```
✗ From the moment she met Marcus, Sarah suspected he was the killer.
[This makes the mystery feel arbitrary]
```

**Fix:** Build suspicion from evidence, not intuition
```
✓ Something about Marcus set her on edge, though she couldn't explain why.
```

---

## Mystery-Specific Considerations

### Fair-Play Knowledge

For mysteries with fair-play rules:
- Reader must have access to all necessary clues before reveal
- Track when each clue becomes available to reader
- Ensure detective doesn't use information reader doesn't have

### Red Herring Knowledge

For intentional misdirection:
- Track what reader is meant to believe at each point
- Track when misdirection is corrected
- Ensure red herrings are planted, not just stated

### Multiple Suspects Knowledge

When multiple characters could be guilty:
- Track which suspects reader knows about
- Track evidence for/against each
- Ensure final answer is one of presented options (unless intentional subversion)

---

## Integration Notes

### With character-voice-architect

Voice profiles may include:
- What character is good at noticing
- What character tends to miss
- How character processes suspicion

Apply these to knowledge tracking:
- Observant characters notice clues more readily
- Oblivious characters miss obvious signs
- Suspicious characters suspect more, trust less

### With content-fidelity-validator

Knowledge violations are a form of content injection:
- Adding knowledge character doesn't have = unauthorized addition
- Early reveals = meaning alteration
- Flag and block accordingly
