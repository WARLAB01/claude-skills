# Voice Extraction Patterns

Patterns and methods for extracting character voice data from manuscript text during canon creation.

## Purpose

Voice extraction creates draft V2 voice profiles that can be refined via character-voice-architect. The goal is to capture what's demonstrably present in the text, not to invent voice characteristics.

---

## Extraction Threshold

**Minimum data for voice profile:**
- 3+ dialogue instances for speech patterns
- 2+ scenes as POV for internal voice
- Total word count of character content: 500+ words

Characters below threshold get a "LOW CONFIDENCE" flag and abbreviated profile.

---

## Dialogue Extraction

### Step 1: Collect All Dialogue

For each character, collect every line of attributed dialogue:

```markdown
### Dialogue Corpus: [Character Name]

**Total instances:** [count]
**Scenes with dialogue:** [Unit_IDs]

**Dialogue Collection:**

1. "[Dialogue line 1]"
   - Context: [brief situation]
   - Unit_ID: [location]
   - Emotional state: [if apparent]

2. "[Dialogue line 2]"
   - Context: [brief situation]
   - Unit_ID: [location]
   - Emotional state: [if apparent]

[Continue for all instances]
```

### Step 2: Attribution Verification

Ensure dialogue is correctly attributed:

**Clear attribution:**
```
"I don't know," Sarah said.
Sarah shook her head. "I don't know."
```

**Contextual attribution:**
```
[Previous line from Marcus]
"I don't know." [Sarah based on context]
```

**Ambiguous (flag):**
```
"I don't know." [Could be either speaker - FLAG]
```

---

## Quantitative Analysis

### Sentence Length

Calculate for all dialogue:

```python
sentences = split_into_sentences(dialogue_corpus)
lengths = [word_count(s) for s in sentences]

metrics = {
    "average_length": mean(lengths),
    "median_length": median(lengths),
    "shortest": min(lengths),
    "longest": max(lengths),
    "std_dev": std(lengths)
}
```

**Classification:**
- Short: average < 8 words
- Medium: average 8-15 words
- Long: average > 15 words
- Variable: high std_dev relative to mean

### Vocabulary Complexity

```python
words = tokenize(dialogue_corpus)
unique_words = set(words)

metrics = {
    "total_words": len(words),
    "unique_words": len(unique_words),
    "lexical_diversity": len(unique_words) / len(words),
    "avg_word_length": mean([len(w) for w in words])
}
```

**Classification:**
- Simple: lexical diversity < 0.4, short avg word length
- Moderate: lexical diversity 0.4-0.6
- Complex: lexical diversity > 0.6, longer avg word length

### Question Frequency

```python
sentences = split_into_sentences(dialogue_corpus)
questions = [s for s in sentences if s.strip().endswith('?')]

metrics = {
    "total_questions": len(questions),
    "question_ratio": len(questions) / len(sentences)
}
```

**Classification:**
- Interrogative: ratio > 0.3
- Balanced: ratio 0.1-0.3
- Declarative: ratio < 0.1

### Contraction Usage

```python
contractions = ["don't", "won't", "can't", "shouldn't", "wouldn't", 
                "I'm", "you're", "he's", "she's", "it's", "we're", "they're",
                "I've", "you've", "we've", "they've", "I'll", "you'll",
                "isn't", "aren't", "wasn't", "weren't", "hasn't", "haven't"]

contraction_count = count_occurrences(dialogue_corpus, contractions)
expansion_opportunities = count_expansion_opportunities(dialogue_corpus)

metrics = {
    "contraction_count": contraction_count,
    "contraction_ratio": contraction_count / expansion_opportunities
}
```

**Classification:**
- Always: ratio > 0.8
- Usually: ratio 0.5-0.8
- Sometimes: ratio 0.2-0.5
- Rarely: ratio < 0.2

---

## Qualitative Analysis

### Verbal Tic Detection

**Method 1: Phrase frequency**

```python
# Extract 2-4 word phrases
phrases = extract_ngrams(dialogue_corpus, [2, 3, 4])
phrase_counts = Counter(phrases)

# Filter for repeated phrases (3+ occurrences)
verbal_tics = {p: c for p, c in phrase_counts.items() if c >= 3}
```

**Method 2: Pattern matching**

Common tic patterns:
```
"you know"          - filler
"I mean"            - hedging  
"like"              - filler (when not comparative)
"basically"         - summarizing
"honestly"          - emphasis
"look"              - attention-getting
"listen"            - attention-getting
"the thing is"      - qualification
"to be honest"      - emphasis/deflection
"at the end of the day" - summarizing
```

**Method 3: Character-specific phrases**

Look for unique phrases used only by this character:
```python
all_character_phrases = {char: extract_phrases(corpus) for char, corpus in characters}

for char, phrases in all_character_phrases.items():
    other_phrases = union(all_character_phrases.values()) - phrases
    unique_phrases = phrases - other_phrases
    # These are character-specific candidates
```

### Profanity Analysis

**Detection:**
```python
profanity_lists = {
    "mild": ["damn", "hell", "crap", "ass"],
    "moderate": ["shit", "bastard", "bitch", "piss"],
    "heavy": ["fuck", "fucking", "motherfucker", ...]
}

detected = categorize_profanity(dialogue_corpus, profanity_lists)
```

**Context analysis:**

For each profanity instance, note:
- Emotional state when used
- Who they're speaking to
- Situation intensity

This reveals triggers:
```markdown
**Profanity Pattern:**
- Level: Moderate
- Words used: "shit", "bastard"
- Triggers: 
  - Under physical threat
  - When lied to
  - Never around children
```

### Response Pattern Detection

Analyze dialogue in context (with preceding line):

**Direct responders:**
```
"Where were you last night?"
"At home. Alone."
```

