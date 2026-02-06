# NovelCrafter Setup & Configuration

This guide covers Codex setup, custom prompts, and AI generation best practices. **Always web-search for current NovelCrafter documentation** — features update frequently.

## Before You Start: Search Current Docs

```
site:novelcrafter.com [feature name]
NovelCrafter [feature] tutorial
```

This reference provides workflow patterns; official docs have current UI/feature details.

## Codex Organization

### Recommended Category Structure

```
CHARACTERS
├── Protagonists
├── Antagonists  
├── Supporting Cast
└── Minor/Background

LOCATIONS
├── Primary Settings
├── Secondary Locations
└── Referenced Places

OBJECTS
├── Evidence/Clues (for mysteries)
├── Significant Items
└── Weapons/Tools

TIMELINE
├── Backstory Events
├── Story Events
└── Future/Planned Events

WORLDBUILDING
├── Organizations
├── Rules/Laws
└── Culture/History
```

### Character Codex Entry Template

```
[NAME]

BASICS
- Age: 
- Role in story:
- Physical: [brief]
- First appears: Scene [X.X.X]

VOICE
- Speech patterns:
- Internal monologue style:
- Verbal tics/phrases:

RELATIONSHIPS
- [Character]: [relationship + dynamic]

KNOWLEDGE STATE (for mysteries)
- Knows:
- Suspects:
- Does NOT know:

ARC
- Starts as:
- Ends as:
- Key turning points:

NOTES FOR AI
[Specific instructions for how AI should write this character]
```

### Location Codex Entry Template

```
[LOCATION NAME]

TYPE: [Interior/Exterior/Both]
APPEARS IN: Scenes [list]

PHYSICAL DESCRIPTION
[Sensory details — what you see, hear, smell]

ATMOSPHERE/MOOD
[Emotional tone this location evokes]

KEY FEATURES
- [Feature 1]: [relevant detail]
- [Feature 2]: [relevant detail]

ASSOCIATED CHARACTERS
- [Who frequents this place and why]

SECRETS (if any)
[Hidden elements, things not immediately visible]

NOTES FOR AI
[How to describe this place, what to emphasize]
```

## Custom Prompt Templates

### Scene Drafting Prompt

```
Write a scene from [CHARACTER]'s POV.

SCENE SETUP:
- Location: [LOCATION]
- Time: [When]
- Goal: [What POV character wants in this scene]
- Conflict: [What opposes them]

CHARACTER STATE:
- Emotional: [How they feel entering]
- Physical: [Any relevant physical state]
- Knowledge: [What they know/don't know]

SCENE SHOULD:
- [Specific beat or moment that must happen]
- [Tone/atmosphere to maintain]
- End with: [Hook, decision, revelation, etc.]

AVOID:
- [Anything this scene should NOT do]
```

### Dialogue-Heavy Scene Prompt

```
Write a conversation between [CHARACTER A] and [CHARACTER B].

CONTEXT: [Why they're talking, where, when]

CHARACTER A wants: [Goal]
CHARACTER B wants: [Goal]

SUBTEXT: [What's NOT being said but present]

POWER DYNAMIC: [Who has upper hand, does it shift?]

The conversation should:
- Reveal: [Information to come out]
- Advance: [What moves forward]
- End on: [Note/beat to end on]

Voice notes:
- A speaks: [Pattern]
- B speaks: [Pattern]
```

### Action/Tension Scene Prompt

```
Write an action sequence where [CHARACTER] must [OBJECTIVE].

STAKES: [What happens if they fail]

OBSTACLES:
1. [First obstacle]
2. [Complication]
3. [Climax moment]

PACING: [Fast throughout / Build to climax / etc.]

SENSORY FOCUS: [What senses to emphasize]

Physical state: [Injuries, exhaustion, etc. to track]

End state: [How does character end up]
```

### Revision/Rewrite Prompt

```
Revise this scene to [SPECIFIC CHANGE].

KEEP:
- [Elements that should remain]
- [Tone/voice to preserve]

CHANGE:
- [Specific changes needed]

CHECK FOR:
- Consistency with [relevant Codex entries]
- Timeline accuracy
- Character knowledge boundaries

Output the full revised scene.
```

## AI Generation Best Practices

### Before Generating

1. **Set context**: Make sure relevant Codex entries are active/linked
2. **Define scope**: One scene at a time, not multiple
3. **Be specific**: Vague prompts get vague output

### Prompt Specificity Spectrum

**Too vague** (will get generic output):
> Write the next scene

**Better**:
> Write a scene where Noah interviews the witness at the diner

**Best**:
> Write a scene from Noah's POV where he interviews Beth at the Route 30 Diner. He's trying to get her to admit she saw something the night of the murder. Beth is evasive because she's scared. The scene should end with her accidentally revealing she saw a car she wasn't supposed to see.

### Iterative Generation

1. **First pass**: Get the structure and beats down
2. **Voice pass**: Refine character voice and dialogue
3. **Sensory pass**: Add specific sensory details
4. **Cut pass**: Remove overwriting, redundancy

### When AI Output Misses

Common issues and fixes:

| Problem | Fix |
|---------|-----|
| Wrong voice | Add more specific voice notes to Codex entry |
| Knows too much | Add explicit "DOES NOT KNOW" to prompt |
| Too generic | Add specific sensory/location details to prompt |
| Wrong tone | Specify genre conventions (see genre-craft.md) |
| Overwritten | Ask for "lean prose" or specify word count |

## Session Management

### Starting a Writing Session

1. Review where you left off (last scene completed)
2. Check Codex entries for relevant characters/locations
3. Note any recent changes that might affect continuity
4. Set clear goal: "I will draft scenes X.X.X through X.X.X"

### Ending a Writing Session

1. Note stopping point and any loose threads
2. Update any Codex entries that changed
3. Flag scenes needing revision
4. Brief note on what's next

### Context Window Management

NovelCrafter's AI has context limits. For long novels:
- Focus active context on current chapter/act
- Don't try to load entire manuscript
- Use Codex entries to maintain consistency without full text

## Export Considerations

When preparing to move content to Scrivener:
- Clean up any placeholder text
- Resolve revision flags
- Ensure scene breaks are clear
- Note which version you're exporting (for tracking)

See `scrivener-sync.md` for export workflow.
