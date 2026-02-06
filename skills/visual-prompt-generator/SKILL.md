---
name: visual-prompt-generator
description: Generate high-quality prompts for AI image and video generation (Grok Imagine, ChatGPT Images, Sora). Use when creating book covers, character sheets, location reference images, scene visualizations, cinematic stills, or video clips. Can analyze prose (chapters, manuscripts) to extract visual elements and build a Visual Canon (characters, locations, props) for consistent image generation. Integrates with novel-workflow for Scrivener/NovelCrafter exports. Triggers include "create a book cover," "visualize this scene," "character sheet for [name]," "extract visuals from this chapter," "build a visual canon," "image prompt for," "video prompt for," or any request for AI-generated imagery related to fiction writing.
---

# Visual Prompt Generator

Generate prompts for AI image/video tools with emphasis on Grok Imagine (fewer content restrictions for thriller/noir work).

## Workflow Entry Point

### Step 1: Determine Task Type

Ask:

> **What are we creating today?**
> 1. **Book Cover** — Marketing-ready cover art with typography space
> 2. **Character Sheet** — Consistent character reference images
> 3. **Location/Setting** — Establishing shots, atmosphere reference
> 4. **Scene Visualization** — Specific moment from narrative
> 5. **Cinematic Still** — Film-frame aesthetic, dramatic composition
> 6. **Video Clip** — Motion via Grok image-to-video pipeline
> 7. **Visual Canon Extraction** — Scan prose to build character/location/prop bible

### Step 2: Tool Selection

**Default: Grok Imagine** — Fewer content restrictions, excellent photorealism, better for thriller/noir content.

Use ChatGPT Images when:
- Need iterative refinement with natural language
- Creating stylized/illustrated art (not photorealistic)
- Content is clearly non-violent/non-mature

Use Sora when:
- Need longer video with dialogue/audio
- Content won't trigger moderation

**Note**: OpenAI tools (ChatGPT Images, Sora) have stricter content moderation that may flag thriller/noir scenes. Grok is the safer default for this genre work.

---

## Visual Canon System

For consistent visuals across a project, build and maintain a Visual Canon document.

### Extraction Workflow

When given prose (chapters, manuscript sections):

1. **Scan for visual elements:**
   - Characters: Physical description, typical clothing, distinguishing features, age, build
   - Locations: Architecture, lighting, atmosphere, key details, time period indicators
   - Props: Significant objects, vehicles, weapons, recurring items
   - Mood/Palette: Lighting tendencies, color associations, weather patterns

2. **Output structured Visual Canon** (save as markdown):
   ```
   # Visual Canon: [Project Name]
   
   ## Characters
   ### [Character Name]
   - **Physical**: [height, build, hair, eyes, skin, age range]
   - **Distinguishing features**: [scars, tattoos, mannerisms]
   - **Typical clothing**: [style, colors, specific items]
   - **Visual shorthand**: [one-line prompt snippet]
   
   ## Locations
   ### [Location Name]
   - **Type**: [interior/exterior, building type]
   - **Key details**: [architectural features, furniture, objects]
   - **Lighting**: [natural/artificial, time of day, mood]
   - **Atmosphere**: [clean/grimy, modern/vintage, etc.]
   - **Visual shorthand**: [one-line prompt snippet]
   
   ## Props
   ### [Prop Name]
   - **Description**: [physical details]
   - **Context**: [where it appears, significance]
   
   ## Mood & Palette
   - **Dominant colors**: [list]
   - **Lighting style**: [description]
   - **Genre visual cues**: [noir shadows, thriller tension, etc.]
   ```

3. **Offer to save** the Visual Canon as a reference document for future sessions.

### Using the Visual Canon

When generating prompts for a project with an existing Visual Canon:
- Pull character descriptions directly into prompts
- Maintain location consistency across images
- Apply established mood/palette to all visuals

---

## Output Type Workflows

### Book Cover

**Goal**: Marketing-ready art with space for title/author text.

**Prompt structure**:
```
[Mood/genre] book cover art, [central visual element], [composition notes], 
[color palette], [style reference], square format with clear space at 
[top/bottom] for title text, [lighting], professional book cover design
```

