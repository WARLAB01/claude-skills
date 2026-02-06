# Revision Strategies for Cascading Changes

Managing large-scale revisions that ripple across multiple chapters is one of the biggest challenges in novel writing. This guide covers strategies and NovelCrafter-specific approaches.

## Types of Cascading Changes

### Type 1: Factual Changes
A detail changes that's referenced multiple times:
- "Tuesday" becomes "Wednesday"
- Character's eye color changes from blue to green
- Location name changes from "Oak Street" to "Elm Avenue"

### Type 2: Timeline Changes
Event order shifts, affecting causality:
- Scene A now happens AFTER Scene B (was before)
- A conversation that set up a later scene now needs different setup

### Type 3: Character Knowledge Changes
What a character knows/doesn't know changes:
- A reveal moved earlier means character knows sooner
- A character now witnessed something they didn't before

### Type 4: Motivation/Arc Changes
A character's underlying reason for acting changes:
- Antagonist's motive shifts from greed to revenge
- Protagonist's goal changes mid-story

## The Revision Audit Process

Before making changes, map the impact:

### Step 1: Identify All Touchpoints
List every scene where the changing element appears or is referenced.

Example for "Tuesday → Wednesday":
```
CHANGE: Murder occurred Wednesday, not Tuesday

TOUCHPOINTS:
- Scene 1.2.3: Noah mentions "Tuesday night" in dialogue
- Scene 2.1.1: April's alibi references Tuesday gym visit
- Scene 2.3.4: Witness statement says "Tuesday evening"
- Scene 3.1.2: Timeline reconstruction scene — full Tuesday reference
- Scene 3.2.1: Final confrontation — "that Tuesday" mentioned
```

### Step 2: Categorize by Impact
- **Simple swap**: Just change the word (dialogue, narration)
- **Logic check needed**: Does the change affect character reasoning?
- **Scene rewrite needed**: The change breaks something fundamental

### Step 3: Process in Dependency Order
Fix upstream scenes before downstream scenes. If Scene 2.1.1's change affects what happens in 2.3.4, fix 2.1.1 first.

## NovelCrafter Revision Prompts

### Factual Find-and-Replace Prompt

For simple factual changes across a scene:

```
REVISION TASK: Change [OLD DETAIL] to [NEW DETAIL]

Review this scene and:
1. Find all instances of [OLD DETAIL] (including indirect references)
2. Replace with [NEW DETAIL]
3. Check that surrounding context still makes sense
4. Flag any passages where the change creates a logic problem

Output the revised scene with changes highlighted.
```

### Timeline Consistency Check Prompt

For verifying timeline after changes:

```
TIMELINE AUDIT for [CHARACTER NAME]

Current scene takes place on [DATE/TIME].

This character's established timeline:
[List key events and when they occurred]

Review this scene and verify:
1. References to past events are correctly placed in time
2. Character's knowledge matches what they'd know at this point
3. Any "yesterday/last week/etc." references are accurate
4. Time-of-day details are consistent

Flag any inconsistencies found.
```

### Character Knowledge Audit Prompt

After moving reveals or changing what characters witness:

```
KNOWLEDGE AUDIT for [CHARACTER NAME]

As of this scene, this character:
- KNOWS: [list]
- SUSPECTS: [list]  
- DOES NOT KNOW: [list]

Review this scene and flag any moment where the character:
1. References knowledge they don't have yet
2. Fails to react to knowledge they should have
3. Has thoughts inconsistent with their knowledge state

Provide specific line references for any issues found.
```

### Motivation Cascade Prompt

When a character's core motivation changes:

```
MOTIVATION REVISION for [CHARACTER NAME]

OLD motivation: [previous motivation]
NEW motivation: [updated motivation]

Review this scene through the lens of the new motivation:
1. Do their actions still make sense?
2. Does their internal monologue align?
3. What subtle changes would make their behavior more consistent?
4. Are there any moments that now ring false?

Suggest specific revisions to align with new motivation.
```

## Workflow: Major Revision in NovelCrafter

### For Factual Changes (Tuesday → Wednesday)

1. **Search**: Use NovelCrafter's search to find all instances
2. **Tag**: Mark each scene needing revision
3. **Batch process**: Use the find-and-replace prompt on each scene
4. **Verify**: Read through the changed scenes for flow

### For Timeline Changes

1. **Map**: Create a before/after timeline
2. **Identify breaks**: Which scenes reference the old timeline?
3. **Triage**: Simple fixes vs. rewrites needed
4. **Fix upstream first**: Start with earliest affected scene
5. **Cascade check**: After each fix, verify downstream scenes

### For Character Arc Changes

1. **Define old vs. new**: Clear statement of what changed
2. **Scene audit**: Which scenes show this character's motivation?
3. **Rewrite key moments**: Scenes where motivation is most visible
4. **Subtlety pass**: Update smaller behavioral tells throughout
5. **Reader test**: Does the character feel consistent?

## Preventing Cascade Problems

### Strategy 1: Codex as Source of Truth
Keep critical facts in NovelCrafter Codex entries. When a fact changes, update the Codex FIRST, then use it as reference for scene revisions.

### Strategy 2: Timeline Document
Maintain a master timeline (in Codex or separate doc) with:
- Date/time of every significant event
- What each character knows at each point
- Update this BEFORE revising scenes

### Strategy 3: Change Log
Track revisions as you make them:
```
REVISION LOG - [Date]

Change: [What changed]
Reason: [Why]
Scenes affected: [List]
Scenes updated: [List with checkmarks]
Outstanding: [Any scenes still needing work]
```

### Strategy 4: Version Snapshots
Before major revisions:
1. Export current state from NovelCrafter
2. Save to Dropbox with date stamp
3. Make revisions
4. If disaster, you can compare/restore

## When Claude Can Help

Use Claude (this conversation) for:
- Planning revision strategy before executing in NovelCrafter
- Generating custom prompts for specific revision needs
- Checking logic of timeline changes
- Discussing whether a change is worth the cascade cost

Example: "I'm thinking of moving the reveal of April's guilt from Chapter 8 to Chapter 6. Can you help me map what that would affect?"

## Integration with Other References

- For knowledge-specific cascades → See `pov-secrets.md`
- For genre-specific revision concerns → See `genre-craft.md`
- For getting revised content into Scrivener → See `scrivener-sync.md`
