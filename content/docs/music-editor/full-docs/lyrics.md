---
sidebar_position: 3
title: "Lyrics"
---

# Lyrics

The **Lyrics** tab is where you manage the text of a song's lyrics. This is separate from timing — you focus on getting the words right here, and connect them to the music in the [Timing tab](./timing).

---

## Lyric sources

A song can have more than one set of lyrics. Each set is called a **source** and appears as its own tab inside the Lyrics tab (for example, "Lyrics", "Lyrics 1", "Romaji").

Why have multiple sources?

- A song in Japanese might have one source for the original text and another for a Romaji transliteration.
- A K-pop song might have the original Korean, a Romaja romanization, and an English translation.
- A duet where two singers alternate might have separate sources for each voice part.

Animations can choose which source to display, or show several at once.

To add a new source, click the **+ Add** button in the tab strip.

---

## Adding lyrics manually

Select the source tab you want to edit. Type or paste the lyrics into the text area, with one lyric line per line of text.

Use blank lines to separate sections — for example, a blank line between a verse and a chorus. You can also add a section label on its own line using square brackets (for example, `[Chorus]`). Section labels are used in the Details tab to help you organize timing.

---

## Importing from an LRC file

If you have an LRC file — a lyrics file where each line starts with a timestamp like `[01:23.45]` — you can import it directly.

Paste the LRC content into the text area. The editor will detect the format automatically and offer to import it. Confirm the import, and the lyrics along with their timestamps will be loaded.

Imported timestamps are anchored to specific points in time and do not automatically shift if you later change the song's BPM. Once your BPM is finalized, use the **Bake to Beats** option in the Timing tab to lock the imported timestamps to the beat grid. See [Beat Grid](./beat-grid) for details.

---

## Language and transliteration

Each source has a **language** selector. Setting the correct language enables features like auto-syllable detection and automatic transliteration.

To let the editor guess the language from the text, click the translate icon button next to the language selector.

### Automatic transliteration

For Chinese (Mandarin), Korean, and Japanese sources, a button appears below the text area to generate a romanized version automatically:

- **Chinese** → Pinyin
- **Korean** → Romaja
- **Japanese** → Kana / Romaji

The generated transliteration is created as a new source tab so you can review and edit it before saving.

---

## Syllable splitting

By default, lyrics are aligned at the line level. For karaoke-style animations that highlight one syllable at a time, you need to split words into their individual syllables.

You mark syllable boundaries by inserting a pipe character (`|`) between syllables inside a word. For example:

```
Hel|lo wor|ld
```

This tells the editor that "Hello" has two syllables (Hel, lo) and "world" has two syllables (wor, ld).

### Auto-syllable

Click the **Auto-syllable** button to have the editor suggest syllable splits automatically for the current source. The button is only available when the source language is set and supported. Auto-split is a good starting point — review the results and fix any mistakes before saving.

---

## Translation sources

Check the **Translation** checkbox on a source to mark it as a translation rather than a primary lyric source. Translation sources are displayed alongside the main lyrics but are not used for timing or syllable sync. Animations can choose to show or hide translations.

---

## Error checking

If the lyrics contain formatting problems — such as mismatched brackets or unexpected characters — a warning badge appears on the tab. Click the warning button in the tab strip to see the list of errors and jump to the affected lines.
