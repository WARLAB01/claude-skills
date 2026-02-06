---
name: suno-songwriting
description: End-to-end AI songwriting assistant and automated song generator for Suno v5. Use for brainstorming song concepts, generating lyrics, crafting style prompts, refining songs, or creating "one-shot" songs directly in the Suno browser. Covers the full creative workflow from initial idea through Suno-ready output, including metatag formatting, genre-specific lyric conventions, style prompt vocabulary, Studio integration for custom audio tracks, batch generation (pauses after every 3 songs), and Chrome assistant instruction generation. Emphasizes clever wordplay and rhyming. Triggers include "write a song", "brainstorm song ideas", "generate lyrics", "style prompt", "create a one-shot", "make a one shot song", "generate a quick song in Suno", "Suno", "song", "songwriting", or any request to create or refine music for Suno AI.
---

# Suno Songwriting Assistant

## Workflow Entry Point

Ask:

> **What are we working on today?**
> 1. **Song Ideas** — brainstorming concepts, themes, narratives, or angles
> 2. **Lyrics + Style** — generating or refining lyrics and style prompts
> 3. **One-Shot** — generate a song directly in Suno via browser automation
> 4. **Chrome Instruction** — generate a prompt to paste into Claude Chrome assistant

If the user's intent is already clear from their message, skip the question and route directly.

---

## Content Guidelines

### Style Prompt Rules

**NEVER include specific artist names in style prompts.** This triggers Suno moderation.

| Instead of... | Use... |
|---------------|--------|
| "Eminem style" | fast aggressive rap, complex rhyme schemes, storytelling, emotional intensity, Detroit hip-hop |
| "Lin-Manuel Miranda" | hip-hop musical theater, rapid-fire lyrics, historical storytelling, Broadway meets hip-hop |
| "Garth Brooks" | 90s country, rich baritone, acoustic guitar, fiddle, heartfelt anthemic storytelling |
| "Journey" | 80s arena rock, soaring tenor vocals, anthemic choruses, piano-driven power ballads |
| "Stranger Things soundtrack" | 80s analog synth, dark atmospheric, pulsing arpeggios, cinematic tension, retro horror |
| "Guns N' Roses" | late 80s hard rock, raw gritty vocals, heavy guitar riffs, blues-influenced swagger |

Describe the *sound* and *characteristics*, not the artist.

### Language Guidelines

**Allowed:** mild profanity (shit, damn, hell, ass, bastard)
**NOT allowed:** sexual terms (fuck, pussy, cock, etc.), slurs, extreme vulgarity

Keep it radio-edit friendly unless user explicitly requests otherwise.

---

## Path 1: Song Ideas

Help develop the concept through questions like:
- What's the story, situation, or emotion?
- Who's the narrator? What's their voice/attitude?
- Target genre or vibe?
- Any specific references, punchlines, or moments that must be included?

Deliver 2-3 fleshed-out concept directions with suggested genres.

---

## Path 2: Lyrics + Style

### Before Writing: Load Genre Reference

**MANDATORY**: Read [references/genre-patterns.md](references/genre-patterns.md) and find the matching genre entry. Extract:
- Recommended syllable count per line
- Rhyme scheme
- Lyric conventions and keywords
- Style prompt template
- Default vocal gender
- Wordplay priority level

If the genre isn't listed, find the closest match and adapt.

### Lyric Priority

Ask what to prioritize (default: hooky/singable chorus):
- **Rhyme scheme** — tight rhymes, internal rhymes, consistency
- **Content/narrative** — story clarity, emotional beats, specific details
- **Style accuracy** — nailing genre conventions, vocal delivery cues
- **Humor/wit** — punchlines, wordplay, comedic timing

### Writing the Lyrics

**Chorus first.** Always craft the chorus before verses. It should be:
- **Hooky** — memorable melodic phrase or wordplay
- **Singable** — natural mouth-feel, not tongue-twisters
- **Repeatable** — works on second/third listen

**Line construction:**
- Match the genre's syllable count (see genre-patterns.md)
- Match syllable counts across parallel sections (Verse 1 ↔ Verse 2)
- End-rhymes help Suno find melodic patterns
- Internal rhymes add sophistication without forcing structure

**Wordplay & rhyming** (unless inappropriate for genre):
- Clever wordplay, puns, double meanings
- Internal rhymes (rhymes within lines, not just at ends)
- Multi-syllable rhymes ("acceleration" / "celebration")
- Near-rhymes and slant rhymes for sophistication
- Unexpected rhyme payoffs

Genres where wordplay is ESPECIALLY important: Rap/Hip-hop, Musical Theater, Novelty songs, Spoken Word.

