# Semantic Comparison Methodology

How to verify that meaning is preserved when text is rewritten.

## Core Principle

**Meaning preservation requires:**
1. Same events occur
2. Same characters perform same actions
3. Same information is conveyed
4. Same emotional trajectory
5. Same causal relationships

**Style changes that preserve meaning:**
- Different word choices for same concepts
- Different sentence structures
- Different rhythm/pacing
- Different voice/register
- Enhanced sensory detail (additive, not alterative)

## Comparison Framework

### Level 1: Event Preservation

Extract core events from both texts:

**Original:** "Sarah entered the room and found the letter on the desk."

Events:
1. Sarah enters room
2. Sarah finds letter
3. Letter is on desk

**Revised:** "Sarah pushed through the door. The letter waited on the desk, white against dark wood."

Events:
1. Sarah enters room (via pushing door)
2. Letter is on desk
3. Implicit: Sarah sees/finds letter

**Assessment:** Events preserved ✓

### Level 2: Agent-Action Preservation

Verify who does what:

| Original | Revised | Match? |
|----------|---------|--------|
| Sarah enters | Sarah pushes through | ✓ Same agent, same action type |
| Sarah finds letter | (implicit) Sarah notices letter | ✓ Same agent, compatible action |

**Flag if:** Agent changes, action changes meaning, or causality reverses.

### Level 3: Information Preservation

Catalog information conveyed:

**Original information:**
- Sarah enters a room
- There is a letter
- Letter is on a desk

**Revised information:**
- Sarah enters a room (via door, with effort)
- There is a letter (white)
- Letter is on a desk (dark wood)

**Assessment:** Original information preserved, details added ✓

**Flag if:** Original information missing or contradicted.

### Level 4: Emotional Trajectory

Track emotional arc:

**Original emotional beats:**
- Neutral entry → discovery → (implied) attention/interest

**Revised emotional beats:**
- Effortful entry → anticipatory detail → focused attention

**Assessment:** Compatible emotional trajectory ✓

**Flag if:** Emotional valence changes (positive→negative, urgent→calm, etc.)

### Level 5: Causal Relationships

Verify cause-effect chains:

**Original:** "Because he was late, she left without him."

Cause: He was late
Effect: She left without him
Relationship: Causation

**Revised:** "His lateness drove her out the door alone."

Cause: His lateness
Effect: She left alone
Relationship: Causation

**Assessment:** Causal relationship preserved ✓

**Flag if:** Cause and effect disconnected, reversed, or new causation introduced.

## Meaning Alteration Categories

### Category A: Agent Substitution

**Problematic:**
- Original: "He opened the door."
- Revised: "She opened the door."
- Issue: Different agent

### Category B: Action Transformation

**Problematic:**
- Original: "She walked to the window."
- Revised: "She ran to the window."
- Issue: Different action implies different emotion/urgency

**Acceptable:**
- Original: "She walked to the window."
- Revised: "She moved to the window."
- Assessment: "Moved" is compatible generalization

### Category C: Object Substitution

**Problematic:**
- Original: "He picked up the knife."
- Revised: "He picked up the gun."
- Issue: Different object changes plot implications

### Category D: Relationship Alteration

**Problematic:**
- Original: "She smiled at him."
- Revised: "She glared at him."
- Issue: Opposite relationship signal

### Category E: Temporal Shift

**Problematic:**
- Original: "He had already left."
- Revised: "He was about to leave."
- Issue: Different temporal relationship to other events

### Category F: Certainty Alteration

**Problematic:**
- Original: "She thought he might be lying."
- Revised: "She knew he was lying."
- Issue: Suspicion upgraded to certainty

**Also problematic:**
- Original: "He was guilty."
- Revised: "He seemed guilty."
- Issue: Fact downgraded to perception

## Semantic Comparison Process

### Step 1: Segment into Units

Break both texts into comparable units:
- Sentences
- Clauses
- Dialogue exchanges

### Step 2: Align Units

Match original units to revised units:

```
Original Unit 1 → Revised Unit 1
Original Unit 2 → Revised Units 2-3 (split)
Original Unit 3 → Revised Unit 4
Original Unit 4 → [MISSING]
[NEW] → Revised Unit 5
```

### Step 3: Compare Aligned Units

For each pair:
1. Extract events
2. Compare agents and actions
3. Verify information preserved
4. Check emotional markers
5. Verify causal relationships

### Step 4: Flag Discrepancies

Generate flags for:
- Missing original units (unauthorized deletion)
- New units not derived from original (unauthorized addition)
- Altered meaning in matched units (unauthorized modification)

## Edge Cases

### Implicit vs Explicit

**Original (implicit):** "The door slammed. He was gone."
**Revised (explicit):** "He slammed the door and left."

**Assessment:** Acceptable—makes implicit explicit without changing meaning.

### Summary vs Expansion

**Original (summary):** "They argued about money."
**Revised (expansion):** "'You spent how much?' she demanded. He shrugged. 'It was necessary.'"

**Assessment:** Acceptable if:
- Core event (argument about money) preserved
- Character positions consistent with original context
- No new information introduced that contradicts established facts

**Flag if:** Expansion introduces new facts, motivations, or outcomes.

### Sensory Detail Addition

**Original:** "The room was dark."
**Revised:** "The room was dark, shadows pooling in corners, the only light a thin strip under the door."

**Assessment:** Acceptable—adds compatible sensory detail without changing meaning.

**Flag if:** Detail changes meaning ("The room was dark and cold" might alter emotional tone).

### Internal Monologue Enhancement

**Original:** "She wondered if he was lying."
**Revised:** "Was he lying? The question gnawed at her, finding no answer."

**Assessment:** Acceptable—same uncertainty, enhanced expression.

**Flag if:** Enhancement resolves uncertainty or adds new conclusions.

## Verification Checklist

For each compared unit:

- [ ] Same events occur
- [ ] Same agents perform actions
- [ ] Actions are semantically compatible
- [ ] Information is preserved (not contradicted)
- [ ] Emotional valence is consistent
- [ ] Causal relationships intact
- [ ] No unauthorized conclusions/realizations
- [ ] No unauthorized backstory
- [ ] No unauthorized characters
- [ ] Temporal relationships preserved

## Confidence Scoring

Rate comparison confidence:

| Score | Meaning |
|-------|---------|
| HIGH | Clear alignment, meaning clearly preserved |
| MEDIUM | Some interpretation required, likely preserved |
| LOW | Significant changes, needs review |
| FAIL | Meaning demonstrably altered |

Use confidence scores to prioritize review queue.
