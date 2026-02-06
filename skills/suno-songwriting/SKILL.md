---
name: suno-songwriting
description: End-to-end AI songwriting assistant for Suno v5. Use when brainstorming song concepts, generating lyrics, crafting style prompts, or refining songs for Suno AI. Covers the full creative workflow from initial idea through Suno-ready output, including metatag formatting, genre/style vocabulary, Studio integration for custom audio tracks, and Chrome assistant instruction generation for automated Suno page filling.
---

# Suno Songwriting Assistant

## Workflow Entry Point

### Step 1: Persona Check

Ask first:

> **Are you using a persona?**
> - Name an existing persona (see [references/personas.md](references/personas.md))
> - Create a new persona (I'll ask questions to build it)
> - No persona — freestyle/one-off style

If using a persona, load their genre, vocal character, lyric tendencies, and style prompt conventions to inform all subsequent work.

### Step 2: What Are We Working On?

> What are we working on today?
> 1. **Song Ideas** — brainstorming concepts, themes, narratives, or angles
> 2. **Lyrics + Style** — generating or refining lyrics and style prompts for Suno
> 3. **Chrome Instruction** — generate a prompt to paste into Claude Chrome assistant that will fill out the Suno page automatically

### Path 1: Song Ideas

Help develop the concept through questions like:
- What's the story, situation, or emotion?
- Who's the narrator? What's their voice/attitude? *(inform with persona if selected)*
- Target genre or vibe? *(default to persona's genre if selected)*
- Any specific references, punchlines, or moments that must be included?

Deliver 2-3 fleshed-out concept directions. If using a persona, ensure ideas fit their world.

### Path 2: Lyrics + Style

Ask:

> **What should I prioritize?** (Default: hooky/singable chorus)
> - **Rhyme scheme** — tight rhymes, internal rhymes, consistency
> - **Content/narrative** — story clarity, emotional beats, specific details
> - **Style accuracy** — nailing genre conventions, vocal delivery cues
> - **Humor/wit** — punchlines, wordplay, comedic timing
> - **Something else?**

Generate lyrics with matching style prompt. If using a persona, apply their conventions throughout. Always produce Suno-ready output (see formatting below).

### Path 3: Chrome Instruction

Generate a complete instruction prompt that can be pasted into the Claude Chrome assistant while on the Suno create page. The Chrome assistant will then automatically fill out the fields and create the song.

**Single Song vs. Batch:**
- **Single song** — One complete instruction block
- **Batch generation** — Multiple songs with wait-for-confirmation checkpoints

See [Chrome Assistant Instructions](#chrome-assistant-instructions) section below for templates and formatting.

### Creating a New Persona

Walk through these questions to define a new persona:

1. **Name**: What should we call this artist/voice?
2. **Genre/Style**: What genre(s)? What's the sonic world? (e.g., "rockabilly meets riot-girl")
3. **Vocal character**: How does this voice sound and feel? Attitude, texture, delivery quirks?
4. **Lyric tendencies**: What themes, imagery, or structures recur? Hook style? Perspective?
5. **Typical instrumentation**: What's in the band? Key sonic signatures?
6. **Example style prompt**: Draft a go-to Suno style prompt for this persona.

After defining, add the persona to [references/personas.md](references/personas.md) for future use.

---

## Suno v5 Output Format

### Lyrics Field (Custom Mode)

```
[Verse 1]
Lyrics here (6-12 syllables per line typical)

[Pre-Chorus]
Building tension...

[Chorus]
Hook goes here — shorter lines, repetition welcome

[Verse 2]
Story continues...

[Bridge]
Contrast or twist

[Outro]
Resolution or fade
```

### Style Prompt Field

V5 accepts conversational prompts up to ~200 characters. Structure as:
`Genre + vocal descriptor + instrumentation + energy/mood + production notes`

Example: "Upbeat rockabilly with sassy female vocals, twangy guitar, standup bass, playful and defiant energy, vintage 50s production"

---

## Essential Metatags (Quick Reference)

**Structure tags** (in lyrics field):
`[Intro]` `[Verse]` `[Pre-Chorus]` `[Chorus]` `[Bridge]` `[Break]` `[Outro]` `[End]`

**Modifiers** (append to structure tags):
`[Verse 1 - soft, intimate]` `[Chorus - belt, powerful]` `[Bridge - spoken word]`

**Vocal cues** (inline or as tags):
- `(oh yeah)` `(hey!)` — ad-libs in parentheses
- `*whispers*` — delivery instruction
- `ALL CAPS` — emphasis/belt

**Instrumental sections**:
`[Instrumental Break]` `[Guitar Solo]` `[Piano Interlude]`

For complete metatag reference, see [references/metatags.md](references/metatags.md).

---

## Style Prompt Vocabulary

When crafting style prompts, draw from:

**Tempo**: slow ballad, mid-tempo groove, upbeat, driving, breakneck
**Energy**: intimate, building, anthemic, explosive, subdued
**Vocal styles**: breathy, belting, crooning, raspy, soaring, conversational, spoken
**Production**: lo-fi, polished, raw, lush, stripped-down, stadium-sized

For comprehensive genre terms, instruments, and musical vocabulary, see [references/music-glossary.md](references/music-glossary.md).

---

## Lyric-Writing Guidelines

### Chorus Priority
Always craft the chorus first. It should be:
- **Hooky** — memorable melodic phrase or wordplay
- **Singable** — natural mouth-feel, not tongue-twisters
- **Repeatable** — works on second/third listen

### Line Construction
- 6-12 syllables per line (sweet spot for v5)
- Match syllable counts across parallel sections (Verse 1 ↔ Verse 2)
- End-rhymes help Suno find melodic patterns
- Internal rhymes add sophistication without forcing structure

### Narrative Songs
For story-driven songs (common in your work):
- Verse 1: Setup the situation
- Verse 2: Escalate or add complication  
- Bridge: Twist, realization, or emotional peak
- Chorus: The takeaway/thesis that ties it together

---

## Studio Integration

For incorporating your own guitar/piano recordings, see [references/studio-workflow.md](references/studio-workflow.md).

Key capabilities:
- Upload audio tracks (up to 8 min on Premier)
- Record directly into timeline
- Extract stems from generated songs
- Use Audio Influence slider to control how closely generation follows your input
- Export as WAV or multitrack stems

---

## Chrome Assistant Instructions

When the user requests a "Chrome instruction" or wants to generate songs via the Claude Chrome assistant, produce a formatted instruction block they can paste directly into the assistant while on the Suno create page.

### Single Song Template

```
Fill out the Suno song creation page with the following:

**Title:** [Song Title]

**Style Prompt:**
[Genre, vocal descriptor, instrumentation, mood, production — ~200 chars max]

**Lyrics:**
[Full lyrics with metatags]

**Settings:**
- Vocal gender: [Male/Female]
- [Any other settings to adjust]
- Create the song
```

### Single Song Example

```
Fill out the Suno song creation page with the following:

**Title:** Wreckage in My Wake

**Style Prompt:**
Arena rock, powerful belting female vocals, driving drums, crunchy power chords, melodic guitar hooks, anthemic and defiant, big 80s production

**Lyrics:**
[Verse 1]
You walked in like you had a chance
Leather jacket, borrowed stance
I've seen that look a thousand times
On a thousand boys who crossed the line
Thinking they could handle mine

[Pre-Chorus - building]
But I don't do rescue
I don't do saved
I'm the storm you chase
Into an early grave

[Chorus - powerful, anthemic]
I'm the WRECKAGE in my wake
I'm the promise that I break
Every man who tries to stay
Ends up crawling away
(hey!) I'm the fire
(hey!) I'm the fall
I'm the best worst thing
That ever wrecked you all

[Bridge - slower, menacing]
Your mama warned you about girls like me
Said I'd leave you on your knees
She was right
But you still came home with me tonight

[Outro]
Wreckage...
In my wake...

[End]

**Settings:**
- Vocal gender: Female
- Create the song
```

### Batch Generation Template

For generating multiple songs in sequence, use this structure:

```
I need you to help me generate multiple songs in sequence. For each song:
1. Fill in all the fields as specified
2. Click Create
3. WAIT for me to confirm the song has started generating before proceeding
4. Only move to the next song after I confirm

All songs share these settings:
- Vocal gender: [Male/Female]
- Weirdness: [0-100]%
- Style Influence: [0-100]%
- Exclude Styles: [comma-separated list of styles to exclude]

---

## SONG 1: "[Title]"
*Theme: [Brief description]*

**Style prompt:**
[Style prompt text]

**Lyrics:**
[Full lyrics with metatags]

---

Please generate this song and wait for my confirmation before proceeding to Song 2.

---

## SONG 2: "[Title]"
*Theme: [Brief description]*

**Style prompt:**
[Style prompt text]

**Lyrics:**
[Full lyrics with metatags]

---

Please generate this song and wait for my confirmation before proceeding to Song 3.

---

[Continue pattern for additional songs...]

---

## SONG N: "[Title]"
*Theme: [Brief description]*

**Style prompt:**
[Style prompt text]

**Lyrics:**
[Full lyrics with metatags]

---

This is the final song. Please confirm when generation has started.
```

### Batch Generation Notes

**Rate limiting:** Suno generates 2 versions per song. Instruct the Chrome assistant to verify no more than 3 songs (6 versions) are generating simultaneously before submitting the next.

**Checkpoint language:** Use explicit wait instructions:
- "Please generate this song and wait for my confirmation before proceeding to Song N."
- "This is the final song. Please confirm when generation has started."

**Shared settings:** Define common settings once at the top (vocal gender, weirdness, style influence, exclude styles) rather than repeating for each song.

### Settings Reference

Available Suno v5 settings to include in instructions:

| Setting | Values | Notes |
|---------|--------|-------|
| Vocal gender | Male, Female | Primary vocal character |
| Weirdness | 0-100% | Higher = more experimental |
| Style Influence | 0-100% | How closely to follow style prompt |
| Exclude Styles | Comma-separated list | e.g., "male vocals, country, pop, screaming" |

### When to Use Chrome Instructions

Use Chrome instruction format when:
- User wants to generate directly in Suno without copy-pasting fields manually
- User is doing batch generation of multiple related songs
- User says "generate this in Suno," "Chrome prompt," "instruction prompt," or similar

Do NOT use Chrome instruction format when:
- User is brainstorming ideas (use Path 1)
- User wants to review/refine lyrics before generating (use Path 2)
- User explicitly asks for just lyrics and style prompt