**Narrative songs** (story-driven):
- Verse 1: Setup the situation
- Verse 2: Escalate or add complication
- Bridge: Twist, realization, or emotional peak
- Chorus: The takeaway/thesis that ties it together

### Narrative Coherence Check

For story-driven songs, before finalizing, verify:
- [ ] Clear arc? (setup → development → resolution)
- [ ] Character motivations clear?
- [ ] Timeline makes sense?
- [ ] Would a listener understand what's happening?
- [ ] Any logical contradictions?

If the story doesn't make sense, revise before proceeding.

### Style Prompt

**Formula:** `Genre + vocal descriptor + key instruments + mood/energy + production style`

- Keep under 200 characters
- Front-load the most important elements
- **NO artist names** — describe the sound instead
- Use the genre-specific template from genre-patterns.md
- For comprehensive vocabulary, read [references/glossary.md](references/glossary.md)

### Lyric Quality Checklist

Before delivering lyrics, verify:
- [ ] Chorus is hooky and singable
- [ ] Lines match genre's syllable range
- [ ] Rhyme scheme is consistent and clever
- [ ] Imagery is vivid, not generic
- [ ] Natural mouth-feel (read aloud mentally)
- [ ] Wordplay/rhymes are satisfying
- [ ] (If narrative) Story makes logical sense
- [ ] Language is within guidelines

### Output Format

Always produce Suno-ready output:

```
[Verse 1]
Lyrics here (genre-appropriate syllable count)

[Pre-Chorus]
Building tension...

[Chorus]
Hook — shorter lines, repetition welcome

[Verse 2]
Story continues...

[Bridge]
Contrast or twist

[Outro]
Resolution or fade

[End]
```

For metatag options beyond basic structure tags, read [references/metatags.md](references/metatags.md).

---

## Path 3: One-Shot (Browser Automation)

Complete automated workflow: generate lyrics + fill Suno form + click Create.

### Step 1: Get Song Concept

Accept freeform description. Extract:
- **Genre/Era** (e.g., "50s doo-wop", "synthwave", "90s country")
- **Theme/Subject** (e.g., "wanting ice cream when cold", "midnight drive")
- **Mood/Energy** (e.g., "playful", "melancholic", "defiant")
- **Vocal preference** if mentioned (male/female)
- **Length:** standard (~2 min) or long (~3-4 min) — see Song Length section
- **Song count:** single or batch

### Step 2: Generate Lyrics + Style

Follow Path 2 process (load genre-patterns.md, write lyrics, build style prompt, run quality checklist). Do NOT present lyrics to user for review — proceed directly to form filling.

### Step 3: Fill Suno Form

**CRITICAL: Always set vocal gender.** Don't skip this step.

**Navigate and verify:**
1. Go to `https://suno.com/create`
2. Ensure Custom mode is selected (not Simple)

**Fill fields (use `find` tool for each):**

| Field | Find Query | Action | Required |
|-------|-----------|--------|----------|
| Lyrics | `"lyrics textarea input"` | form_input | Yes |
| Style | `"style prompt input textbox"` | form_input | Yes |
| Advanced Options | `"Advanced Options expand button"` | left_click to expand | Yes |
| **Vocal Gender** | `"Male button vocal gender"` or `"Female..."` | **left_click** | **YES** |
| Song Title | `"Song Title Optional input field"` | form_input | Yes |
| Create | `"Create button to generate song"` | left_click | Yes |

**Important:** Element refs change after scrolling/clicking. Always re-find elements.

### Step 4: Confirm Generation

After clicking Create:
- Take screenshot to verify songs appear in queue
- Confirm 2 variations are generating
- Report success to user

---

## Path 4: Chrome Instruction

Generate a complete instruction prompt that can be pasted into the Claude Chrome assistant while on the Suno create page.

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
- Create the song
```

### Batch Template

```
Generate multiple songs in sequence. For each song:
1. Fill in all fields as specified
2. Click Create
3. WAIT for me to confirm before proceeding to the next song

All songs share these settings:
- Vocal gender: [Male/Female]

---

## SONG 1: "[Title]"

**Style prompt:**
[Style prompt text]

**Lyrics:**
[Full lyrics with metatags]

---

Please generate this song and wait for my confirmation before proceeding to Song 2.

---

