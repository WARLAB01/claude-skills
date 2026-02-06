---
name: suno-one-shot
description: High-quality automated Suno v5 song generation via browser. Use when user wants to create a "one-shot" or "one shot" song directly in Suno. Takes freeform song concepts, generates genre-optimized lyrics using Suno v5 best practices, then fills Suno's create page and clicks Create. Standard one-shots target ~2 minutes; say "long" or "longer" for typical 3-4 minute songs. Handles batch generation (pauses after every 3 songs for Suno processing). Emphasizes clever wordplay and rhyming. Triggers include "create a one-shot", "make a one shot song", "generate a quick song in Suno", or any request to automatically create songs in the Suno browser interface.
---

# Suno One-Shot Generator

High-quality automated workflow for generating songs directly in Suno via browser automation.

---

## Content Guidelines

### Style Prompt Rules

**NEVER include specific artist names in style prompts.** This triggers Suno moderation.

❌ Bad: `"Eminem-style rap, fast flow"`
✅ Good: `"Fast aggressive rap, complex rhyme schemes, storytelling, Detroit hip-hop influence"`

❌ Bad: `"Garth Brooks country ballad"`
✅ Good: `"90s country ballad, rich baritone vocals, acoustic guitar, fiddle, heartfelt storytelling"`

Describe the *sound* and *characteristics*, not the artist.

### Language Guidelines

**Allowed:** mild profanity (shit, damn, hell, ass, bastard)
**NOT allowed:** sexual terms (fuck, pussy, cock, etc.), slurs, extreme vulgarity

Keep it radio-edit friendly unless user explicitly requests otherwise.

### Wordplay & Rhyming Priority

**Unless inappropriate for the genre**, emphasize:
- Clever wordplay, puns, double meanings
- Internal rhymes (rhymes within lines, not just at ends)
- Multi-syllable rhymes ("acceleration" / "celebration")
- Near-rhymes and slant rhymes for sophistication
- Unexpected rhyme payoffs

Genres where this is ESPECIALLY important: Rap/Hip-hop, Musical Theater, Novelty songs
Genres where it's less critical: Ambient, certain EDM, Drone

### Narrative Coherence Check

**For story-driven songs**, before finalizing lyrics, verify:
- [ ] Does the narrative have a clear arc? (setup → development → resolution)
- [ ] Are character motivations clear?
- [ ] Does the timeline make sense?
- [ ] Would a listener understand what's happening?
- [ ] Are there any logical contradictions?

If the story doesn't "make sense," revise before proceeding.

---

## Song Length Options

### Standard One-Shot (~2 minutes or less)
**Default.** Tight structure, no bridge:
```
[Verse 1] - 4-6 lines
[Chorus] - 4-6 lines
[Verse 2] - 4-6 lines
[Chorus]
[Outro] - 2-4 lines
```
Total: ~20-30 lines

### Long/Longer (~3-4 minutes)
**Triggered by:** user says "long", "longer", "full length", "typical length"

Standard song structure with bridge:
```
[Intro] - optional instrumental or short vocal
[Verse 1] - 6-8 lines
[Pre-Chorus] - 2-4 lines (optional)
[Chorus] - 4-6 lines
[Verse 2] - 6-8 lines
[Pre-Chorus]
[Chorus]
[Bridge] - 4-6 lines (contrast section)
[Chorus] - can be double chorus or with variation
[Outro] - 2-6 lines
```
Total: ~40-55 lines

---

## Batch Generation (Multiple Songs)

### Suno Limit: 3 Songs at a Time

Suno processes a maximum of **3 songs simultaneously** (6 total variations since each creates 2).

**For 1-3 songs:** Generate all, then confirm completion.

**For 4+ songs:**
1. Generate songs 1-3
2. **STOP and ask user to confirm** songs are processing/complete
3. Only after confirmation, proceed with songs 4-6
4. Repeat checkpoint pattern every 3 songs

### Batch Workflow

```
Songs 1-3: Generate → Screenshot → CHECKPOINT (wait for user)
Songs 4-6: Generate → Screenshot → CHECKPOINT (wait for user)
Songs 7-9: Generate → Screenshot → CHECKPOINT (wait for user)
...continue pattern...
```

