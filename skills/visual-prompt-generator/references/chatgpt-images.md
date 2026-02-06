# ChatGPT Images (DALL-E 3) Prompting Guide

Use when Grok isn't suitable or when you need iterative natural-language refinement.

## Core Understanding

DALL-E 3 uses **prompt rewriting** — GPT-4 optimizes prompts before they reach the image model. This means:
- Short prompts get expanded automatically
- You can give instructions to the rewriter
- Click "i" on generated images to see the actual prompt used

## Prompt Structure

```
[Subject] + [Style] + [Composition] + [Lighting/Mood] + [Technical details]
```

## Critical Limitations

### Negation Handling
DALL-E **cannot process negations** — "no," "don't," "without" often produce the forbidden element.
- ❌ "A scene without any text"
- ✅ "A clean, text-free scene with only visual elements"

**Always describe what you WANT, not what you don't want.**

### Avoid These Patterns
- ❌ "The lighting should be..." → ✅ "Dramatic lighting with strong shadows"
- ❌ "Create an image of..." → ✅ Just describe the image directly
- ❌ "A scene of a forest" → ✅ "A forest at dawn with mist..."

Using "create," "visualize," or "a scene" can trigger meta-imagery (brushes, stages, image-within-image).

### Internal Templates
DALL-E uses templates that can override instructions:
- **Backlight template**: Often adds backlight even when front lighting specified
- **Facial template**: Applies standardized facial features
- **Moon template**: Same moon appears repeatedly (workaround: use "pearl" for celestial spheres)

## Style Parameters

**API/Settings options:**
- `style: "vivid"` — Cinematic, hyper-real (ChatGPT default)
- `style: "natural"` — Subdued, realistic
- `quality: "hd"` — More detail and consistency

**Size options:** 1024×1024, 1792×1024, 1024×1792

**Size affects style:**
- Square → Portrait-style, close compositions
- Wide (1792×1024) → Professional photoshoot feel
- Tall (1024×1792) → Cellphone camera feel, more candid

## Realism Tips

Paradoxically, avoid "photorealistic" or "hyperrealistic":
- These trigger painting styles attempting to look realistic
- **Use "photo style"** instead for camera-like images
- Include camera metadata: "Canon EOS R5, 45MP, 24-70mm f/2.8 lens"

## Content Complexity

DALL-E processes ~256 tokens but only **30-40 graphical elements** translate accurately:
- Beyond this, objects degrade
- Better to guide direction than describe every detail
- Simple mood descriptions affect entire scene

## Order Matters

Elements are weighted by order:
- First-described elements get more attention
- "red, orange, yellow flowers" gives slight red dominance vs. "yellow, orange, red flowers"

## Text in Images

DALL-E struggles with text:
1. Generate the image without text
2. Add text in post (Canva, Photoshop)
3. OR keep text very simple: "neon sign saying OPEN" (one or two words max)

## Iteration Tips

- Start broad, then refine: "I like this, but make the lighting more dramatic"
- Ask for variations: "Same concept but different color palette"
- Use follow-up prompts for specific elements
- To prevent expansion: "Use the prompt unchanged as entered"

## Session Starter (Optional)

To improve GPT's prompt writing:
```
When creating DALL-E prompts:
- Use positive descriptions only (no negations)
- Use direct language (avoid "should," "could")
- Don't use "create an image" or "visualize"
- Don't say "a scene of" — describe directly
- Order elements by importance
```

## Genre Templates

### Noir/Thriller
```
Noir thriller atmosphere, [subject], deep shadows with selective [color] highlights,
wet surfaces reflecting light, moody and atmospheric, [composition],
cinematic lighting with strong contrast, photo style
```

### Vintage/Period
```
[Era] aesthetic, [subject], period-accurate details, [color palette],
film photography feel with subtle grain, [lighting], photo style
```

### Horror/Suspense
```
Unsettling [scene type], [subject], underexposed with pools of [light source],
desaturated except for [accent color], negative space suggesting presence,
atmospheric and dread-filled, photo style
```

## Content Moderation Notes

ChatGPT Images has **stricter moderation** than Grok:
- Violence, even implied, may be rejected
- Noir/thriller scenes may trigger reviews
- Faces of real people are restricted
- "In the style of [living artist]" is blocked

For thriller/noir content, **Grok is the safer default**.
