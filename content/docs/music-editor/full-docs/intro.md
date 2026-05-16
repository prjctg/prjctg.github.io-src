---
sidebar_position: 2
---

# Music Editor Full Documentation

The music editor is where song data is created and refined. Accurate data is what lets animations sync precisely to the music — every beat marker, lyric line, and chord you add improves the experience for every animation that uses that song.

---

## What Music Editors Do

A music editor's job is to annotate a song with structured data:

- **Tempo (BPM)** — the foundation of all beat-relative timing
- **Time signatures** — how beats group into measures
- **Keys and chords** — harmonic data that animations can react to
- **Sections** — verse, chorus, bridge, outro, etc.
- **Lyrics** — lines, words, syllables with precise timing
- **Notes** — individual note events for note-level animations

All of this data is what the event system delivers to animations at playback time.

---

## Editor Workflow

1. **Select a song** from the song browser (`/s/e`) or open a song's detail page.
2. **Set the tempo** — enter BPM manually or use the tap detector to derive it from the audio.
3. **Place timing events** — use the beat grid to add and position beats, measures, sections, keys, and chords.
4. **Add lyrics** — type or import lyrics, then align them to the audio timeline.
5. **Split syllables** — break words into syllables for fine-grained sync.
6. **Save** — changes are persisted and immediately available to all animations.

---

## Editor Tabs

When you open a song for editing, several tabs are available:

| Tab | Purpose |
|---|---|
| **Info** | Song title, artists, video URL, duration |
| **Lyrics** | Add and edit lyric lines per language, manage lyric sources |
| **Align** | Time-align lyrics to the audio |
| **Timing** | Beat grid — place and adjust all timing events |

---

## In This Section

The following pages cover each part of the editor in detail:

- [Beat Grid](./beat-grid) — how to place and edit timing events
- [Tempo Editor](./tempo-editor) — setting BPM and handling variable tempo
- [Lyrics Editor](./lyrics-editor) — adding, importing, aligning, and splitting lyrics