**Checkpoint message:**
> "Songs [X-Y] are now generating. Suno processes 3 at a time, so please confirm when these are done (or well underway) before I submit the next batch."

---

## Workflow

### Step 1: Get Song Concept(s)

Accept freeform description from user. Extract for each song:
- **Genre/Era** (e.g., "50s doo-wop", "synthwave", "90s country")
- **Theme/Subject** (e.g., "wanting ice cream when cold", "midnight drive")
- **Mood/Energy** (e.g., "playful", "melancholic", "defiant")
- **Vocal preference** if mentioned (male/female)
- **Length:** standard (~2 min) or long (~3-4 min)
- **Song count:** single or batch

### Step 2: Match Genre & Apply Conventions

Find the matching genre in the Genre Patterns section below and extract:
- Recommended structure (adjust for length)
- Syllable count per line
- Rhyme scheme
- Lyric conventions and keywords
- Style prompt template
- Default vocal gender

### Step 3: Generate High-Quality Lyrics

**Apply genre conventions:**
- Use the genre's recommended syllable count
- Follow the genre's rhyme scheme
- Include genre-specific vocabulary/keywords
- Match the genre's typical themes and imagery
- **Prioritize clever wordplay and rhyming** (unless genre-inappropriate)

**Apply v5 best practices:**
- Structure tags on own lines: `[Verse 1]`, `[Chorus]`
- 1-3 performance cues max per section: `[Chorus - powerful, belt]`
- Ad-libs in parentheses: `(oh yeah)`, `(hey!)`
- ALL CAPS for belt moments
- Hyphens for sustained notes: `lo-ove`, `wa-ay`
- Consistent syllable counts across parallel sections

**Lyric quality checklist:**
- [ ] Chorus is hooky and singable
- [ ] Lines match genre's syllable range
- [ ] Rhyme scheme is consistent and clever
- [ ] Imagery is vivid, not generic
- [ ] Natural mouth-feel (read aloud mentally)
- [ ] Wordplay/rhymes are satisfying
- [ ] (If narrative) Story makes logical sense
- [ ] Language is within guidelines

### Step 4: Generate Style Prompt

Use the v5 formula:
```
[Era/Genre], [vocal descriptor], [key instruments], [mood/energy], [production style]
```

**Rules:**
- Keep under 200 characters
- Front-load most important elements
- **NO artist names** — describe the sound instead
- Use genre-specific template from reference

### Step 5: Fill Suno Form via Browser

**CRITICAL: Always set vocal gender.** Don't skip this step.

**Navigate and verify:**
1. Go to `https://suno.com/create`
2. Ensure Custom mode is selected (not Simple)

**Fill fields (use `find` tool for each):**

| Field | Find Query | Action | Required |
|-------|-----------|--------|----------|
| Lyrics | `"lyrics textarea input"` | form_input | ✅ Yes |
| Style | `"style prompt input textbox"` | form_input | ✅ Yes |
| Advanced Options | `"Advanced Options expand button"` | left_click to expand | ✅ Yes |
| **Vocal Gender** | `"Male button vocal gender"` or `"Female..."` | **left_click** | ✅ **YES - Don't forget!** |
| Song Title | `"Song Title Optional input field"` | form_input | ✅ Yes |
| Create | `"Create button to generate song"` | left_click | ✅ Yes |

**Important:** Element refs change after scrolling/clicking. Always re-find elements.

### Step 6: Confirm Generation

After clicking Create:
- Take screenshot to verify songs appear in queue
- Confirm 2 variations are generating
- Report success to user

**For batches:** After every 3rd song, STOP and checkpoint with user.

---

## Vocal Gender Selection

**ALWAYS set this. Don't skip.**

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
| Rap/Hip-hop | Usually Male (unless specified) |
| 80s/90s Country | Varies (check artist style) |
| Outlaw Country | Male |
| Musical Theater | Varies by character |

If ambiguous, ask user or choose based on lyric perspective.

---

## Quick Reference: Describing Artists Without Naming Them

