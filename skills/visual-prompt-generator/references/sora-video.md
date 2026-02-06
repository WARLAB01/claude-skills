# Sora 2 Video Prompting Guide

Use for video with dialogue/audio when content won't trigger moderation.

## Core Understanding

Sora 2 features:
- Native **audio generation** (dialogue, sound effects, ambience)
- Strong **physics grounding**
- **Multi-shot consistency**
- Improved steerability for camera and materials

**Key insight:** Prompt like briefing a cinematographer who hasn't seen your storyboard. Details you omit get improvised.

## Prompt Philosophy

Two valid approaches:
1. **Detailed prompts** → Control and consistency
2. **Lighter prompts** → Creative freedom, surprising variations

Same prompt = different results each time. This is a feature.

## Technical Parameters (API, not prose)

- **model:** `sora-2` or `sora-2-pro` (higher quality, longer render)
- **size:** 1280×720 or 720×1280 (sora-2); additional sizes for sora-2-pro
- **seconds:** 4, 8, or 12 (default: 4)

Set these in API parameters, not in prompt text.

## Video Length Strategy

Shorter clips follow instructions more reliably:
- Better to stitch two 4-second clips than one 8-second
- Plan for editing/stitching in post

## Prompt Structure

Write prompts like **shot lists** — each shot should have:
- One camera setup
- One subject action
- One lighting recipe

```
[Style/Aesthetic] + [Subject] + [Setting] + [Camera] + [Lighting] + [Action] + [Audio]
```

## Ultra-Detailed Template

For cinematic results:

```
Format & Look:
[Duration] seconds; [shutter]; [capture emulation]; [grain/texture]; [color treatment]

Lenses & Filtration:
[Lens specs]; [filters if any]

Grade / Palette:
Highlights: [description]
Mids: [description]
Blacks: [description]

Lighting & Atmosphere:
[Key light]; [Fill]; [Accents]; [Practicals]; [Atmosphere/Fog]

Location & Framing:
[Setting]; [Foreground]; [Midground]; [Background]

Wardrobe / Props:
Main subject: [detailed description]
Props: [list]

Sound:
[Diegetic sounds]; [Ambient]; [Effects]

Shot Description:
[00:00–XX:XX] — "[Shot Name]" ([lens], [camera movement])
[Detailed action and visual description]
```

## Shorter Prompt Example

For simpler needs:
```
In a 90s documentary-style interview, an old Swedish man sits in a study and says, 
"I still remember when I was young."
```

Works because "90s documentary" sets style implicitly.

## Visual Cues That Work

| Weak | Strong |
|------|--------|
| "A beautiful street at night" | "Wet asphalt, zebra crosswalk, neon signs reflecting in puddles" |
| "Person moves quickly" | "Cyclist pedals three times, brakes, and stops at crosswalk" |
| "Cinematic look" | "Anamorphic 2.0x lens, shallow DOF, volumetric light" |

## Camera Direction

**Framing:**
- "Wide establishing shot, eye level"
- "Medium close-up, slight angle from behind"
- "Aerial wide shot, slight downward angle"

**Motion:**
- "Slowly tilting camera"
- "Handheld ENG camera"
- "Slow dolly-in"
- "Arc around subject to the left"

## Motion and Timing

Keep it simple:
- One clear camera move per shot
- One clear subject action per shot
- Describe actions in beats or counts

❌ "Actor walks across the room"
✅ "Actor takes four steps to the window, pauses, and pulls the curtain in the final second"

## Dialogue Rules

**Critical:**
1. Place dialogue in a **separate block** below visual description
2. Keep lines **concise and natural**
3. **Label speakers** in multi-character scenes
4. Long speeches won't sync — plan for ADR

```
[Visual description paragraph]

Dialogue:
- Detective: "You're lying. I can hear it in your silence."
- Suspect: "Or maybe I'm just tired of talking."
```

**Timing:**
- 4-second shot = 1-2 short exchanges
- 8-second clip = a few more lines

## Audio Description

Even for silent shots, suggest rhythm:
```
Background Sound:
Rain, ticking clock, soft mechanical hum, faint bulb sizzle.
```

## Image-to-Video Workflow

1. Generate still image (DALL-E or Grok) as "first frame"
2. Image must match target video resolution
3. Use as `input_reference` parameter
4. Text prompt defines what happens next
5. Great for character/scene consistency

## Physics Cues

Encode materials and forces explicitly:
- "Wet nylon jacket"
- "8–10 mph crosswind from camera left"
- "Footfalls splashing in shallow puddles"
- "Soft shadow penumbra on wall"

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Motion issues | Simplify to one camera move; specify stability |
| Lip-sync problems | Shorten dialogue; plan ADR in post |
| Text artifacts | Exclude legible text; add overlays in post |
| Physics glitches | Detail surfaces and forces explicitly |
| Color/flicker | Constrain color palettes; fix in post |

## Content Moderation

Sora has **stricter moderation** than Grok:
- Violence may be rejected
- Thriller/noir tension scenes may trigger reviews
- Plan to use Grok image-to-video for restricted content

## Technical Notes

- **Watermark:** Sora adds visible watermark + C2PA metadata
- **Generation time:** Several minutes depending on complexity
- **Models:** `sora-2` (faster) vs `sora-2-pro` (higher quality)
