# Mystery Detection

Genre markers and heuristics for detecting mystery/thriller content and enabling mystery-specific artifacts.

## Detection Threshold

**Enable mystery mode when:** 2+ high-confidence markers OR 4+ medium-confidence markers are detected.

---

## High-Confidence Markers

Any TWO of these trigger mystery mode:

### Investigation Vocabulary

Scan for clusters of these terms (3+ in close proximity):

```
investigate, investigation, detective, clue, evidence
suspect, alibi, witness, interrogate, question (verb)
murder, homicide, crime scene, victim, perpetrator
case, solve, deduce, motive, opportunity, means
forensic, autopsy, coroner, medical examiner
```

### Central Crime

Story revolves around a crime to be solved:

- Murder or death under suspicious circumstances
- Theft of significant item
- Disappearance of person
- Fraud, blackmail, or conspiracy
- Any crime where "who did it" or "how" drives the plot

**Detection:** Crime mentioned in first 20% of manuscript AND referenced in final 20%.

### Hidden Information Structure

Key information is deliberately concealed from reader/characters:

- Secrets that drive character behavior
- Information revealed in stages
- "Reveal" scenes where truth emerges
- Characters who know things other characters don't

**Detection patterns:**
```
"didn't know that..."
"had no idea..."
"the truth was..."
"what [character] didn't realize..."
"finally understood..."
"the secret..."
"couldn't tell anyone..."
```

### Multiple Suspects

Three or more characters could plausibly be responsible:

- Multiple characters with motive
- Multiple characters with opportunity
- Alibi discussions
- Suspicion shifting between characters

**Detection:** 3+ characters discussed in context of suspicion/guilt/alibis.

### Revelation Scene Structure

Scenes structured around information reveals:

- Climactic explanation of "what really happened"
- Confession scenes
- Evidence confrontation scenes
- "Gather all suspects" scenes

---

## Medium-Confidence Markers

Four or more of these also trigger mystery mode:

### Procedural Elements

- Police procedure descriptions
- Courtroom scenes
- Legal terminology
- Evidence handling
- Interview/interrogation scenes

### Noir Atmosphere

- First-person cynical narrator
- Urban setting with moral ambiguity
- Femme fatale or homme fatal characters
- References to classic noir (Chandler, Hammett, etc.)
- Rain, shadows, smoke imagery clusters

### Thriller Pacing

- Short chapters
- Cliffhanger chapter endings
- Multiple POV with information asymmetry
- Ticking clock elements
- Chase or escape sequences

### Psychological Suspense

- Unreliable narrator signals
- Gaslighting dynamics
- Memory gaps or trauma
- "Is this real?" questioning
- Paranoia or surveillance themes

### Amateur Sleuth Patterns

- Civilian investigating crime
- "Stumbles into" mystery
- Using non-professional methods
- Personal stakes in solving mystery
- Conflict with official investigators

---

## Genre Subtype Detection

Once mystery mode is enabled, detect subtype for artifact customization:

### Classic Whodunit

**Markers:**
- Fair-play clue distribution
- Multiple viable suspects throughout
- Logical solution derivable from clues
- Detective figure (professional or amateur)

**Additional artifacts:** Clue registry with "available to reader" timestamps

### Police Procedural

**Markers:**
- Law enforcement protagonist
- Procedure-heavy investigation
- Forensic evidence focus
- Team dynamics

**Additional artifacts:** Evidence chain of custody, procedure compliance notes

### Noir/Hardboiled

**Markers:**
- Morally ambiguous protagonist
- Corruption themes
- Violence as problem-solving
- Cynical worldview in narration

**Additional artifacts:** Moral compromise tracker, double-cross registry

### Psychological Thriller

**Markers:**
- Internal conflict focus
- Unreliable perspective
- Gaslighting or manipulation
- Reality questioning

**Additional artifacts:** Narrator reliability tracker, perception vs. reality log

### Cozy Mystery

**Markers:**
- Amateur sleuth
- Small community setting
- Limited violence (often off-page)
- Hobby or profession hook (baking, knitting, bookstore, etc.)

**Additional artifacts:** Community relationship map, recurring character registry

---

## Detection Algorithm