| Instead of... | Use... |
|---------------|--------|
| "Eminem style" | fast aggressive rap, complex rhyme schemes, storytelling, emotional intensity, Detroit hip-hop |
| "Lin-Manuel Miranda" | hip-hop musical theater, rapid-fire lyrics, historical storytelling, Broadway meets hip-hop |
| "Garth Brooks" | 90s country, rich baritone, acoustic guitar, fiddle, heartfelt anthemic storytelling |
| "Journey" | 80s arena rock, soaring tenor vocals, anthemic choruses, piano-driven power ballads |
| "Stranger Things soundtrack" | 80s analog synth, dark atmospheric, pulsing arpeggios, cinematic tension, retro horror |
| "Guns N' Roses" | late 80s hard rock, raw gritty vocals, heavy guitar riffs, blues-influenced swagger |

---

## Error Handling

| Problem | Solution |
|---------|----------|
| Element not found | Re-run `find` with alternative query |
| Form not filling | Scroll element into view first |
| Create button inactive | Verify Lyrics and Style fields have content |
| Wrong workspace | Check workspace dropdown before creating |
| **Forgot vocal gender** | Go back, expand Advanced Options, set it |
| Batch >3 songs | Checkpoint after every 3 songs |
| Story doesn't make sense | Revise narrative before generating |

---

# Suno v5 Metatags Reference

## V5 Key Improvements

- Tags processed more consistently than v4.5
- Clearer emotion parsing
- Better section-aware editing
- Respects exclusions better (e.g., "no autotune" works)
- Better syllable alignment and phrasing

---

## Structure Tags

### Primary Sections
| Tag | Usage |
|-----|-------|
| `[Intro]` | Opening, sets tone (4-8 bars typical) |
| `[Verse]` or `[Verse 1]` | Story/narrative section |
| `[Pre-Chorus]` | Tension builder before chorus |
| `[Chorus]` | Hook, most memorable part |
| `[Post-Chorus]` | Momentum after chorus |
| `[Bridge]` | Contrast section, often before final chorus |
| `[Outro]` | Closing section |
| `[End]` | Hard stop signal |

### Instrumental Sections
| Tag | Usage |
|-----|-------|
| `[Instrumental]` | General instrumental break |
| `[Guitar Solo]` | Guitar-focused section |
| `[Piano Solo]` | Piano-focused section |
| `[Drum Break]` | Percussion-focused |
| `[Interlude]` | Transitional instrumental |

### Dynamic/Energy Tags
| Tag | Usage |
|-----|-------|
| `[Build]` | Energy increase |
| `[Drop]` | EDM-style drop |
| `[Break]` | Strip-down moment |
| `[Climactic]` | Peak energy |
| `[Big Finish]` | Powerful ending |
| `[Fade Out]` | Gradual ending |

---

## Vocal/Performance Tags

### Delivery Style (use as modifiers)
```
[Verse 1 - whisper]
[Chorus - belt, powerful]
[Bridge - spoken word]
[Verse 2 - falsetto]
```

### Vocal Style Tags
| Tag | Best For |
|-----|----------|
| `[whisper]` | Intimate intros, bridges |
| `[shout]` | Punk, metal, high-energy |
| `[belt]` | Powerful chorus moments |
| `[falsetto]` | High emotional moments |
| `[raspy]` | Blues, rock |
| `[breathy]` | Pop ballads, dream pop |
| `[spoken word]` | Bridges, intros |
| `[rap verse]` | Hip-hop sections |

### Inline Vocal Cues
- `(oh yeah)` `(hey!)` — Ad-libs in parentheses
- `ALL CAPS` — Belt/emphasis
- `lo-ove`, `sooo-long` — Sustained notes with hyphens

---

## V5 Best Practices

1. **Structure First** - Start with clean section tags
2. **1-3 Performance Cues Per Section Max** - Too many = confused output
3. **Consistent Labels** - If you use `[Pre-Chorus]`, keep using it
4. **Front-Load Intent** - Most important descriptors in first 20-30 words
5. **Tags Reinforce, Not Replace** - Lyrics still need the cadence you want

---

## Style Prompt Formula

**Template:**
```
[Era/Genre], [vocal descriptor], [mood/energy], [key instruments], [production notes]
```

**Examples:**

**Synthwave:**
```
Synthwave, 100 BPM, nostalgic night-drive. Soft dream-pop vocals. Instruments: analog bass, gated snares, Juno pads. Tape warmth, wide stereo.
```

