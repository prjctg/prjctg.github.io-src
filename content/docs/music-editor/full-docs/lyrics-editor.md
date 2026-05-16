---
sidebar_position: 5
---

# Lyrics Editor

The lyrics editor lets you add, import, and time-align lyrics. Accurate lyric timing enables animations to react to individual lines, words, and syllables in sync with the music.

---

## Lyrics Tab

The **Lyrics** tab is where you manage lyric content — the text itself, without worrying about timing yet.

### Adding Lyrics Manually

Type or paste lyric lines into the editor. Each line becomes one lyric event in the timeline. You can have multiple lyric streams for different languages or vocal parts (e.g., original language + romanization + translation).

### Managing Lyric Streams

Each stream has a language code and can be independently toggled. A stream marked as **skipped** is stored but not shown to animations by default.

### Transliteration Support

For languages that benefit from phonetic romanization (e.g., Chinese → Pinyin, Japanese → Romaji), the editor can auto-generate a transliteration stream. This creates a parallel set of lyric events that animations can display alongside the original.

---

## LRC Import

If you have an LRC file — a lyrics file with `[mm:ss.ss]` timestamps — you can import it directly. The timestamps in an LRC file are absolute times (seconds into the song), independent of any BPM.

To import:
1. Open the **Lyrics** tab for the target stream.
2. Paste the LRC content or use the import button.
3. The importer parses each `[mm:ss.ss] lyric text` line and creates a lyric event anchored to that exact timestamp.

Imported LRC events are stored as **absolute-time events** — they are pinned to seconds, not beat numbers. This means they will not shift if you later change the BPM. Once you have finalized the BPM, use the **Bake to Beats** button in the beat grid toolbar to convert them to beat-relative events. See [Beat Grid](./beat-grid#beat-relative-vs-absolute-time-events) for details.

---

## Align Tab

The **Align** tab is where you set and refine the timing of each lyric line — placing them precisely on the audio timeline.

### How to Align

1. Start playback.
2. When a lyric line begins, click the line (or press the assigned hotkey) to stamp it with the current playback time.
3. Repeat for each line in sequence.
4. After a first pass, use the waveform or beat grid view to fine-tune individual line positions.

---

## Syllable Splitting

Lyrics are initially aligned at the **line** level. For animations that react to individual syllables (e.g., karaoke-style highlighting), you need to split each word into syllables.

### Using the Syllable Splitter

Click on a word in the lyrics view to open the syllable split popover. The popover shows the word with suggested split points. Click between letters to add or remove split points, then confirm. The word is saved as an ordered list of syllable segments with their own timing events.

### Auto-Split

For supported languages, the editor can auto-suggest syllable boundaries. Review and adjust the suggestions before confirming — auto-split is a starting point, not guaranteed to be correct.

---

## Event Hierarchy

Lyric events in the timeline have a four-level hierarchy. Animations can subscribe to whichever level(s) they need:

| Level | Event type | Description |
|---|---|---|
| Line | `LINE` / `LINE_` | Start and end of a lyric line |
| Segment | `SEGMENT` | A portion of a line sung by one person or voice |
| Word | `WORD` / `WORD_` | Start and end of a word |
| Syllable | `SYL` / `SYL_` | Start and end of a syllable |

The `_` suffix events (e.g., `LINE_`, `SYL_`) fire at the **end** of that unit, just before the next one begins. Animations use these to trigger exit effects (fading out a highlighted syllable, sliding out a line, etc.).

---

## Multi-Language Support

A song can have multiple lyric streams, each with its own language code. Animations that use an `mchannel` config parameter let the user choose which stream to display. This means you can add lyrics in multiple languages and each user can pick their preferred one — all without any animation code changes.