```python
def detect_mystery_mode(manuscript):
    high_markers = 0
    medium_markers = 0
    
    # High-confidence checks
    if has_investigation_vocabulary_cluster(manuscript):
        high_markers += 1
    if has_central_crime(manuscript):
        high_markers += 1
    if has_hidden_information_structure(manuscript):
        high_markers += 1
    if has_multiple_suspects(manuscript):
        high_markers += 1
    if has_revelation_scenes(manuscript):
        high_markers += 1
    
    # Medium-confidence checks
    if has_procedural_elements(manuscript):
        medium_markers += 1
    if has_noir_atmosphere(manuscript):
        medium_markers += 1
    if has_thriller_pacing(manuscript):
        medium_markers += 1
    if has_psychological_suspense(manuscript):
        medium_markers += 1
    if has_amateur_sleuth_patterns(manuscript):
        medium_markers += 1
    
    # Decision
    if high_markers >= 2:
        confidence = "HIGH"
        enable = True
    elif medium_markers >= 4:
        confidence = "MEDIUM"
        enable = True
    elif high_markers == 1 and medium_markers >= 2:
        confidence = "MEDIUM"
        enable = True
    else:
        confidence = "LOW"
        enable = False
    
    return {
        "enable_mystery_mode": enable,
        "confidence": confidence,
        "high_markers": high_markers,
        "medium_markers": medium_markers,
        "subtype": detect_subtype(manuscript) if enable else None
    }
```

---

## Output Format

```markdown
## Genre Detection Results

### Mystery/Thriller Markers Found

**High-confidence markers:** [X]/5
- [x] Investigation vocabulary cluster
- [ ] Central crime
- [x] Hidden information structure
- [ ] Multiple suspects
- [x] Revelation scenes

**Medium-confidence markers:** [X]/5
- [x] Procedural elements
- [x] Noir atmosphere
- [ ] Thriller pacing
- [ ] Psychological suspense
- [ ] Amateur sleuth patterns

### Decision

**Mystery mode:** ENABLED | DISABLED
**Confidence:** HIGH | MEDIUM | LOW
**Detected subtype:** [subtype or "General mystery"]

### User Confirmation

[If MEDIUM confidence:]
> I've detected mystery/thriller elements with medium confidence.
> Should I enable mystery-specific artifacts?
> - Mystery Registry
> - Truth/Deception/Misunderstanding List  
> - Character Awareness Timeline
>
> [ ] Yes, enable mystery mode
> [ ] No, treat as general fiction
```

---

## False Positive Handling

Some genres share mystery markers but aren't mysteries:

### Literary Fiction with Secrets

- Has hidden information but no investigation
- **Distinguisher:** No detective figure, no "solving" arc

### Thriller without Mystery

- Has suspense but answer is known
- **Distinguisher:** Reader knows the threat, tension is survival not discovery

### Romance with Suspense Subplot

- Has mystery elements but romance is primary
- **Distinguisher:** Mystery resolves to enable romantic resolution

**Protocol:** When markers are ambiguous, ask user:

> This manuscript has some mystery elements but may not be primarily a mystery.
> The main plot appears to be [detected primary genre].
> 
> Would you like mystery artifacts generated?
> - [ ] Yes, generate full mystery artifacts
> - [ ] Yes, but as supplementary (not primary structure)
> - [ ] No, skip mystery artifacts

---

## Vocabulary Reference

### Investigation Terms
```
investigate, probe, examine, scrutinize, look into
detective, investigator, sleuth, PI, private eye
clue, lead, tip, evidence, proof, indication
suspect, person of interest, perpetrator, culprit
alibi, whereabouts, timeline, opportunity
motive, reason, cause, incentive
witness, testimony, statement, account
interrogate, question, interview, grill
```

### Crime Terms
```
murder, homicide, manslaughter, killing
theft, robbery, burglary, heist
fraud, embezzlement, forgery, con
kidnapping, abduction, disappearance
blackmail, extortion, coercion
assault, battery, attack
arson, sabotage, vandalism
conspiracy, cover-up, obstruction
```

### Revelation Terms
```
reveal, disclose, uncover, expose, unmask
discover, realize, learn, find out
confess, admit, come clean, own up
the truth, the real story, what really happened
secret, hidden, concealed, buried
finally understood, now knew, dawned on
```