**50s Doo-Wop:**
```
1950s doo-wop, playful male vocals, finger snaps, upright bass, warm reverb, sock hop energy, novelty song, vintage production.
```

**Arena Rock:**
```
Arena rock, powerful belting vocals, driving drums, power chords, melodic guitar hooks, anthemic and defiant, big 80s production.
```

---

# Genre Patterns & Lyric Conventions

## Table of Contents
1. Vintage/Retro (50s Doo-Wop, Motown, Rockabilly, Torch Songs)
2. Rock/Alternative (Classic Rock, Arena Rock, Indie, Punk)
3. 80s Music (Synth/Stranger Things, Arena Rock, Hair Metal, New Wave)
4. Rap/Hip-Hop & Spoken Word (Storytelling, Musical Theater, Old School, Spoken Word)
5. Country (80s/90s, Outlaw, Modern)
6. Modern Pop/Electronic (Synthwave, Pop, EDM, Indie Electronic)

---

## Vintage/Retro

### 50s Doo-Wop

**Default Vocal:** Male | **Syllables:** 6-10 | **Rhyme:** AABB (strict)

**Lyric Conventions:**
- Simple, innocent themes: young love, heartbreak, dancing
- Nonsense syllables: `Doo-wop, shoo-bop!`, `Sha-na-na`
- Direct address: "my baby," "my darling"

**Style Template:**
```
1950s doo-wop, [male/female] vocals, finger snaps, upright bass, [mood], warm reverb, vintage production
```

---

### 60s Soul/Motown

**Default Vocal:** Varies | **Syllables:** 8-12 | **Rhyme:** ABAB (strict)

**Lyric Conventions:**
- Emotional directness: "I need you," "Don't leave me"
- Call-and-response built in
- Gospel-influenced phrasing

**Style Template:**
```
1960s Motown soul, [powerful/smooth] vocals, punchy horns, driving bass, tambourine, warm analog
```

---

### Torch Songs/Big Band

**Default Vocal:** Female | **Syllables:** 10-14 | **Rhyme:** ABAB (moderate)

**Lyric Conventions:**
- Sophisticated vocabulary
- Metaphors: smoke, rain, shadows, empty rooms
- Internal rhyme and near-rhyme

**Style Template:**
```
1940s torch song, [smoky/intimate] vocals, sparse piano, muted trumpet, strings, melancholic, jazz club atmosphere
```

---

## Rock/Alternative

### Classic Rock

**Default Vocal:** Male | **Syllables:** 8-12 | **Rhyme:** ABAB (moderate)

**Lyric Conventions:**
- Universal themes: freedom, rebellion, love, the road
- Imagery: highways, fire, night, thunder
- One killer hook line in chorus

**Style Template:**
```
Classic rock, [driving/mid-tempo], [gritty/soaring] vocals, crunchy guitar riffs, powerful drums, [mood]
```

---

### Arena Rock/Power Ballad

**Default Vocal:** Male | **Syllables:** 6-10 | **Rhyme:** AABB (strict)

**Lyric Conventions:**
- Themes: perseverance, love, defiance
- "We/us" language for anthemic feel
- ALL CAPS for belt moments

**Style Template:**
```
Arena rock, [powerful/anthemic], belting vocals, driving drums, power chords, melodic guitar hooks, big 80s production
```

---

### Punk

**Default Vocal:** Male | **Syllables:** 4-8 | **Rhyme:** AABB (strict)

**Lyric Conventions:**
- Direct, no metaphor necessary
- Anger, frustration, sarcasm
- Short punchy lines, shouted delivery

**Style Template:**
```
Punk rock, [fast/aggressive], [shouted/snarled] vocals, distorted guitars, pounding drums, raw production, DIY energy
```

---

## 80s Music

### 80s Synth/Stranger Things Style

**Default Vocal:** Either/Instrumental | **Syllables:** 8-12 | **Rhyme:** ABCB (loose)

**Lyric Conventions:**
- Themes: danger, the unknown, night, something lurking
- Cinematic imagery: shadows, lights flickering, running
- Sparse lyrics okay — atmosphere matters more

**Style Template:**
```
80s analog synth, dark atmospheric, pulsing arpeggios, cinematic tension, retro horror, Carpenter-style, VHS aesthetic
```

