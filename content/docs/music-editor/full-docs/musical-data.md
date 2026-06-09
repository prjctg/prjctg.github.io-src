---
sidebar_position: 7
title: "Musical Data"
---

# Musical Data

The **Details** tab holds four types of musical annotation: Sections, Keys, Chords, and Time Signatures. These are used by animations to react to the structure and harmony of a song — for example, changing color on a chorus, or displaying chord names above the lyrics.

Open the Details tab from the main tab strip. Inside, four sub-tabs are available: **Sections**, **Keys**, **Chords**, and **Time Sig**.

---

## Sections

Sections mark the named structural parts of a song: intro, verse, pre-chorus, chorus, bridge, outro, and so on.

On Animr, sections are derived from your lyrics rather than entered directly here. To create a section, add a label line in square brackets in the **Lyrics** tab — for example:

```
[Verse 1]
Lyric line one
Lyric line two

[Chorus]
Chorus line one
```

The Sections sub-tab then shows each labeled section alongside its start time (pulled from the Timing tab) and a progress indicator showing how many lines in that section have been timed.

### Syncing repeated sections

When the same section appears more than once (for example, a chorus that repeats three times), the Sections view groups them together and marks one as the **source** — the best-timed instance. For the others, a **Sync here** button appears. To sync a repeated section:

1. Start playback.
2. When that section begins in the audio, click **Sync here**.

The timing from the source section is copied across, offset to the new start point.

---

## Keys

A song's musical key describes which notes are "home base" for that song. The key helps certain animations choose colors, highlights, or effects that fit the mood.

The overall key of the song is set in the **Info** tab. Use the **Keys** sub-tab to mark any points where the key changes mid-song.

### Adding a key change

1. Play the song and pause at the moment the key changes.
2. Click **Add at current position**.
3. Choose the new key from the dropdown in the table row that appears.

To remove a key change, click the delete button on that row.

You can also add key changes quickly from the **Timing** tab by using the **+ Key change at playhead** button in the key strip at the top of the beat grid.

---

## Chords

Chord markers show which chord is being played at any given moment in the song. Animations can use this information to display chord names, highlight piano keys, or change visual effects in time with the harmony.

### Adding a chord

1. Play the song and pause at the moment the chord changes.
2. Open the **Chords** sub-tab and click **Add at current position**.
3. Type the chord name in the text field (for example, `Am`, `C/E`, or `G7`).

The table shows each chord alongside its beat position and the corresponding time in the song. To delete a chord, click the trash button on that row.

---

## Time Signatures

The time signature tells you how beats are grouped into measures. Most popular music uses 4/4 (four beats per measure). Waltzes use 3/4. Some songs change time signature during an instrumental section or a bridge.

If the whole song is in 4/4 (the default), you do not need to add anything here.

### Adding a time signature change

1. Seek to the point in the song where the time signature changes.
2. Click **Add change at current position**.
3. Use the dropdowns in the new row to set the numerator (the top number) and the denominator (the bottom number).

To remove a time signature change, click the delete button on that row.
