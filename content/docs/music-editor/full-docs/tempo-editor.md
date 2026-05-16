---
sidebar_position: 4
---

# Tempo Editor

The tempo editor lets you set and refine the BPM (beats per minute) of a song. Getting BPM right is the most important step — all beat-relative events (beats, measures, chords, sections, lyrics) are positioned using beat numbers, and their playback times are derived from the BPM. An accurate BPM means accurate sync.

---

## Setting BPM

You can enter the BPM directly in the BPM input field. If you know the exact BPM from an external source (music database, DAW, etc.), type it in.

The BPM value takes effect immediately. All beat-relative events shift proportionally to reflect the new tempo.

---

## Tap Detection

If you don't know the exact BPM, use the **tap detector**:

1. Start playback.
2. Click (or tap) the **Tap** button in time with the beat you hear.
3. After a few taps, the detected BPM is shown and applied.

Tap more times for a more accurate average. The detector computes the BPM from the intervals between your taps.

---

## BPM Regions (Variable Tempo)

Some songs change tempo mid-way through, or have a short intro that doesn't fit the main BPM. The tempo editor supports **BPM regions**: each region has its own BPM value and starts at a specific time offset.

- **Add a region** by clicking the **+** button next to the BPM input while the playhead is at the desired start position.
- **Edit a region** by clicking on it and entering a new BPM.
- **Delete a region** by selecting it and pressing Delete.

The first region always starts at time zero. Regions are listed in chronological order.

---

## How BPM Affects Events

Every beat-relative event stores a **beat number** (e.g., beat 2.5). At playback time, the scheduler converts that beat number to a time in seconds using the BPM and region boundaries. The formula is:

```
time = startOfRegion + (beatNumber - regionStartBeat) × (60 / regionBPM)
```

When you change the BPM, all beat-relative events automatically recalculate to new positions — no manual adjustment needed.

---

## Absolute-Time Events and BPM Changes

If the song contains **absolute-time events** (see [Beat Grid — Beat-Relative vs. Absolute-Time Events](./beat-grid#beat-relative-vs-absolute-time-events)), those events are deliberately not affected by BPM changes. Their playback position stays fixed in seconds. Their displayed beat position is recalculated to show where they fall within the new BPM grid, but the underlying time anchor does not change.

This is intentional: absolute-time events are typically LRC-imported lyrics whose timestamps are independent of any BPM. Once you have finalized the BPM, use **Bake to Beats** in the beat grid toolbar to convert them to beat-relative events.
