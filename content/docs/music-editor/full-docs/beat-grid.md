---
sidebar_position: 3
---

# Beat Grid

The beat grid is the main timing editor. It displays the song's timeline as a grid of beats and measures, and lets you place, move, and delete timing events.

---

## What the Beat Grid Shows

The horizontal axis is time (seconds). The vertical axis organizes events by type. Each row displays one category of event:

| Row | Event type | Description |
|---|---|---|
| **Beat** | `BEAT` | Individual beat markers |
| **Measure** | `MEASURE` | Bar/measure start markers |
| **Section** | `SECTION` | Song sections (verse, chorus, bridge, etc.) |
| **Key** | `KEY` | Key signature changes |
| **Chord** | `CHORD` | Chord changes |
| **Time Sig** | `TIMESIG` | Time signature changes |

Lyric events (lines, words, syllables) are managed separately in the **Lyrics** and **Align** tabs.

---

## Navigating the Grid

- **Scroll horizontally** to move through the song's timeline.
- **Zoom in/out** to adjust the density of the visible beats.
- The **playhead** (vertical cursor) tracks the current playback position in real time.
- Click anywhere in the grid to seek the song to that time position.

---

## Adding Events

1. Make sure playback is running or seek to the position where you want to add an event.
2. Click the target row at the desired time position to place a new event.
3. For events that carry a value (key, chord, section name, time signature), a popover or input will appear to let you set the value.

### Chord Input

A hotkey overlay is available when placing chord events. Press the corresponding key (shown in the overlay) to quickly enter chord names without typing. The overlay appears automatically when you click the chord row.

---

## Moving Events

Click and drag an event marker horizontally to move it to a different time position. Events snap to the beat grid by default.

---

## Selecting and Deleting Events

- **Click** an event to select it.
- **Click and drag** across a range to select multiple events.
- Press **Delete** or use the **Delete** button in the toolbar to remove selected events.

---

## Toolbar Actions

The toolbar above the beat grid provides additional operations:

### Quantize

Snaps all beat events to the nearest exact beat position derived from the current BPM. Use this after manually tapping beats to clean up small timing imprecisions. This operation affects all events in the current stream group.

### Bake to Beats

When a song contains **absolute-time events** (events whose position is anchored to seconds rather than beat numbers), a **Bake** button appears in the toolbar. Baking converts all absolute-time events into beat-relative events by computing their beat position from the current BPM. After baking, the events move with BPM changes like all other events.

Absolute-time events are typically created by LRC import. See the [Lyrics Editor](./lyrics-editor) for details.

### Delete All

Removes all events in the selected range or the current stream group. Use with care — this operation cannot be undone after saving.

---

## Beat-Relative vs. Absolute-Time Events

Most events are **beat-relative**: they store a beat number, and their playback time is derived from the BPM. When you change the BPM, these events shift proportionally to stay musically aligned.

**Absolute-time events** store a fixed time in seconds and do not shift when BPM changes. They are shown with a visual indicator in the grid. Use the Bake button to convert them to beat-relative when you are satisfied with the BPM.
