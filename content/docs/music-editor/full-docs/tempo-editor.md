---
sidebar_position: 6
title: "Tempo Editor"
---

# Tempo Editor

The tempo editor is the **Tempo (BPM)** field in the **Info** tab. Getting the BPM right is the most important step in editing a song — all beat and lyric timing is built on top of it.

---

## What BPM means

BPM stands for "beats per minute." It describes how fast the song moves. A song at 60 BPM has one beat every second. A song at 120 BPM has two beats every second.

Every timing event in the beat grid — beats, measures, chords, sections, and lyrics — is stored as a beat position rather than a raw time. The editor converts beat positions to actual times in the song using the BPM. This means:

- If you change the BPM, all beat-relative events automatically shift to stay on the same beats.
- An accurate BPM keeps everything aligned with the music even after small adjustments.

---

## Typing the BPM directly

If you already know the BPM — from a music database, a DAW, or the original recording — just type it into the BPM field. The change takes effect immediately and all existing events shift to match.

---

## Tap detector

If you don't know the BPM, use the built-in tap detector:

1. Start playback so you can hear the song.
2. Click the **Tap** button in the BPM field in time with the beat — as if you were tapping your foot.
3. After several taps the editor shows the calculated BPM and applies it.

Tap more times for a more accurate result. The first tap or two are less reliable; the accuracy improves as you keep tapping. You can tap along for as long as you like, then stop.

---

## BPM regions (variable tempo)

Some songs are not a single steady tempo throughout. They may have a slow intro, a mid-song tempo change, or a live recording with slight drift.

The tempo editor supports **BPM regions**: sections of the song that each have their own BPM. When the song crosses a region boundary, the editor switches to that region's BPM.

### Adding a region

1. Seek the playhead to the point in the song where the new tempo begins.
2. Click the **+** button next to the BPM field.
3. Enter the BPM value for the new region.

The first region always starts at the very beginning of the song.

### Editing a region

Click the region entry and type a new BPM value.

### Deleting a region

Select the region and press Delete. The first region (starting at time zero) cannot be deleted.

---

## Absolute-time events and BPM changes

If the song contains lyrics imported from an LRC file, those events are anchored to fixed times and will not shift when you change the BPM. This is intentional — their original timestamps are independent of any BPM.

Once you have settled on the right BPM, use **Bake to Beats** in the Timing tab to convert those events so they follow the beat grid. See [Beat Grid](./beat-grid) for details.
