# Suno v5 Metatags Reference

Metatags in `[brackets]` control song structure, vocal delivery, mood, and instrumentation. Most effective in the first 20-30 words and around section changes.

## Structure Tags

### Primary Sections
| Tag | Purpose |
|-----|---------|
| `[Intro]` | Opening section (can be unreliable — try `[Instrumental Intro]` instead) |
| `[Verse]` / `[Verse 1]` | Story/narrative sections with changing lyrics |
| `[Pre-Chorus]` | Builds anticipation before chorus |
| `[Chorus]` | Main hook, repeated section |
| `[Post-Chorus]` | Momentum after chorus |
| `[Bridge]` | Contrasting section, often emotional peak |
| `[Outro]` / `[Ending]` | Closing section |
| `[End]` | Signals song termination |

### Secondary Sections
| Tag | Purpose |
|-----|---------|
| `[Hook]` | Short memorable phrase (can be within chorus) |
| `[Refrain]` | Repeated line/phrase, often at verse ends |
| `[Break]` | Instruments drop out, creates contrast |
| `[Drop]` | EDM-style maximum energy release |
| `[Interlude]` | Instrumental passage between sections |

### Instrumental Sections
```
[Instrumental Intro]
[Guitar Solo]
[Piano Solo]
[Piano Interlude]
[Instrumental Break]
[Drum Break]
[Bass Solo]
```

### Dynamic/Energy Tags
| Tag | Usage |
|-----|-------|
| `[Build]` | Energy increase |
| `[Drop]` | EDM-style drop |
| `[Break]` | Strip-down moment |
| `[Climactic]` | Peak energy |
| `[Big Finish]` | Powerful ending |
| `[Fade Out]` | Gradual ending |

## Section Modifiers

Append descriptors to structure tags for nuance:

```
[Verse 1 - soft, intimate]
[Chorus - belt, powerful]
[Bridge - spoken word]
[Verse 2 - building intensity]
[Outro - fading, wistful]
```

**Rule: 1-3 performance cues per section max.** Too many = confused output.

## Vocal Delivery

### Inline Cues
| Syntax | Effect |
|--------|--------|
| `(oh yeah)` `(hey!)` | Ad-libs (parentheses) |
| `*whispers*` | Delivery instruction (asterisks) |
| `ALL CAPS` | Emphasis, belting |
| `...` | Pause or trailing off |
| `lo-ove`, `sooo-long` | Sustained notes (hyphens) |

### Vocal Style Tags
```
[Vocal Style: Whisper]    — intimate intros, bridges
[Vocal Style: Belt]       — powerful chorus moments
[Vocal Style: Falsetto]   — high emotional moments
[Vocal Style: Raspy]      — blues, rock
[Vocal Style: Crooning]   — smooth ballads
[Vocal Style: Breathy]    — pop ballads, dream pop
[Vocal Effect: Reverb]
[Vocal Effect: Delay]
```

### Delivery as Section Modifiers
```
[Verse 1 - whisper]
[Chorus - belt, powerful]
[Bridge - spoken word]
[Verse 2 - falsetto]
```

## Mood & Energy Tags

```
[Mood: Uplifting]   [Mood: Melancholy]   [Mood: Defiant]
[Mood: Playful]     [Mood: Intense]      [Mood: Dreamy]

[Energy: Low]       [Energy: Building]
[Energy: High]      [Energy: Explosive]
```

## Instrumentation Tags

```
[Instrument: Acoustic Guitar]
[Instrument: Electric Guitar (Distorted)]
[Instrument: Piano]
[Instrument: Strings (Legato)]
[Instrument: Synth Pads]
[Instrument: Drums (Heavy)]
```

## Advanced Tags (V5)

```
[Tempo: Slow] / [Tempo: Mid] / [Tempo: Fast]
[Key: C minor]
[Vocalist: Female] / [Vocalist: Male]
[Genre: Indie Pop]
```

## V5 Best Practices

1. **Structure First** — start with clean section tags
2. **1-3 Performance Cues Per Section Max** — too many = confused output
3. **Consistent Labels** — if you use `[Pre-Chorus]`, keep using it
4. **Front-Load Intent** — most important descriptors in first 20-30 words
5. **Tags Reinforce, Not Replace** — lyrics still need the cadence you want
6. **`[End]` for clean stops** — prevents trailing generation

## Example: Full Song with Metatags

```
[Intro - soft piano]

[Verse 1]
Walking through the empty streets at dawn
Every shadow whispers your name

[Pre-Chorus - building]
And I know, I know, I know...

[Chorus - powerful, soaring]
We were FIRE in the night
Burning bright, burning right
(oh oh oh)

[Verse 2]
*spoken* They said we'd never last
But here I am still holding on

[Bridge - intimate, vulnerable]
Maybe tomorrow, maybe someday
We'll find our way back home

[Chorus - belt, full band]
We were FIRE in the night...

[Outro - fading]
Fire in the night...
*whispers* fire...

[End]
```
