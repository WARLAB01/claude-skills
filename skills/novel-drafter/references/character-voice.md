# Character Voice Profiles (V2)

This reference covers the V2 voice profile format used across novel-drafter, character-voice-architect, and canon-creator.

## Full Specification

For complete V2 format specification, see character-voice-architect's `references/voice-profile-v2-spec.md`.

## Quick Reference for Drafting

When drafting, the most critical profile elements are:

1. **Speech Patterns:** How do they talk?
2. **Internal Voice (POV):** How do they think?
3. **Pulp Level:** How stylized is their voice?
4. **Verbal Markers:** What makes them distinctive?

## Identifying Major Characters

Before asking about voices, identify who needs a full profile:

**Tier 1: POV Characters (always need full profile)**
- Anyone whose head we're in for a scene
- Their internal monologue must be distinctive

**Tier 2: Frequent Dialogue Characters (need dialogue profile)**
- Appear in 3+ scenes with speaking parts
- Interact with multiple POV characters

**Tier 3: Minor Characters (basic notes only)**
- Appear briefly
- Note any distinctive speech quirk, but no full profile needed

## Voice Profile Sources

V2 voice profiles can come from:

1. **canon-creator** — Draft profiles extracted from existing manuscript
2. **character-voice-architect Mode A** — Full interactive profile building
3. **Manual creation** — Simplified profile created during novel-drafter setup

For existing manuscripts, always prefer profiles from canon-creator or character-voice-architect, as they're based on actual text analysis.

## Simplified Profile for New Characters

When creating profiles during drafting (not analyzing existing text):

```markdown
# Voice Profile: [CHARACTER NAME]
Version: 2.0 (Draft)

## Quick Reference
| Field | Value |
|-------|-------|
| Role | [POV / Supporting] |
| Archetype | [from menu or custom] |
| Pulp Level | [1-5] |
| Profanity | [level] |

## Speech Patterns
- Sentence length: [short/medium/long]
- Vocabulary: [register]
- Verbal tics: ["phrases"]

## Internal Voice (POV only)
- Thought style: [analytical/emotional/etc.]
- What they notice: [priorities]
- Self-deprecating humor: [yes/no/level]

## Pulp at This Level
[Example of how their voice sounds]
```

## Voice Discovery Questions

For characters without existing profiles:

### Speech Patterns
> "How does [Character] speak? Consider:"
> - Vocabulary level (educated/simple/technical/slang)
> - Sentence structure (formal/casual/clipped/rambling)
> - Regional dialect or accent markers
> - Verbal tics or pet phrases
> - Profanity usage

### For POV Characters Only: Internal Voice
> "How does [Character] think internally?"
> - More articulate or less than their speech?
> - Prone to tangents or focused?
> - Self-critical or self-assured?
> - Observational style (what do they notice first?)

### Emotional Expression
> "How does [Character] express emotion?"
> - Openly or suppressed?
> - Physical tells (fidgeting, tension, etc.)
> - Deflection through humor/anger/silence?

### Character-Specific Vocabulary
> "Any words, phrases, or references unique to [Character]?"
> - Professional jargon from their job
> - Cultural references from their background
> - Repeated metaphors or frames of reference

## Archetype Selection

For new characters, present archetype options based on declared genres. See character-voice-architect's `references/voice-archetypes.md` for full library.

**Common Noir/Mystery Archetypes:**
- Hardboiled Detective
- World-Weary Cop
- Femme Fatale
- Smooth Criminal
- Working Class Hero
- Nervous Witness
- Wounded Romantic
- Hidden Poet
- Cynical Reporter

Users can:
- Select a primary archetype
- Add secondary influence
- Pick specific traits from archetype menus
- Blend multiple archetypes

## Applying Voice During Drafting

### Before Each Scene

1. Check: Who is the POV character?
2. Load their voice profile
3. Note which other major characters appear
4. Load their dialogue profiles

### During Drafting

**Internal Monologue**
- Use POV character's thought style
- Apply their observational preferences (what do they notice?)
- Vocabulary should match their internal voice level
- If they have verbal tics, some may appear in thoughts too
- Apply appropriate pulp level

**Dialogue**
- Each character speaks in their own voice, not the POV character's
- When POV character speaks, match their speech patterns
- Filter how POV perceives others' speech (they might note an accent, a word choice)
- Respect each character's profanity settings

### Voice Consistency Checklist

Before finalizing a scene, verify:

- [ ] POV character's internal voice matches their profile
- [ ] POV character's dialogue matches their speech patterns
- [ ] Other characters' dialogue matches their profiles
- [ ] No voice bleed (characters sounding like each other)
- [ ] Emotional state reflected appropriately
- [ ] Pulp level consistent with profile setting
- [ ] Verbal tics appearing at appropriate frequency

## Common Voice Mistakes

### Voice Bleed
**Problem**: All characters start sounding alike, usually like the author.
**Fix**: Before each dialogue line, check: Would THIS character use THESE words?

### POV Contamination
**Problem**: POV character thinks in a voice that's not theirs.
**Fix**: Review voice profile before each scene. Read internal monologue aloud — does it sound like them?

### Inconsistent Vocabulary
**Problem**: Character uses words outside their established vocabulary range.
**Fix**: Keep a "vocabulary range" note. A blue-collar character shouldn't suddenly use "perspicacious."

### Lost Verbal Tics
**Problem**: Character's pet phrases disappear partway through draft.
**Fix**: At chapter checkpoints, verify tics still appearing (not in every line, but periodically).

### Emotional Voice Mismatch
**Problem**: Character is described as stressed but their internal voice is calm.
**Fix**: Stress should affect voice — shorter thoughts, more fragments, different focus.

### Pulp Level Drift
**Problem**: Character's voice becomes more/less stylized than their profile specifies.
**Fix**: Reference pulp-calibration.md examples. At checkpoints, compare to profile's set level.

## Voice Contrast Matrix

For stories with multiple POV characters, create a quick contrast matrix:

| Element | Noah | April | Beth |
|---------|------|-------|------|
| Vocabulary | Professional, precise | Controlled, formal | Simple, nervous |
| Sentence length | Medium, complete | Short, clipped | Run-on, rambling |
| Notices first | Details, inconsistencies | Threats, exits | Emotions, faces |
| Internal style | Analytical | Guarded, calculating | Anxious, scattered |
| Verbal tic | Blues lyrics in thoughts | None (too controlled) | "I mean..." |
| Pulp level | 4 | 3 | 2 |

This makes it easy to verify voices stay distinct.

## Chapter Checkpoint: Voice Review

At each chapter checkpoint, verify:

1. **POV consistency**: Did the POV character sound like themselves throughout?
2. **Dialogue attribution**: Could you identify speakers without dialogue tags?
3. **Voice drift**: Any signs of voices becoming similar?
4. **Pulp consistency**: Did pulp level stay consistent with profile?
5. **New characters**: Any new speaking characters who need profiles?

Log any issues and corrections in the validation log.

## Integration with character-voice-architect

If voice issues are detected during drafting:

1. Log the issue
2. After draft completion, run character-voice-architect Mode C (Tuner) on affected scenes
3. Apply suggested fixes
4. Update voice profiles if character voice has evolved intentionally
