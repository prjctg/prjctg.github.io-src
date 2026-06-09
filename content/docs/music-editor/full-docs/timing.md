---
sidebar_position: 4
title: "Timing"
---

# Timing

The **Timing** tab is where you connect your lyrics to the music. You stamp each lyric line with the exact moment it starts in the song, so animations know when to display or highlight each line.

---

## What timing alignment means

Lyrics in the Lyrics tab are just text — they have no position in the song yet. Alignment gives each line a start time. Once a line is aligned, an animation can react to it: fading it in, scrolling it, or beginning a karaoke highlight at exactly the right moment.

---

## The Timing tab layout

The Timing tab shows two areas:

- **Beat grid (top)** — a visual timeline of the song. Each lyric line you have timed appears as a marker on the grid. See [Beat Grid](./beat-grid) for full details on the grid itself.
- **Lyrics panel (bottom)** — a scrolling view of your lyric lines, showing how many syllables each line has and which lines have been timed.

You can drag the divider between the two areas to resize them.

---

## Recording mode: tapping along with the music

The fastest way to time lyrics is to record while the song plays.

1. Click the **Record** button in the toolbar. The button turns red and recording begins.
2. Play the song from the beginning (or from where you want to start timing).
3. Each time a new lyric line begins, press **C** to stamp that line with the current playback position.
4. To stamp an individual syllable instead of a new line, press **Space**.
5. If you tap too early or too late, press **Backspace** to undo the last tap.
6. Click **Stop** (the red button) when you are done recording.

After your first pass, most lines will be approximately timed. You can then fine-tune individual events in the beat grid.

### Ghost timing

When you have already timed a section of the song (such as the first chorus) and the same section repeats later, the editor shows faint guide markers for the repeated section based on the earlier timing. These ghosts are a preview — your taps replace them.

---

## Fine-tuning with the beat grid

After recording, zoom in on the beat grid and drag individual markers to adjust their positions. Events snap to the beat grid by default, which helps keep everything musically aligned.

Use the **Snap** button in the toolbar to control whether events snap to the grid, and the step dropdown (e.g., 1/4 beat, 1/8 beat) to control how fine the snapping is.

---

## Key change strip

At the top of the beat grid in the Timing tab, a strip shows the current musical key at the playhead position. Click **+ Key change at playhead** to insert a key marker at that moment. This is a quick way to mark key changes while listening to the song. You can also manage key changes more directly in the [Details tab](./musical-data).

---

## Undo and redo

Press **Ctrl+Z** to undo the last action and **Ctrl+Y** to redo it. This works for both recorded taps and manual edits in the grid.

---

## Multiple lyric streams

If the song has parts sung simultaneously by different voices, you can time each voice part on its own stream. Use the stream selector in the toolbar overflow menu to switch between streams. See [Beat Grid — Streams](./beat-grid) for details.

---

## Auto-save

The Timing tab saves your work to your device automatically when you navigate away. Click **Save** in the main toolbar to publish.
