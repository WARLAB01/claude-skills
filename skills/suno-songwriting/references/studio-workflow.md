# Suno Studio Workflow

Guide for integrating your own recordings (guitar, piano, etc.) with Suno-generated music.

## Getting Started

Access Studio via the Studio icon under Create in the left panel. The interface provides a Timeline (multi-track arrangement), Transport (play, record, tempo controls), and Context Bar (changes based on current selection).

## Uploading Audio

### From Create Page
1. Click **Audio Upload** button (next to Create)
2. Choose file from device or record new audio
3. Premier plan: up to 8 minutes upload length
4. Add description and click Create for AI generation based on your audio

### In Studio
1. Open Studio project
2. Click **Upload** in the Transport section
3. Select audio file — appears on Timeline for arrangement

## Recording Directly

1. Add a new audio track to Timeline
2. Click **Input** on track → select microphone
3. Set tempo/BPM in Transport (use Metronome for timing)
4. **Arm** track with red Record button on track
5. Press **Record** on Transport
6. Recording uploads to Timeline automatically

**Tip**: Use headphones to prevent feedback when recording.

## Audio Influence Slider

When generating AI content based on your uploaded/recorded audio:
- **Low influence**: AI takes more creative liberty, your audio is a loose guide
- **High influence**: AI closely follows your audio's rhythm, melody, structure

Use higher influence when you want AI drums/instruments to match your recorded pattern closely.

## Workflow: Building a Song Around Your Recording

### Guitar/Piano Track as Foundation
1. Upload or record your guitar/piano part
2. In Create, set your style prompt
3. Adjust **Audio Influence** (higher = closer to your playing)
4. Generate → two versions created
5. Choose preferred version or comp (combine best parts)

### Adding AI Instruments to Your Recording
1. Import your recording to Studio Timeline
2. Use **Context Bar** → Create to add instruments
3. Style prompt example: "Drums and bass to complement acoustic guitar, mid-tempo folk rock"
4. AI generates two takes in **Take Lanes**
5. **Comp** the best parts or choose one
6. Click **Copy to Main Track**

### Extracting and Replacing Elements
1. Generate a full song you like
2. **Get Stems** → Extract into 12 separate tracks
3. Keep the parts you want (vocals, drums, etc.)
4. Replace others with your own recordings
5. Mix in Studio

## Comping (Combining Takes)

When you generate, Suno creates two versions in Take Lanes:
1. Click dropdown on track to see Take Lanes
2. Select portions from each take
3. Combine the best parts into one track
4. **Copy to Main Track** when satisfied

## Mixing

**Volume (Faders)**: Adjust relative loudness of each track (values in dB).
**Panning**: Position tracks left/right in stereo field for space and separation.
**Solo/Mute**: Solo to hear only that track, Mute to silence it.

## Exporting

Access **Export** dropdown (top-right above Timeline):

| Option | Output |
|--------|--------|
| **Full Song** | Complete mix, saves to Library |
| **Selected Time Range** | Highlighted section only |
| **Multitrack** | Individual WAV stems to device |

**Right-click export**: Right-click any clip → Export for that specific clip as audio file.
**MIDI Export**: Studio can analyze audio → generate MIDI for use in your DAW.

All audio exports are high-quality WAV files.

## Typical Workflow: Guitar + AI

1. **Record** 30-60 second guitar part (verse/chorus structure)
2. **Upload** to Suno
3. **Generate** with style prompt: "Add drums, bass, and keys to acoustic guitar, indie folk rock, warm production"
4. **Audio Influence**: 70-80% (keeps your chord progression)
5. **Review** two generated versions
6. **Import to Studio** for mixing
7. **Extract stems** if you want to isolate/replace elements
8. **Add vocals** or additional instruments
9. **Export** final mix

## Tips for Best Results

- **Tempo consistency**: Record to a click if possible
- **Clean recordings**: Less noise = better AI interpretation
- **Clear structure**: Distinct verse/chorus helps AI follow form
- **Style prompt alignment**: Describe the genre you're playing
- **Experiment with influence**: Try different levels to find sweet spot