---

### 80s Arena Rock (Journey, Styx style)

**Default Vocal:** Male (high tenor) | **Syllables:** 8-12 | **Rhyme:** ABAB (strict)

**Lyric Conventions:**
- Themes: don't stop believin', holding on, open arms
- Geographic imagery: city lights, highways, small town to big dreams
- Belt-worthy sustained vowels in chorus

**Style Template:**
```
80s arena rock, soaring tenor vocals, piano-driven, anthemic chorus, big drums, melodic guitar, inspirational, stadium-sized production
```

---

### 80s Hair Metal/Glam

**Default Vocal:** Male (high) | **Syllables:** 6-10 | **Rhyme:** AABB (simple)

**Lyric Conventions:**
- Themes: partying, girls, rock n' roll lifestyle
- Braggadocious attitude
- "Tonight" and "rock" appear constantly
- Exclamations: "Yeah!" "Whoa!" "C'mon!"

**Style Template:**
```
80s hair metal, high-pitched male vocals, heavy guitar riffs, flashy guitar solo, big drums, Sunset Strip glam, arena production
```

---

### 80s New Wave

**Default Vocal:** Either | **Syllables:** 6-10 | **Rhyme:** ABAB (playful)

**Lyric Conventions:**
- Themes: alienation, modern life, relationships (detached)
- Ironic or clever observations
- Less emotional, more cerebral

**Style Template:**
```
80s new wave, [synth-driven/angular guitar], [detached/cool] vocals, danceable beat, post-punk influence, MTV era production
```

---

## Rap/Hip-Hop & Spoken Word

### Storytelling Rap (Eminem-style)

**Default Vocal:** Male | **Syllables:** 10-16 (dense) | **Rhyme:** AABB + heavy internal | **Wordplay:** EXTREMELY HIGH

**Lyric Conventions:**
- COMPLEX RHYME SCHEMES ARE CRITICAL
- Internal rhymes every line (rhyme mid-line, not just end)
- Multi-syllable rhymes: "memorable" / "terrible" / "bearable"
- Personal narrative with emotional stakes

**Example Internal Rhyme:**
```
"I'm STANDING at the BRINK of my SANITY SINKING
While HANDING out the DRINKS and I'm FRANTICALLY THINKING"
```

**Style Template:**
```
Fast aggressive rap, complex rhyme schemes, emotional intensity, storytelling, rapid-fire flow, Detroit hip-hop influence, minimal beat, raw delivery
```

---

### Hip-Hop Musical Theater (Hamilton-style)

**Default Vocal:** Varies | **Syllables:** 8-14 | **Rhyme:** Complex, multi-syllable | **Wordplay:** EXTREMELY HIGH

**Lyric Conventions:**
- Dense historical/literary references
- Puns and double meanings constantly
- Mix rap verses with sung hooks
- Rhymes that feel inevitable but surprising

**Example:**
```
"I'm past patiently waitin', I'm PASSIONATELY smashin' every
EXPECTATION, every ACTION's an ACT of creation"
```

**Style Template:**
```
Hip-hop musical theater, rapid-fire lyrics, Broadway meets hip-hop, orchestral and beat fusion, clever wordplay
```

---

### Old School/Party Rap

**Default Vocal:** Male | **Syllables:** 8-12 | **Rhyme:** AABB (playful) | **Wordplay:** HIGH

**Reference Songs:** Bust a Move, Fresh Prince, Thong Song, Damn It Feels Good to Be a Gangsta

**Lyric Conventions:**
- FUN over technical complexity
- Storytelling with humor
- Party situations, dating scenarios
- Call-and-response opportunities

**Style Template:**
```
Old school hip-hop, [party/playful] vibe, bouncy beat, storytelling, funky bassline, 90s production, feel-good energy
```

---

### Spoken Word Poetry

**Default Vocal:** Either | **Syllables:** 8-16 (varies) | **Rhyme:** Optional (near-rhyme preferred) | **Wordplay:** HIGH

**Reference:** "Wo-man" from So I Married An Axe Murderer

**Lyric Conventions:**
- NO fixed meter required — natural speech rhythm
- Repetition as rhetorical device ("She was... She was...")
- Lists that build intensity
- Can be comedic OR dramatic

