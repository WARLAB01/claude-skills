# Verification Protocol

Methodology for verifying extracted facts against source manuscript to prevent hallucinations.

## Core Principle

**Every fact in the canon bible must trace to a specific quote in the manuscript.**

If a fact cannot be anchored to source text, it is either:
1. A hallucination (fabricated by the extraction process)
2. An inference (derived but not stated)
3. An ambiguity (multiple interpretations possible)

Only anchored facts belong in canon. Inferences and ambiguities require user decisions.

---

## Anchor Format

Every extracted fact must include:

```markdown
**Fact**: [statement]
**Anchor**: "[15-25 word quote from manuscript]"
**Location**: Unit_ID, paragraph X (or line X for poetry/dialogue)
```

### Good Anchors

- Direct quotes that contain the fact
- Minimal but sufficient context
- Exact text from manuscript (no paraphrasing)

### Bad Anchors

- Paraphrased content
- Quotes that imply but don't state the fact
- Overly long quotes (>30 words)
- Quotes from different locations stitched together

---

## Verification Categories

### VERIFIED

The anchor exists at the stated location AND directly supports the fact.

**Criteria:**
- Quote found verbatim in manuscript at stated location
- Quote clearly states or shows the claimed fact
- No interpretation required

**Example:**
```
Fact: Sarah has red hair
Anchor: "Sarah pushed her red hair back from her face"
Location: U003, para 7
Status: VERIFIED ✓
```

### ANCHOR_NOT_FOUND

The stated anchor does not exist at the claimed location.

**Possible causes:**
- Typo in anchor quote
- Wrong Unit_ID or paragraph number
- Anchor was hallucinated

**Resolution:**
1. Search manuscript for similar text
2. If found elsewhere, update location
3. If not found, flag for removal or user review

**Example:**
```
Fact: Marcus drives a blue truck
Anchor: "Marcus climbed into his blue pickup"
Location: U007, para 12
Search result: Quote not found in U007
Action: Search all units for "Marcus" + "truck" or "pickup"
```

### CLAIM_MISMATCH

The anchor exists but doesn't support the claimed fact.

**Possible causes:**
- Extraction error (misread the text)
- Over-interpretation
- Conflation of multiple facts

**Resolution:**
1. Re-read anchor in full context
2. Revise fact to match what anchor actually says
3. Or find correct anchor for original fact

**Example:**
```
Fact: Sarah is 32 years old
Anchor: "Sarah had been on the force for twelve years"
Location: U002, para 3
Issue: Anchor gives tenure, not age
Action: Either find age anchor or revise fact to "Sarah has 12 years on the force"
```

### AMBIGUOUS

The anchor supports multiple interpretations.

**Possible causes:**
- Deliberately ambiguous writing
- Context-dependent meaning
- Unreliable narrator

**Resolution:**
1. Note all possible interpretations
2. Flag for user decision
3. User chooses: pick interpretation, mark as ambiguous, or exclude

**Example:**
```
Fact: Marcus killed his brother
Anchor: "He'd done what needed to be done. His brother would never hurt anyone again."
Location: U015, para 22
Issue: Could mean murder, self-defense, or calling police
Interpretations:
  A) Marcus killed his brother (direct reading)
  B) Marcus stopped his brother by other means (indirect reading)
  C) Marcus arranged for someone else to handle it
USER DECISION REQUIRED
```

### INFERRED

The fact is not stated but can be logically derived.

**Policy:** Inferences do NOT belong in canon unless marked.

**Example:**
```
Fact: Sarah's apartment is on the third floor
Evidence: "Sarah climbed two flights of stairs to her door"
Issue: Inference (assumes ground floor = 1, each flight = 1 floor)
Action: Mark as [INFERRED] or exclude
```

---

## Verification Process

### Step 1: Batch Anchor Check

For each extraction chunk, verify all anchors exist:

```python
for fact in extracted_facts:
    quote = fact.anchor
    location = fact.location
    
    # Find quote in manuscript
    found = search_manuscript(quote, location)
    
    if not found:
        flag_as("ANCHOR_NOT_FOUND", fact)
    elif found.location != location:
        update_location(fact, found.location)
```

