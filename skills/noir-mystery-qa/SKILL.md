---
name: noir-mystery-qa
description: Generate prioritized, scene-referenced Fix Lists for noir/mystery/thriller fiction with voice consistency checks. Use when QA-checking scenes for continuity errors, fair-play violations, mystery logic issues, pacing problems, dialogue quality, voice consistency, or formatting inconsistencies. Works standalone on single scenes or as a QA gate within larger revision workflows (Scrivener scene files, chapter batches). Integrates with character-voice-architect voice profiles. Triggers include "QA this scene", "check my mystery scene", "fix list for this chapter", "validate this noir scene", "find issues in my thriller manuscript", or requests to audit fiction for craft/continuity problems before or after editing.
---

# Noir/Mystery/Thriller QA Fix List Generator

Produces actionable, prioritized Fix Lists for noir/mystery/thriller scenes without creating continuity problems, fair-play violations, voice drift, or ripple effects.

## Hard Safety Rules (Non-Negotiable)

- Do NOT invent new plot facts unless explicitly requested
- Do NOT introduce new characters unless explicitly requested
- Do NOT "solve" mystery problems with off-page knowledge or convenient realizations
- Do NOT recommend fixes requiring other-scene changes without flagging as **Cross-scene dependency**
- **Do NOT add memories, backstory, or realizations in suggested rewrites**
- If a fix risks ripple effects (timeline, alibi, clue order, relationships, injuries, locations):
  1. Label it **Cross-scene dependency**
  2. Specify what to check in other scenes
  3. Provide a safer alternative

## Activation Protocol

When activated, ask these questions IN ORDER:

> 1) Paste the scene(s) or provide link(s). Include filenames if possible.
> 2) Any constraints? (Default: no new characters, no new plot facts, preserve POV/tense)
> 3) Confirm: italics reserved for internal thoughts? (yes/no)
> 4) Do you want micro-rewrites included, or instructions only?
> 5) Voice profiles available? (If yes, provide paths for voice consistency checks)

Do not proceed until answered.

## Processing Steps

1. **Segment** input into scenes (filename headers or inferred boundaries)
2. **Build Fact Ledger** per scene:
   - Who present / Where / When
   - Injuries, relationships, known clues, alibis, key objects
3. **Load Voice Profiles** (if available)
4. **Evaluate** in priority order:
   - Continuity + Fair-Play (critical)
   - Mystery Logic
   - **Voice Consistency** (if profiles loaded)
   - Scene structure/pacing (turn, escalation)
   - Dialogue quality (transaction, subtext, fingerprint)
   - Formatting consistency
5. **Generate** Fix List + required sections

## Default Rulebook

### Plot/Scene (Priority 1)

| Rule | Requirement |
|------|-------------|
| P1 | Earn its page: scene does 2+ of: advance plot, escalate stakes, reveal character under pressure |
| P2 | Start late / leave early: cut setup/travel/greetings unless tension/clue-bearing |
| P3 | Scene turn: end with meaningful shift (new fact, suspicion, risk, commitment, loss) |
| P4 | Fair-play: solutions inferable from on-page clues before reveal |
| P5 | Escalate with consequences: raise costs (safety, leverage, reputation, relationships, freedom) |
| P6 | Exposition must change behavior: if it doesn't change decisions or raise tension, cut/convert |

### Voice (Priority 2)

| Rule | Requirement |
|------|-------------|
| V1 | Character dialogue matches established voice profile |
| V2 | POV internal voice consistent with profile |
| V3 | Verbal tics appear at appropriate frequency |
| V4 | Profanity level matches profile and context |
| V5 | Voice doesn't bleed between characters |
| V6 | Emotional expression matches profile patterns |

### Dialogue (Priority 2)

| Rule | Requirement |
|------|-------------|
| D1 | Dialogue is transaction (leverage, threat, temptation, negotiation, evasion, intimacy) |
| D2 | Subtext over statements: rewrite on-the-nose into implication/pressure |
| D3 | Cut transcript filler: remove small talk unless tension/clue-bearing |
| D4 | Indirect answers under pressure (deflect, counter, partial truth, weaponized humor) |
| D5 | Verbal fingerprint per character (rhythm, vocabulary, bluntness, humor, avoidance) |
| D6 | Minimal tag noise: default said/asked; remove adverbs; action beats for power shifts |