**Key considerations**:
- Leave 20-30% negative space for typography (usually top third)
- Favor symbolic/evocative imagery over literal scene depiction
- Genre signals: noir = shadows/silhouettes, thriller = tension/motion blur
- Avoid faces unless character-driven (faces compete with title)

**Example**:
```
Noir thriller book cover art, rain-slicked Chicago street at night with 
single figure silhouetted against neon bar sign, deep shadows with 
selective red and blue neon highlights, moody and atmospheric, 
square format with clear dark space at top for title, 
cinematic lighting with strong backlight, professional book cover design
```

### Character Sheet

**Goal**: Consistent reference image(s) for a character.

**Prompt structure**:
```
[Character description from Visual Canon], [pose/expression], 
[clothing for this image], [lighting setup], [background], 
character reference photo style, [camera/lens notes]
```

**For multiple angles** (generate separately):
- Front-facing neutral expression
- Three-quarter profile
- Full body showing clothing/posture
- Action pose typical of character

**Consistency tips**:
- Use identical physical descriptors across all prompts
- Specify "same person as previous" won't work — must re-describe fully
- Lock down: hair color/style, eye color, facial structure, build, age range

### Location/Setting

**Goal**: Establishing shot for reference.

**Prompt structure**:
```
[Location type] [time of day], [architectural/environmental details], 
[atmospheric conditions], [lighting], [mood], 
establishing shot, [aspect ratio], cinematic photography style
```

**Example**:
```
Small-town Indiana diner exterior at dusk, 1970s architecture with 
large plate glass windows glowing warm yellow, gravel parking lot 
with two pickup trucks, overcast sky with last light on horizon, 
humid summer atmosphere, establishing shot, 16:9 widescreen, 
cinematic photography style reminiscent of Midwest Gothic
```

### Scene Visualization

**Goal**: Specific narrative moment rendered visually.

**Prompt structure**:
```
[Action/moment], [character(s) with brief description], [setting], 
[emotional tone], [lighting that reinforces mood], [composition], 
[camera angle], cinematic still, photo style
```

**From prose**: Extract the key visual beat, not every detail. Focus on:
- What's the emotional core?
- What single image captures the tension?
- What would a film poster show?

### Cinematic Still

**Goal**: Film-frame aesthetic, could be a movie poster or production still.

**Prompt structure**:
```
Cinematic still from [genre] film, [scene description], 
[character(s)], [dramatic lighting: key light position, shadows, color], 
[lens: 35mm/50mm/85mm], [film stock: Kodak/Fuji], [aspect ratio], 
[director/film reference for style], photo style
```

**Film grammar to invoke**:
- Neo-noir: Fincher (*Se7en*, *Zodiac*), Villeneuve (*Sicario*, *Prisoners*)
- Classic noir: shadows, venetian blinds, low angles
- Midwest Gothic: *No Country for Old Men*, *Fargo* — flat landscapes, oppressive sky
- Southern Gothic: *True Detective S1* — humid, decayed, atmospheric

### Video Clip (Grok Image-to-Video)

**Two-step workflow**:

1. **Generate still image first** using any of the above workflows
2. **Add motion prompt** describing what moves

**Motion prompt structure**:
```
[Subject] + [motion verb + adverb] + [secondary motion] + [camera movement]
```

**Motion prompt principles**:
- Describe what MOVES, not what exists (image already shows that)
- Use degree adverbs: slowly, quickly, violently, subtly
- One primary motion + one secondary motion max
- Camera movements: pan, zoom, dolly, handheld shake, static

**Example image prompt**:
```
Noir detective in trench coat standing in rain-soaked alley, 
neon sign flickering above, steam rising from grate, 
cinematic lighting, photo style
```

**Example motion prompt**:
```
Man slowly turns head to look over shoulder, rain continues falling, 
neon sign flickers irregularly, camera slowly dollies forward
```

---

## Grok Imagine Prompt Principles