### Step 2: Claim Validation

For each verified anchor, confirm it supports the claim:

```
Read anchor in context (±2 paragraphs)
Ask: Does this anchor DIRECTLY state or show the fact?

If YES → VERIFIED
If NO but anchor implies fact → INFERRED (flag)
If NO and anchor says something different → CLAIM_MISMATCH (flag)
If anchor could mean multiple things → AMBIGUOUS (flag)
```

### Step 3: Cross-Reference Check

For facts that appear in multiple extractions:

```
Collect all anchors for same fact
Verify anchors are consistent
If contradictory anchors exist → flag as CONTRADICTION
```

### Step 4: Generate Verification Report

```markdown
## Verification Report

**Extraction batch:** [chunk ID]
**Total facts:** [count]

| Status | Count | % |
|--------|-------|---|
| VERIFIED | X | X% |
| ANCHOR_NOT_FOUND | X | X% |
| CLAIM_MISMATCH | X | X% |
| AMBIGUOUS | X | X% |
| INFERRED | X | X% |

### Items Requiring Review

[List all non-VERIFIED items with details]
```

---

## Edge Cases

### Dialogue Attribution

When fact comes from character dialogue:

```
Fact: The murder happened at midnight
Anchor: "It was midnight when I heard the shot," Sarah said.
Issue: Sarah CLAIMS this, but is she reliable?

Resolution:
- If narrator confirms: VERIFIED
- If only character claims: Mark as "[Character] states:" 
- If character known to lie: Mark as "[Character] claims (reliability: LOW):"
```

### Flashbacks and Memories

When fact comes from character memory:

```
Fact: Marcus grew up in Detroit
Anchor: "He remembered Detroit winters, the way the cold cut through everything."

Resolution:
- Mark as "Memory/flashback source"
- Note: Memory may be unreliable
- Cross-reference with other sources if available
```

### Descriptions vs. Reality

When physical descriptions may be subjective:

```
Fact: Sarah is beautiful
Anchor: "God, she was beautiful," Marcus thought.

Resolution:
- This is Marcus's perception, not objective fact
- Revise to: "Marcus finds Sarah beautiful"
- Or: "Sarah (described as beautiful by Marcus)"
```

### Time-Sensitive Facts

When facts change over the course of the manuscript:

```
Fact: Sarah works at the 14th Precinct
Anchor 1 (U003): "Sarah walked into the 14th Precinct"
Anchor 2 (U045): "Her new desk at the 23rd felt wrong"

Resolution:
- Create timeline-aware entry:
  "Sarah works at 14th Precinct (U001-U044)"
  "Sarah transfers to 23rd Precinct (U045+)"
```

---

## User Checkpoint Protocol

After verification, present flagged items:

```markdown
## Verification Complete

✓ Verified: [X] facts
⚠ Flagged: [Y] items requiring your review

### Flagged Items

**1. ANCHOR_NOT_FOUND**
> Fact: [fact]
> Claimed anchor: "[quote]"
> 
> Options:
> - [ ] Search for correct anchor
> - [ ] Remove from canon
> - [ ] Keep with [UNVERIFIED] marker

**2. AMBIGUOUS**
> Fact: [fact]
> Anchor: "[quote]"
> Interpretations:
>   A) [interpretation 1]
>   B) [interpretation 2]
> 
> Options:
> - [ ] Use interpretation A
> - [ ] Use interpretation B
> - [ ] Keep as ambiguous
> - [ ] Exclude from canon

[Continue for all flagged items]
```

---

## Quality Metrics

Track verification quality across the full canon:

| Metric | Target | Concern Threshold |
|--------|--------|-------------------|
| Verification rate | >95% | <90% |
| Anchor accuracy | >98% | <95% |
| User decisions required | <5% | >10% |
| Contradictions found | 0 | >2 |

If concern thresholds are exceeded, review extraction methodology.