### Formatting (Priority 3)

| Rule | Requirement |
|------|-------------|
| F1 | Thoughts = italics ONLY |
| F2 | Text messages: quotes + "he texted/she replied" |
| F3 | Long docs/screens: labeled block inserts, no italics |
| F4 | File names: parentheses — (CaseNotes_11-42PM.txt) |
| F5 | Signs: Title Case or ALL CAPS for shouting |
| F6 | Consistency across project |

## Required Output Format

### A) Fix List

Every item MUST include all fields:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FIX ID: S02-F03
SEVERITY: Critical | High | Medium | Low
SCENE: [filename or "Scene 1"]
LOCATION: "[5–25 word quote]" (P# or near: <phrase>)
ISSUE TYPE: Continuity | Fair-Play | Mystery Logic | Voice Consistency | Pacing | Characterization | Dialogue | Clarity | Formatting
RULE MAPPING: P4, D2, V1
CHARACTER: [Name, if voice issue]
PROFILE REF: [violated trait, if voice issue]
WHY: [1–3 specific sentences]
SAFE FIX:
  - [stepwise instruction with guardrails]
  - Guardrails: do not add facts / preserve clue order / preserve meaning / no new content
SAFETY CHECK:
  - Facts preserved: [list]
  - Cross-scene dependency: None | [specify + what to check + safer alternative]
  - Fidelity: Run content-fidelity-validator on any rewrite
MICRO-REWRITE: [only if requested or ≤3 lines]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### B) Cross-scene Dependency Notes

Only if dependencies exist:

```
CROSS-SCENE DEPENDENCIES
━━━━━━━━━━━━━━━━━━━━━━━━
1. [Fix ID]: [dependency description]
   Check in: [scene/chapter]
   Safer alternative: [option that avoids ripple]
```

### C) Formatting Consistency Summary

```
FORMATTING SUMMARY
━━━━━━━━━━━━━━━━━━
✓ Italics: thoughts only — [PASS/issues found]
✓ Text messages — [PASS/issues found]
✓ Document inserts — [PASS/issues found]
✓ File names — [PASS/issues found]
✓ Signs — [PASS/issues found]
Remaining inconsistencies: [list or "None"]
```

### D) Voice Consistency Summary

Only if voice profiles were loaded:

```
VOICE CONSISTENCY SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━
Profiles loaded: [character list]

Per-character assessment:
✓ [Character A]: Voice consistent | [X issues found]
✓ [Character B]: Voice consistent | [X issues found]

Common issues:
- [Pattern 1]: [count] occurrences
- [Pattern 2]: [count] occurrences

For detailed voice work, consider running character-voice-architect Mode C.
```

## Severity Definitions

| Severity | Criteria |
|----------|----------|
| Critical | Continuity break, fair-play violation, or mystery logic failure |
| High | Scene doesn't earn its page, missing turn, major pacing issue, or significant voice break in POV character |
| Medium | Dialogue quality, characterization drift, voice inconsistency, or clarity problems |
| Low | Formatting inconsistency, minor polish, or minor voice drift |

## Integration Mode

When used as QA gate in larger workflow:

**Pre-Edit QA:** Run before editing to generate Fix List as change plan
**Post-Edit QA:** Run after editing to validate no new issues introduced
**Voice QA:** Run with voice profiles to check characterization consistency

For voice-specific work at scale, use character-voice-architect Mode C, which produces Fix Lists in this same format.

Output includes:
- `[PRE-EDIT]` or `[POST-EDIT]` label
- Comparison notes if both runs available

## Related Skills

| Skill | Relationship |
|-------|--------------|
| **character-voice-architect** | Provides voice profiles, Mode C produces compatible Fix Lists |
| **content-fidelity-validator** | Validates that fixes don't introduce new content |
| **canon-creator** | Provides canon for fact-checking |
| **manuscript-revision-orchestrator** | Can use Fix List as Change Instructions |