**Do**:
- Keep prompts short and specific (quality > quantity)
- Use camera/lens terminology for realism: "85mm lens, shallow depth of field"
- Anchor subjects with prominent features: "man with salt-and-pepper beard," "woman wearing leather jacket"
- Specify lighting explicitly: "single overhead spotlight," "neon blue rim light"
- Include aspect ratio: "16:9 widescreen," "square 1:1 format"
- Use "photo style" for photorealistic output

**Don't**:
- Use negations ("no blur," "without text") — they don't work
- Over-describe — the model expands prompts internally
- Say "create" or "visualize" — just describe the image
- Expect text rendering to be perfect — add text in post

**Photorealism markers**:
- "Photo style" (not "photorealistic" which triggers painting styles)
- Camera metadata: "Canon EOS R5, 35mm lens, f/2.8"
- Skin texture: "natural pores, realistic skin"
- Lighting: "soft natural window light," "practical lighting from desk lamp"

---

## ChatGPT Images (DALL-E) Notes

Use when Grok isn't suitable. See [references/chatgpt-images.md](references/chatgpt-images.md) for full guide.

**Key differences from Grok**:
- Prompts get rewritten by GPT-4 before generation
- Negations don't work here either
- "Vivid" style = cinematic (default), "Natural" = subdued
- Better for illustrated/stylized art
- Stricter content moderation

---

## Sora Video Notes

Use for longer video with dialogue. See [references/sora-video.md](references/sora-video.md) for full guide.

**Key points**:
- Think like a shot list: one camera setup, one action per shot
- Shorter clips (4 sec) follow instructions better than longer
- Place dialogue in separate block below visual description
- Stricter content moderation than Grok

---

## Genre Visual Language

### Noir
- Chiaroscuro lighting (strong contrast, deep shadows)
- Silhouettes and partial faces
- Wet streets reflecting neon
- Cigarette smoke, steam, fog
- Muted palette with selective color (neon signs, red lips)
- Low angles, canted frames
- Venetian blind shadows

### Thriller
- Motion blur suggesting urgency
- Shallow depth of field isolating subject
- Cold color palette (teal, steel blue)
- Harsh overhead or interrogation lighting
- Tight framing creating claustrophobia
- Dutch angles for disorientation

### Mystery
- Obscured elements (faces in shadow, partial views)
- Evidence/clue objects prominent
- Investigative lighting (flashlight beams, desk lamp pools)
- Document/photo textures

### Horror
- Underexposed with pools of light
- Practical lighting sources visible
- Desaturated except for organic colors (blood red, sickly green)
- Wide shots with negative space (something could be there)
- Extreme close-ups of wrong details

### Midwest/Southern Gothic
- Oppressive sky, flat horizons
- Decay and rust
- Washed-out daylight or golden hour extremes
- Isolated structures in landscape
- Humid atmosphere, heat haze

---

## Integration with Novel Workflow

### Scrivener Export Parsing
When provided Scrivener RTF/text exports:
- Scene breaks marked with `#` or `* * *`
- Chapter folders become natural groupings
- Parse synopsis/notes if included

### NovelCrafter Export Parsing
When provided NovelCrafter exports:
- Codex entries contain character/location data — extract to Visual Canon
- Scene summaries indicate key visual moments
- POV markers help identify whose perspective to visualize

### Workflow Integration
```
[Novel Workflow] → [Visual Prompt Generator]
     ↓                      ↓
  Manuscript          Visual Canon
  Codex entries   →   Character sheets
  Scene prose     →   Scene visualizations
  Setting notes   →   Location reference
```

---

## Quick Reference: Task → Prompt Template

| Task | Start With |
|------|------------|
| Book cover | Mood + central symbol + composition + typography space |
| Character | Physical details + clothing + pose + lighting + "character reference" |
| Location | Type + time + details + atmosphere + "establishing shot" |
| Scene | Action + characters + setting + emotion + "cinematic still" |
| Cinematic | Genre film + scene + lighting + lens + film reference |
| Video | Generate still first → add motion verbs + camera movement |

---

## Reference Files

- [references/chatgpt-images.md](references/chatgpt-images.md) — Full DALL-E prompting guide
- [references/sora-video.md](references/sora-video.md) — Full Sora prompting guide
- [references/visual-canon-template.md](references/visual-canon-template.md) — Blank template for new projects
