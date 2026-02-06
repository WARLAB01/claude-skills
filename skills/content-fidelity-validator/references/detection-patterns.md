# Detection Patterns

Patterns and heuristics for detecting content injection in manuscript revisions.

## Entity Detection

### Character Name Patterns

Extract potential character names using:

1. **Proper noun detection**: Capitalized words in dialogue attribution
   - `"..." said [Name]`
   - `[Name] said "..."`
   - `[Name] + action verb`

2. **Pronoun antecedent mapping**: Track who pronouns refer to
   - Build entity list from original
   - Verify all pronouns in revised map to original entities

3. **New name indicators**:
   - First mention patterns: "a man named [X]", "[X], who..."
   - Introduction patterns: "I'm [X]", "Call me [X]"

### Location Name Patterns

1. **Prepositional phrases**: "in [Location]", "at [Location]", "to [Location]"
2. **Setting descriptions**: "the [Location] was...", "[Location]'s streets..."
3. **Proper nouns with location suffixes**: Street, Avenue, Building, Park, etc.

### Object Name Patterns

1. **Article + proper noun**: "the [Object]", "a [Object] called..."
2. **Possession patterns**: "[Character]'s [object]"
3. **Significant objects**: Items given narrative weight

## Memory/Backstory Detection

### Temporal Markers

Phrases indicating past reference:

```
remembered, recalled, thought back to
flashback to, memory of, reminded of
back when, years ago, as a child
that time when, the day that, the night when
used to, had once, before [event]
childhood, youth, growing up
her mother had, his father used to
```

### Backstory Sentence Structures

1. **Past perfect + temporal**: "She had always known..."
2. **Childhood references**: "Growing up in [location]..."
3. **Relationship history**: "They had met when..."
4. **Formative events**: "Ever since [past event]..."

### Memory Injection Indicators

Compare original and revised for:
- New past-tense narrative not in original
- New proper nouns in memory context
- New emotional associations with past

## Reflection/Realization Detection

### Cognitive Verbs

```
High-confidence injection indicators:
- realized, suddenly realized, finally realized
- understood, now understood, came to understand
- recognized, dawned on, occurred to
- grasped, comprehended, saw clearly
- decided, concluded, determined
- knew now, was certain now
```

### Realization Sentence Structures

1. **Sudden insight**: "It hit him that...", "She suddenly knew..."
2. **Gradual understanding**: "He was beginning to see...", "It was becoming clear..."
3. **Certainty statements**: "He was sure now that...", "She knew without doubt..."

### Insight Injection Indicators

Flag when revised contains:
- Conclusions not supported by original text
- Character knowledge not established in original
- Interpretations that go beyond original's implications

## World Detail Detection

### World-Building Markers

```
Phrases introducing world facts:
- In this city/world/place...
- The way things worked here...
- Everyone knew that...
- It was common knowledge...
- The rules stated...
- According to [authority]...
```

### Setting Expansion Indicators

Compare for:
- New descriptions of how the world works
- New social rules or customs
- New historical facts
- New relationships between established elements

## Meaning Alteration Detection

### Emotional Valence Shifts

Track emotional markers:

```
Positive: smiled, laughed, warmth, comfort, relief, joy
Negative: frowned, tensed, cold, fear, anger, dread
Neutral: observed, noted, watched, waited
```

Compare emotional distribution in original vs revised.

### Relationship Dynamic Shifts

Monitor for changes in:
- Power balance between characters
- Affection/hostility indicators
- Trust/distrust markers
- Alliance/opposition signals

### Intention Alteration

Character intention markers:

```
wanted to, planned to, intended to
hoped, wished, desired
aimed to, meant to, sought to
```

Verify intentions in revised match original.

## Deletion Detection

### Beat Identification

Identify significant beats in original:

1. **Action beats**: Character does something
2. **Dialogue beats**: Character says something significant
3. **Reaction beats**: Character responds to stimulus
4. **Description beats**: Significant setting/atmosphere detail

### Deletion Check Process

For each beat in original:
1. Search for corresponding content in revised
2. If not found, check if deletion was authorized
3. Flag unauthorized deletions

### Acceptable Deletions

- Redundant descriptions (if authorized for tightening)
- Filler dialogue (if authorized for pacing)
- Transitional content (if authorized)

### Unacceptable Deletions

- Plot-relevant actions
- Character-defining moments
- Clue-bearing details
- Relationship-defining exchanges

## Pattern Matching Implementation

### Regex Patterns for Scanning

```python
# Memory indicators
MEMORY_PATTERNS = [
    r'\b(remembered|recalled|thought back)\b',
    r'\b(flashback|memory of|reminded of)\b',
    r'\b(as a child|years ago|back when)\b',
    r'\b(used to|had once|before the)\b',
]

# Realization indicators
REALIZATION_PATTERNS = [
    r'\b(realized|understood|recognized)\b',
    r'\b(dawned on|occurred to|hit (him|her))\b',
    r'\b(knew now|was certain|became clear)\b',
    r'\b(finally (saw|understood|grasped))\b',
]

# New entity indicators
NEW_ENTITY_PATTERNS = [
    r'(a|the) (man|woman|person) (named|called) [A-Z][a-z]+',
    r"(I'm|I am|call me) [A-Z][a-z]+",
    r'[A-Z][a-z]+ (entered|appeared|arrived)',
]
```

### Comparison Algorithm

```
FOR each sentence in revised:
    IF sentence matches MEMORY_PATTERNS:
        IF no corresponding memory in original:
            FLAG as Memory Injection

    IF sentence matches REALIZATION_PATTERNS:
        IF realization content not derivable from original:
            FLAG as Reflection Injection

    IF sentence contains NEW_ENTITY_PATTERNS:
        IF entity not in original entity list:
            FLAG as Entity Injection
```

## False Positive Handling

### Acceptable Additions

Some additions are acceptable under voice enhancement:

1. **Sensory detail expansion** (if authorized)
   - Original: "He walked in."
   - Revised: "He walked in, the floorboards creaking under his weight."
   - Assessment: Acceptable if sensory enhancement authorized

2. **Emotional beat expansion** (if authorized)
   - Original: "She felt afraid."
   - Revised: "Fear coiled in her gut, cold and familiar."
   - Assessment: Acceptable if voice enhancement authorized

3. **Dialogue rhythm adjustment** (if authorized)
   - Original: "Yes, I'll do it."
   - Revised: "Yeah. I'll do it."
   - Assessment: Acceptable if voice rewriting authorized

### Unacceptable Regardless of Authorization

These are NEVER acceptable without explicit approval:

1. New named characters
2. New plot events
3. New backstory facts
4. New world rules
5. Changed character motivations
6. Altered plot outcomes

## Severity Classification

### High Severity (Automatic Block)

- New characters
- New significant backstory
- Plot-altering realizations
- Relationship dynamic reversals
- Missing plot beats

### Medium Severity (Flag for Review)

- Minor reflections consistent with character
- Small sensory additions
- Subtle emotional adjustments
- Non-essential details

### Low Severity (Log but Allow)

- Punctuation-only changes
- Minor word choice variations
- Grammatical improvements
- Formatting standardization