**Indirect responders:**
```
"Where were you last night?"
"Why does it matter?"
```

**Deflectors:**
```
"Where were you last night?"
"You know, I've been meaning to ask you something."
```

**Over-explainers:**
```
"Where were you last night?"
"I was at home, like I usually am on Tuesdays. I made dinner around seven, 
watched some TV, went to bed early because I had that meeting this morning."
```

---

## Internal Voice Extraction (POV Characters)

### Collect Internal Monologue

Extract all non-dialogue narrative from POV scenes:

```markdown
### Internal Voice Corpus: [Character Name]

**POV scenes:** [Unit_IDs]
**Total internal content:** [word count]

**Thought samples:**

1. [Extended thought passage]
   - Context: [what prompted this]
   - Unit_ID: [location]
   - Emotional state: [if apparent]

[Continue for significant passages]
```

### Thought Style Analysis

**Structure patterns:**

- Analytical: Logical progression, cause-effect reasoning
- Emotional: Feeling-focused, sensation-heavy
- Fragmented: Incomplete thoughts, interruptions
- Flowing: Long, connected passages
- Mixed: Varies by situation

**Self-reference patterns:**

- First person consistent: "I thought...", "I noticed..."
- Second person (self-talk): "You idiot...", "You should have..."
- Third person (dissociation): "[Name] was such a fool..."
- Name-free: Observations without self-reference

### Observation Priority Detection

In scene openings and transitions, what does this POV notice first?

```markdown
**Scene Entry Pattern Analysis:**

Scene [Unit_ID]:
- First noticed: [what they observe first]
- Category: [people/threats/environment/objects/emotions]

Scene [Unit_ID]:
- First noticed: [what they observe first]  
- Category: [people/threats/environment/objects/emotions]

**Pattern:** [Character] typically notices [category] first.
```

### Self-Perception Indicators

Look for:
- How they describe their own actions
- Self-critical or self-forgiving tendencies
- Comparison to others
- Blind spots (what they don't notice about themselves)

---

## Output Format

### Draft Voice Profile

```markdown
# Draft Voice Profile: [CHARACTER NAME]

**Status:** DRAFT — Requires refinement via character-voice-architect
**Confidence:** HIGH | MEDIUM | LOW
**Data basis:** [X] dialogue instances, [Y] POV scenes

---

## Extracted Speech Patterns

### Quantitative Findings

| Metric | Value | Classification |
|--------|-------|----------------|
| Avg sentence length | [X] words | [Short/Medium/Long] |
| Vocabulary complexity | [X] | [Simple/Moderate/Complex] |
| Question frequency | [X]% | [Interrogative/Balanced/Declarative] |
| Contraction usage | [X]% | [Always/Usually/Sometimes/Rarely] |

### Detected Verbal Markers

**Verbal tics found:**
- "[tic 1]" — [X] occurrences — Example: "[quote]" ([Unit_ID])
- "[tic 2]" — [X] occurrences — Example: "[quote]" ([Unit_ID])

**Profanity:**
- Level: [none/mild/moderate/heavy]
- Words used: [list]
- Apparent triggers: [situations]

**Response tendency:** [Direct/Indirect/Deflecting/Over-explaining]

---

## Extracted Internal Voice (if POV)

### Thought Style

- Structure: [Analytical/Emotional/Fragmented/Flowing/Mixed]
- Self-reference: [1st person/2nd person/3rd person/mixed]
- Articulation vs speech: [More/Less/Same]

### Observation Priority

1. [First priority] — [evidence]
2. [Second priority] — [evidence]
3. [Third priority] — [evidence]

### Self-Perception

- Self-image: [how they see themselves]
- Critical tendency: [harsh/moderate/gentle]
- Blind spots: [what they miss]

---

## Sample Dialogue Cluster

> "[Quote 1]" — [Unit_ID]
> "[Quote 2]" — [Unit_ID]
> "[Quote 3]" — [Unit_ID]
> "[Quote 4]" — [Unit_ID]
> "[Quote 5]" — [Unit_ID]

---

## Sample Internal Monologue (if POV)

> [Extended passage showing internal voice]
> — [Unit_ID]

---

## Suggested Archetype Alignment

Based on detected patterns, this character may align with:

**Primary:** [Archetype] — because [reasoning]
**Secondary:** [Archetype] — because [reasoning]

*Note: Archetype selection should be confirmed via character-voice-architect Mode A*

---

## Refinement Recommendations

To complete this profile, address:

1. [ ] Confirm archetype alignment
2. [ ] Set pulp level (1-5)
3. [ ] Verify verbal tics are intentional
4. [ ] Add emotional expression patterns
5. [ ] Define response patterns under pressure
```

---

## Low-Confidence Handling

When data is insufficient:

```markdown
# Draft Voice Profile: [CHARACTER NAME]

**Status:** DRAFT — LOW CONFIDENCE
**Warning:** Insufficient data for reliable extraction

**Data available:**
- Dialogue instances: [X] (minimum 3 required)
- POV scenes: [X] (minimum 2 required for internal voice)

**Partial findings:**
[Whatever can be extracted]

**Recommendation:** 
- Use archetype defaults from character-voice-architect
- Or: Gather more manuscript data before profiling
- Or: Create profile based on author intent rather than extraction
```

---

## Quality Checklist

Before finalizing extraction:

- [ ] All dialogue correctly attributed
- [ ] Quantitative metrics calculated
- [ ] Verbal tics verified (not just common phrases)
- [ ] Profanity context analyzed
- [ ] Sample dialogue representative
- [ ] Internal voice captured (if POV)
- [ ] Observation priorities identified (if POV)
- [ ] Archetype suggestions reasoned
- [ ] Confidence level appropriate
- [ ] Refinement recommendations specific
