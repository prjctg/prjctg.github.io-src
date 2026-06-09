---
sidebar_position: 2
title: "Song Info"
---

# Song Info

The **Info** tab is the first tab you see when you open a song for editing. It holds the basic facts about the song: its title, who performed it, where to find the audio or video, and its musical properties.

---

## Title

Type the song's full title as it is commonly known. This field is required — you cannot save a song without a title.

---

## Artists

Type the name of the artist or artists. For multiple artists, separate their names with commas or use the style common for that song (e.g., "Artist A feat. Artist B").

---

## Tempo (BPM)

BPM stands for beats per minute — it describes how fast the song moves. Setting an accurate BPM is important because the beat grid and all timing events depend on it.

You can type the BPM directly or use the tap detector built into this field. For songs that change speed mid-way through, you can define multiple BPM regions.

See [Tempo Editor](./tempo-editor) for a full guide.

---

## Song URL

Enter the URL of the song's audio or video. Supported sources are YouTube, Vimeo, Dailymotion, and SoundCloud.

You can add more than one URL — for example, a YouTube version and a SoundCloud version — so the player can fall back if one source is unavailable.

### Offset

Each URL has an **Offset** field (in milliseconds). Use this when the audio or video has silence or an intro before the song actually starts, and you want to shift playback so that beat 1 lines up with the music. A positive offset delays the start of playback; a negative offset starts it earlier.

---

## Key

Select the musical key of the song from the dropdown. The available options cover all twelve pitches in both sharp and flat notation (for example, A, A#/Bb, B, C, and so on).

The key you set here is used as the default for the whole song. If the song changes key mid-way through, you can mark those changes in the [Details tab](./musical-data).

---

## Duration

The Duration field fills in automatically when a song URL has been loaded and the player reads the track length. It is read-only — you cannot type into it directly. If it shows blank, make sure a valid song URL is entered and the player has finished loading.

---

## Unlisted

Check the **Unlisted** checkbox to hide the song from public search results and browse pages. Unlisted songs are still accessible by direct link. Use this while the song data is incomplete or still being worked on.
