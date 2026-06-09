---
sidebar_position: 5
title: "Beat Grid"
---

# Beat Grid

The beat grid is the visual timeline at the heart of the **Timing** tab. It shows the song's full duration as a horizontal strip, with time running left to right. Every timing event you add — whether a lyric tap, a chord marker, or a section boundary — appears here as a colored marker.

---

## What the beat grid shows

The grid is divided into horizontal rows, one for each type of event:

| Row | What it shows |
|---|---|
| **Beat** | Individual beat markers — the pulse of the song |
| **Measure** | Bar/measure start markers — groups of beats |
| **Section** | Song section boundaries — verse, chorus, bridge, etc. |
| **Key** | Key signature markers |
| **Chord** | Chord change markers |
| **Time Sig** | Time signature change markers |

Below these rows, the lyric timing events are shown (one row per lyric line), so you can see how your text aligns with the beat.

---

## Navigating the grid

- **Scroll horizontally** to move through the song's timeline.
- Use **Zoom In** / **Zoom Out** in the toolbar overflow menu (the three-dots button) to make beats more or less spread out.
- The **playhead** — a vertical line — tracks the current playback position as the song plays.
- Click anywhere in the grid to jump playback to that point in the song.

---

## Toolbar modes

The toolbar has a mode selector that changes what happens when you click or drag on the grid:

| Mode | What it does |
|---|---|
| **Select** | Click to select events; drag to select a range |
| **Edit** | Click an event to edit its value (chord name, section name, etc.) |
| **Add** | Click a row to add a new event at that position |
| **Toggle** | Click a beat position to add an event if none exists there, or remove it if one does |

---

## Adding events

1. Switch to **Add** or **Toggle** mode.
2. Click the row for the type of event you want to add, at the time position you want.
3. For events that carry a label (such as a chord name or section name), a small input appears so you can type the value.

### Chord shortcuts

When you click the Chord row in Add mode, a hotkey overlay appears showing letter shortcuts for common chord names. Press the matching key instead of typing to enter chords quickly.

---

## Moving events

Switch to **Select** mode, then click and drag a marker left or right to move it to a new time position. Events snap to the beat grid by default.

---

## Selecting and deleting events

- Click an event to select it.
- Drag across a range to select multiple events.
- Press **Delete** or use **Ctrl+X** (Cut) to remove selected events.
- Press **Ctrl+A** to select all events.
- Press **Ctrl+C** / **Ctrl+V** to copy and paste a selection to the playhead position.

---

## Snap

The **Snap** button in the toolbar controls whether events snap to beat positions when you drag them. A dropdown next to it lets you choose the snap resolution — for example, 1/4 beat or 1/16 beat.

When Snap is on, clicking **Snap** again snaps the current selection to the nearest grid position at the chosen resolution.

---

## Beat-relative events vs. absolute-time events

Most events are **beat-relative**: they are stored as a beat position (for example, "beat 5.5"), and the editor works out when in the song that beat falls based on the BPM. When you change the BPM, beat-relative events automatically shift to stay on the correct beat.

**Absolute-time events** are pinned to a fixed number of seconds into the song. They do not move when the BPM changes. LRC-imported lyrics arrive as absolute-time events. They are shown with a small indicator in the grid to distinguish them.

Once your BPM is finalized, use **Bake to Beats** — available in the toolbar overflow menu when absolute-time events are present — to convert them to beat-relative events. After baking, they will shift with future BPM changes like everything else.

---

## Streams

Some songs have parts sung simultaneously by different voices. The grid supports **multiple streams** — one stream per voice part. Use the toolbar overflow menu to switch between Single Stream and Multiple Streams, and to select which stream you are currently editing.