**Example "Wo-man" Style:**
```
Woman
Woah-man
She was a THIEF, you gotta BELIEVE
She stole my HEART and my CAT
```

**Style Template:**
```
Spoken word poetry, [dramatic/comedic] delivery, rhythmic speech, building intensity, [jazz/minimal beat], theatrical performance
```

---

## Country

### 80s/90s Country (Garth Brooks Era)

**Default Vocal:** Varies | **Syllables:** 8-12 | **Rhyme:** ABAB (strict)

**Reference:** Garth Brooks, George Strait, Brooks & Dunn, Reba McEntire

**Lyric Conventions:**
- STORYTELLING is paramount — beginning, middle, end
- Working class imagery: trucks, bars, farms, small towns
- Specific details make it real ("1989 Ford truck")
- Twang-friendly words (don't, ain't, y'all)

**Style Template:**
```
90s country, [rich baritone/warm alto] vocals, acoustic guitar, fiddle, steel guitar, heartfelt storytelling, Nashville production
```

---

### Outlaw Country

**Default Vocal:** Male | **Syllables:** 8-10 | **Rhyme:** AABB (simple)

**Lyric Conventions:**
- Anti-hero perspective: outlaws, gamblers, drinkers
- Unapologetic about vices
- Dark humor welcome
- References to the road, running, law, freedom

**Style Template:**
```
Outlaw country, [gruff/weathered] male vocals, sparse acoustic guitar, rebellious attitude, 1970s Austin sound, raw production
```

---

## Modern Pop/Electronic

### Synthwave/Retrowave

**Default Vocal:** Either | **Syllables:** 8-12 | **Rhyme:** ABAB (moderate)

**Lyric Conventions:**
- Themes: night drives, neon, memories, escape
- Atmospheric imagery: rain, lights, highways
- Romantic but melancholic

**Style Template:**
```
Synthwave, [soft/powerful] vocals, nostalgic night-drive, analog bass, gated snares, Juno pads, tape warmth
```

---

### Modern Pop

**Default Vocal:** Either | **Syllables:** 6-10 | **Rhyme:** ABAB (strict)

**Lyric Conventions:**
- Relatable themes: love, heartbreak, confidence
- Pre-chorus creates anticipation
- One undeniable hook line in chorus

**Style Template:**
```
Modern pop, [upbeat/emotional], [polished/breathy] vocals, synth bass, catchy hooks, radio-ready production
```

---

### EDM/Dance

**Default Vocal:** Either | **Syllables:** 4-8 | **Rhyme:** AABB (simple)

**Lyric Conventions:**
- Simple, repetitive phrases
- Energy and movement themes
- Hooks designed for chanting

**Style Template:**
```
[EDM subgenre], [BPM], high energy, [euphoric/dark], heavy bass, festival-ready production
```

---

## Quick Reference Tables

### Syllables by Genre

| Genre | Syllables/Line |
|-------|---------------|
| Doo-Wop | 6-10 |
| Motown | 8-12 |
| Torch Song | 10-14 |
| Classic Rock | 8-12 |
| Arena Rock | 6-10 |
| Punk | 4-8 |
| 80s Synth | 8-12 |
| Storytelling Rap | 10-16 |
| Old School Rap | 8-12 |
| Spoken Word | 8-16 |
| 90s Country | 8-12 |
| Outlaw Country | 8-10 |
| Synthwave | 8-12 |
| Modern Pop | 6-10 |
| EDM | 4-8 |

### Wordplay Priority by Genre

| Genre | Wordplay Priority |
|-------|-------------------|
| Storytelling Rap | **VERY HIGH** |
| Musical Theater Rap | **VERY HIGH** |
| Old School Rap | High |
| Spoken Word | High |
| Torch Song | High |
| Most other genres | Medium |
| Punk, EDM, Hair Metal | Low |

---

## Sources

- [Jack Righteous Suno Guides](https://jackrighteous.com/en-us/pages/suno-ai-meta-tags-guide)
- [OpenMusicPrompt](https://openmusicprompt.com/blog/suno-ai-metatags-guide)
- [HowToPromptSuno](https://howtopromptsuno.com/)
- [Suno v5 Wiki](https://www.sunov5.wiki/)
