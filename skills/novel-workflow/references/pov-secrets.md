# POV & Secrets Management for Multi-POV Mystery

Managing character knowledge in POV-switching mysteries is one of the hardest craft challenges. This guide covers both the craft principles and NovelCrafter setup.

## The Core Problem

In a mystery with multiple POVs:
- **April** (secretly the murderer) knows she did it
- **Detective Noah** doesn't know who did it
- **Witness Beth** saw something but doesn't understand what she saw

When AI generates prose, it needs to respect these knowledge boundaries. April's internal monologue should carry guilt; Noah's should carry uncertainty; Beth's should carry confused memory.

## Knowledge Tier System

Organize character knowledge into tiers:

### Tier 1: Universal Knowledge
Facts everyone in the story knows:
- A murder occurred
- The victim's public identity
- The setting/location

### Tier 2: Role-Specific Knowledge
Facts characters know based on their role:
- **Investigators**: Evidence found, witness statements, official timeline
- **Suspects**: Their own alibis, their relationship to victim
- **Witnesses**: What they personally observed

### Tier 3: Secret Knowledge
Facts only specific characters know:
- **The killer**: The truth of what happened
- **Accomplices**: Their piece of the conspiracy
- **Hidden witnesses**: What they're concealing and why

## NovelCrafter Codex Setup

### Character Entry Structure

For each character, create a Codex entry with these sections:

```
[Character Name]

ROLE: [Protagonist/Antagonist/Suspect/Witness/etc.]

PUBLIC PROFILE:
[What anyone meeting them would know — job, appearance, relationships]

KNOWN TO INVESTIGATORS:
[What has been officially established about them in the case]

PRIVATE TRUTH:
[What this character actually knows/did — include secrets here]

POV VOICE NOTES:
[How they think, speak patterns, emotional tendencies]

KNOWLEDGE BOUNDARIES:
- Knows: [list]
- Suspects but doesn't know: [list]
- Does NOT know: [list]
```

### Example: April (Secret Killer)

```
April Marsh

ROLE: Suspect (secretly the killer)

PUBLIC PROFILE:
Victim's business partner. 34, composed, professional demeanor. 
Known for calm under pressure.

KNOWN TO INVESTIGATORS:
- Had access to victim's office
- Alibi: Claims she was at gym (unverified)
- Financial motive: Insurance policy

PRIVATE TRUTH:
- Killed victim at 9:47 PM using the letter opener
- Staged the break-in afterward
- Knows the security camera was disabled
- Carrying guilt masked as grief

POV VOICE NOTES:
- Internal monologue: controlled, calculating, with flashes of panic
- Hyperaware of what others might suspect
- Constantly assessing threats to her secret

KNOWLEDGE BOUNDARIES:
- Knows: She is the killer, exactly how it happened, where evidence is hidden
- Suspects: That Noah is getting closer to the truth
- Does NOT know: That Beth saw her car that night
```

### Example: Detective Noah

```
Noah Mercer

ROLE: Protagonist/Investigator

PUBLIC PROFILE:
FBI agent, mid-30s. Methodical, observant. 
Daily runner, doesn't drink. Listens to old Chicago blues.

KNOWN TO INVESTIGATORS:
- Lead on this case
- Has access to all official evidence

PRIVATE TRUTH:
- Gut says April is involved but can't prove it
- Troubled by gaps in the timeline

POV VOICE NOTES:
- Internal monologue: analytical, notices details others miss
- Blues lyrics sometimes surface in his thoughts
- Professional distance masking personal investment

KNOWLEDGE BOUNDARIES:
- Knows: Official evidence, witness statements, timeline gaps
- Suspects: April's alibi is false, something about the staging feels off
- Does NOT know: April is the killer, Beth saw something important
```

## Custom Prompts for POV-Aware Generation

### POV Scene Generation Prompt

Create a custom prompt in NovelCrafter for drafting POV scenes:

```
You are writing from [CHARACTER]'s point of view.

CRITICAL: This character's knowledge is LIMITED to:
- What they have personally witnessed
- What they have been told by others
- What they have reasonably deduced

This character DOES NOT KNOW:
[Pull from character's "Does NOT know" list]

This character SECRETLY KNOWS (if applicable):
[Pull from character's "Private Truth"]

Write internal monologue and observations that respect these boundaries.
If this character has a secret, let it color their perception without 
explicitly revealing it to the reader (unless this is a reveal scene).

Scene context: [SCENE DESCRIPTION]
```

### Guilt Leakage Prompt (for secret-keepers)

For characters hiding something, subtle tells should leak through:

```
[CHARACTER] is hiding [SECRET].

Write their POV so that:
- They notice things an innocent person wouldn't notice
- Their emotional reactions are slightly "off" — too controlled or too intense
- They have intrusive thoughts they quickly suppress
- Physical stress responses appear (tight jaw, shallow breath, etc.)

Do NOT: Have them explicitly think about their secret in ways that 
reveal it to the reader. Show behavioral leakage, not confession.
```

### Investigation POV Prompt

For detective/investigator characters:

```
[CHARACTER] is investigating and currently believes [CURRENT THEORY].

Write their POV so that:
- They notice clues but may misinterpret them
- Their working theory colors what they pay attention to
- They have professional observation habits
- Uncertainty is present — they're working toward truth, not possessing it

Include: Sensory details they'd notice professionally.
Avoid: Certainty they haven't earned, leaps of logic without evidence.
```

## Scene-Level Knowledge Tracking

For each scene, note:
1. **POV character**: Whose head are we in?
2. **Knowledge state at scene start**: What does POV know entering this scene?
3. **Knowledge change**: What do they learn (or think they learn)?
4. **Reader knowledge**: What has the reader figured out that POV hasn't?

This creates dramatic irony when readers know more than characters, and suspense when characters know more than readers.

## Common Pitfalls

### Pitfall 1: Omniscient Bleed
**Problem**: POV character notices or thinks about things they couldn't know.
**Fix**: Before each scene, explicitly list what this character knows RIGHT NOW.

### Pitfall 2: Inconsistent Secrets
**Problem**: Secret-keeper behaves differently toward the secret in different scenes.
**Fix**: Define the secret-keeper's coping mechanism and apply it consistently.

### Pitfall 3: Reader Confusion
**Problem**: Too many POVs with too many knowledge states.
**Fix**: Limit POV characters (3-4 max for most mysteries). Each should have a distinct voice AND distinct knowledge set.

### Pitfall 4: Premature Revelation
**Problem**: AI generation accidentally reveals secrets through character thoughts.
**Fix**: Use explicit "DO NOT reveal" instructions in prompts. Review AI output for leaks.

## Revision Workflow for Knowledge Consistency

When revising, do a "knowledge audit":

1. Create a timeline of what each character learns and when
2. Read through each POV character's scenes in isolation
3. Flag any moment where they know something they shouldn't
4. Flag any moment where they should react to knowledge but don't

See `references/revision-strategies.md` for prompts to help with this audit.
