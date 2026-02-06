---
name: content-fidelity-validator
description: Validate that manuscript revisions contain only authorized changes with zero content injection. Use as a validation layer within any revision workflow to detect unauthorized additions (new characters, memories, backstory, reflections, world details, plot elements). Designed for batch processing with deferred review. Outputs inline annotations plus separate review file for flagged chunks. Triggers include integration calls from manuscript-revision-orchestrator, character-voice-architect, or any skill performing text rewrites. Can also be invoked standalone with "validate these changes", "check for content injection", "fidelity check this revision".
---

# Content Fidelity Validator

Systematic validation layer to ensure manuscript revisions contain only authorized changes. Catches content injection that LLMs commonly introduce: new memories, reflections, backstory, characters, world details, and meaning alterations.

## Core Principle

**Every element in the revised text must either:**
1. Exist in the original text, OR
2. Be explicitly authorized by the change instructions

Anything else is **unauthorized injection** and must be blocked.

## Integration Pattern

This skill is designed to be invoked by other revision skills:

```
[Revision Skill] MODE C (Editing)
    ↓
    Chunk revised
    ↓
Content Fidelity Validator
    ↓
[PASS] → Continue to next chunk
[FAIL] → Block chunk, log to review file, continue processing
```

**Key feature:** Failures do NOT halt processing. Flagged chunks are logged for batch review while remaining chunks continue processing.

## Validation Categories

### Category 1: Entity Injection
Detect new named entities not present in original:
- New character names
- New location names
- New organization names
- New object names (artifacts, vehicles, etc.)

**Exception:** Pronouns referring to existing entities are allowed.

### Category 2: Memory/Backstory Injection
Detect references to past events not established in original:
- "He remembered when..."
- "She thought back to..."
- References to childhood, past relationships, prior events
- Flashback content not in original

### Category 3: Reflection/Realization Injection
Detect new internal conclusions or insights:
- "He realized that..."
- "She understood now..."
- "It occurred to him..."
- New interpretations of existing facts

### Category 4: World Detail Injection
Detect new world-building elements:
- New rules, laws, customs
- New historical facts
- New setting details beyond what's described
- New relationships between existing entities

### Category 5: Meaning Alteration
Detect changes that preserve words but alter meaning:
- Changed emotional tone (anger → sadness)
- Changed relationship dynamics
- Changed character motivations
- Changed plot implications

### Category 6: Unauthorized Removal
Detect deletions not authorized by change instructions:
- Missing plot beats
- Removed character actions
- Deleted dialogue
- Cut descriptions

## Input Requirements

The validator requires three inputs:

1. **Original text** — The unmodified source chunk
2. **Revised text** — The modified chunk
3. **Authorized changes** — List of what changes are permitted

### Authorized Changes Format

```markdown
## Authorized Changes for [Unit_ID]

### Explicit Operations
- REPLACE: "old text" → "new text"
- ADD after "anchor": "new content"
- REMOVE: "text to delete"

### Scope Permissions
- Voice enhancement: YES/NO
- Style modification: YES/NO
- Dialogue rewriting: YES/NO (preserve meaning)
- Internal monologue enhancement: YES/NO (preserve meaning)

### Constraints
- New characters: NOT PERMITTED
- New backstory: NOT PERMITTED
- New memories: NOT PERMITTED
- New realizations: NOT PERMITTED unless derived from on-page facts
```

## Validation Process

### Step 1: Entity Extraction

Extract all named entities from both texts:

```
Original entities: [Character A, Location X, Object Y, ...]
Revised entities: [Character A, Character B, Location X, Object Y, Object Z, ...]
```

**Flag:** Any entity in revised but not in original (unless authorized).

### Step 2: Temporal Reference Scan

Identify all references to past events:

```
Original temporal refs: ["that night at the bar", "their first case together"]
Revised temporal refs: ["that night at the bar", "their first case together", "his childhood in Detroit"]
```

**Flag:** Any new temporal reference (unless authorized).

### Step 3: Cognitive Verb Scan

Identify all realization/reflection constructs:

```
Cognitive verbs to scan:
- realized, understood, recognized, grasped, comprehended
- remembered, recalled, thought back, flashed back
- decided, concluded, determined, resolved
- noticed (new observations not in original)
- felt (new emotions not in original)
```

**Flag:** New cognitive constructs not present in original (unless authorized).

### Step 4: Semantic Comparison

Compare meaning preservation:

For each sentence in revised text:
1. Find corresponding content in original
2. Verify core meaning is preserved
3. Flag alterations that change:
   - Who did what to whom
   - Emotional valence
   - Causal relationships
   - Character intentions

### Step 5: Deletion Check

Verify all original content is accounted for:

For each significant element in original:
1. Locate in revised OR
2. Confirm deletion was authorized

**Flag:** Unauthorized deletions.

## Output Format

### PASS Result

```markdown
## Fidelity Validation: PASS

**Unit_ID:** [ID]
**Validation timestamp:** [datetime]

### Validation Summary
- Entities: ✓ No unauthorized additions
- Temporal refs: ✓ No unauthorized additions
- Cognitive constructs: ✓ No unauthorized additions
- Semantic preservation: ✓ Meaning preserved
- Content completeness: ✓ No unauthorized deletions

**Result:** FIDELITY_PASS — Chunk approved for output.
```

### FAIL Result