## SONG 2: "[Title]"
[Continue pattern...]
```

**Rate limiting:** Instruct Chrome assistant to verify no more than 3 songs (6 versions) generating simultaneously before submitting next.

---

## Song Length & Structure

### Standard (~2 minutes or less) — Default

Tight structure, no bridge:
```
[Verse 1] — 4-6 lines
[Chorus] — 4-6 lines
[Verse 2] — 4-6 lines
[Chorus]
[Outro] — 2-4 lines
[End]
```
Total: ~20-30 lines

### Long (~3-4 minutes)

Triggered by: "long", "longer", "full length", "typical length"

Full structure with bridge:
```
[Intro] — optional instrumental or short vocal
[Verse 1] — 6-8 lines
[Pre-Chorus] — 2-4 lines (optional)
[Chorus] — 4-6 lines
[Verse 2] — 6-8 lines
[Pre-Chorus]
[Chorus]
[Bridge] — 4-6 lines (contrast section)
[Chorus] — can be double or with variation
[Outro] — 2-6 lines
[End]
```
Total: ~40-55 lines

---

## Batch Generation

Suno processes max **3 songs simultaneously** (6 total variations since each creates 2).

**For 1-3 songs:** Generate all, then confirm completion.

**For 4+ songs:**
1. Generate songs 1-3
2. **STOP and ask user to confirm** songs are processing/complete
3. Only after confirmation, proceed with songs 4-6
4. Repeat checkpoint every 3 songs

**Checkpoint message:**
> "Songs [X-Y] are now generating. Suno processes 3 at a time — please confirm when these are done (or well underway) before I submit the next batch."

---

## Vocal Gender Defaults

**ALWAYS set this.** Don't skip.

| Genre | Default |
|-------|---------|
| 50s Doo-Wop (group) | Male |
| Motown | Varies by song |
| Rockabilly | Male |
| Torch Song | Female |
| Classic/Arena Rock | Male |
| 80s Hair Metal | Male |
| Synthwave | Either (often male) |
| Modern Pop | Either |
| Rap/Hip-hop | Usually Male |
| 80s/90s Country | Varies |
| Outlaw Country | Male |
| Musical Theater | Varies by character |

If ambiguous, ask user or choose based on lyric perspective.

---

## Essential Metatags (Quick Reference)

**Structure:** `[Intro]` `[Verse]` `[Pre-Chorus]` `[Chorus]` `[Bridge]` `[Break]` `[Outro]` `[End]`

**Modifiers:** `[Verse 1 - soft, intimate]` `[Chorus - belt, powerful]` `[Bridge - spoken word]`

**Vocal cues:**
- `(oh yeah)` `(hey!)` — ad-libs in parentheses
- `*whispers*` — delivery instruction
- `ALL CAPS` — emphasis/belt
- `lo-ove` — sustained notes with hyphens

**Instrumental:** `[Instrumental Break]` `[Guitar Solo]` `[Piano Interlude]`

For the complete metatag reference, read [references/metatags.md](references/metatags.md).

---

## Suno Settings Reference

| Setting | Values | Notes |
|---------|--------|-------|
| Vocal gender | Male, Female | Primary vocal character |
| Weirdness | 0-100% | Higher = more experimental |
| Style Influence | 0-100% | How closely to follow style prompt |
| Exclude Styles | Comma-separated | e.g., "male vocals, country, pop" |

---

## Studio Integration

For incorporating your own guitar/piano recordings into Suno, read [references/studio-workflow.md](references/studio-workflow.md).

Key capabilities: upload audio tracks (up to 8 min on Premier), record directly into timeline, extract stems from generated songs, Audio Influence slider to control how closely generation follows your input, export as WAV or multitrack stems.

---

## Error Handling

| Problem | Solution |
|---------|----------|
| Element not found | Re-run `find` with alternative query |
| Form not filling | Scroll element into view first |
| Create button inactive | Verify Lyrics and Style fields have content |
| Wrong workspace | Check workspace dropdown before creating |
| Forgot vocal gender | Go back, expand Advanced Options, set it |
| Batch >3 songs | Checkpoint after every 3 songs |
| Story doesn't make sense | Revise narrative before generating |
| Style prompt >200 chars | Trim less important descriptors |
| Generic-sounding lyrics | Re-check genre-patterns.md conventions |

---

## Reference Files

| File | When to Load |
|------|-------------|
| [references/genre-patterns.md](references/genre-patterns.md) | **ALWAYS** before writing lyrics — genre-specific syllable counts, rhyme schemes, conventions, style templates |
| [references/glossary.md](references/glossary.md) | When crafting style prompts — comprehensive vocabulary for tempo, genre, vocal, instrumentation, production, mood |
| [references/metatags.md](references/metatags.md) | When using advanced metatags beyond basic structure tags |
| [references/studio-workflow.md](references/studio-workflow.md) | When user wants to integrate their own recordings with Suno |

---

## Sources

- [Jack Righteous Suno Guides](https://jackrighteous.com/en-us/pages/suno-ai-meta-tags-guide)
- [OpenMusicPrompt](https://openmusicprompt.com/blog/suno-ai-metatags-guide)
- [HowToPromptSuno](https://howtopromptsuno.com/)
- [Suno v5 Wiki](https://www.sunov5.wiki/)