```markdown
## Fidelity Validation: FAIL

**Unit_ID:** [ID]
**Validation timestamp:** [datetime]
**Status:** BLOCKED — Flagged for review

### Detected Injections

#### Injection 1: [Category]
**Type:** [Entity/Memory/Reflection/World Detail/Meaning Alteration/Deletion]
**Location:** "[10-20 word quote from revised text]"
**Issue:** [Specific description of what was injected]
**Original:** "[Corresponding original text, or 'NOT PRESENT']"
**Severity:** High | Medium

#### Injection 2: [Category]
[...]

### Validation Summary
- Entities: [✓ or ✗ count]
- Temporal refs: [✓ or ✗ count]
- Cognitive constructs: [✓ or ✗ count]
- Semantic preservation: [✓ or ✗ count]
- Content completeness: [✓ or ✗ count]

**Result:** FIDELITY_FAIL — [X] injection(s) detected. See review file.
```

## Review File Format

All failed chunks are logged to a cumulative review file:

```markdown
# Fidelity Review Queue

Generated: [datetime]
Total chunks processed: [X]
Passed: [Y]
Failed (pending review): [Z]

---

## Chunk: [Unit_ID] — FAILED

### Original Text
```
[Full original chunk]
```

### Proposed Revision
```
[Full revised chunk with INJECTION markers]
```

### Detected Injections

1. **[Category]** at "[location quote]"
   - Issue: [description]
   - Recommendation: [Remove entirely | Revise to: "suggested fix"]

2. **[Category]** at "[location quote]"
   - Issue: [description]
   - Recommendation: [Remove entirely | Revise to: "suggested fix"]

### User Decision Required
- [ ] Approve chunk as-is (accept injections)
- [ ] Reject and reprocess without injections
- [ ] Manually edit and resubmit

---

## Chunk: [Unit_ID] — FAILED
[...]
```

## Inline Annotation Format

When outputting revised text with inline markers:

```markdown
The detective walked into the bar. ««INJECTION:MEMORY He remembered his
father bringing him here as a child, the smell of stale beer and broken
dreams.»» "Looking for someone?" the bartender asked.
```

Markers use `««INJECTION:[TYPE] ... »»` for easy grep/search.

## Batch Processing Mode

For unattended batch processing:

1. **Process all chunks** regardless of pass/fail
2. **Log failures** to review file
3. **Mark failed chunks** in output with inline annotations
4. **Continue to next chunk** immediately after validation
5. **Generate summary** at end of batch

### Batch Summary Format

```markdown
# Fidelity Validation Batch Summary

**Session:** [datetime]
**Manuscript:** [name]
**Chunks processed:** [total]

## Results
- PASS: [count] ([%])
- FAIL: [count] ([%])

## Injection Breakdown
| Type | Count | Severity Distribution |
|------|-------|----------------------|
| Entity | [X] | [High: Y, Medium: Z] |
| Memory/Backstory | [X] | [High: Y, Medium: Z] |
| Reflection | [X] | [High: Y, Medium: Z] |
| World Detail | [X] | [High: Y, Medium: Z] |
| Meaning Alteration | [X] | [High: Y, Medium: Z] |
| Unauthorized Deletion | [X] | [High: Y, Medium: Z] |

## Most Common Patterns
1. [Pattern description] — [count] occurrences
2. [Pattern description] — [count] occurrences

## Review Required
See `fidelity-review-queue.md` for [X] chunks requiring manual review.
```

## Severity Definitions

| Severity | Criteria | Action |
|----------|----------|--------|
| **High** | New characters, significant backstory, plot-altering changes | Must be removed or explicitly approved |
| **Medium** | Minor reflections, small world details, subtle meaning shifts | Flag for review, may be acceptable |

## Integration with Other Skills

### manuscript-revision-orchestrator

Insert between MODE C and MODE D:

```
MODE C: Editing
    ↓
    [Chunk edited]
    ↓
Content Fidelity Validator
    ↓
[PASS] → MODE D: Validation
[FAIL] → Log to review, continue to next chunk
```

Add to MODE D validation output:
```
QA Result: PASS | FAIL
Fidelity Result: PASS | FAIL (see review file)
```

### character-voice-architect

Call after each voice rewrite:

```
Voice Alchemist rewrites chunk
    ↓
Content Fidelity Validator
    ↓
[PASS] → Accept rewrite
[FAIL] → Block, request rewrite without injections
```

### noir-mystery-qa

Can invoke for post-edit validation:

```
Fix applied
    ↓
Content Fidelity Validator
    ↓
Confirm fix didn't introduce new elements
```

## Standalone Usage

When invoked directly:

> Provide:
> 1. Original text (paste or file path)
> 2. Revised text (paste or file path)
> 3. What changes were authorized?
>
> I'll validate that only authorized changes were made.

## Working Directory

```
/home/claude/fidelity-working/
├── config/
│   └── session-config.md       # Authorized changes, constraints
├── chunks/
│   ├── [unit-id]-original.md
│   ├── [unit-id]-revised.md
│   └── [unit-id]-result.md
├── review/
│   └── fidelity-review-queue.md
└── output/
    └── batch-summary.md
```

## Reference Files

- `references/detection-patterns.md` — Regex and heuristics for each injection category
- `references/semantic-comparison.md` — Methodology for meaning preservation checks
