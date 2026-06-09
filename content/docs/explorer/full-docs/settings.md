---
sidebar_position: 4
title: "Preferences and Settings"
---

# Preferences and Settings

Open **Settings** from the navigation (the gear icon) to reach the Preferences page. Your preferences are saved on this device and apply whether or not you are signed in.

---

## Lyric Channel

These options affect how lyrics are displayed in the animation.

### Show Pronunciation Guide

When enabled, animations that support it will show a pronunciation guide alongside the lyrics. Useful for songs in languages you are learning.

### Prefer Romanisation

When enabled, romanised text (a Latin-alphabet representation of the lyrics) is shown instead of or alongside the original script, where available.

---

## Appearance

### Motion preference

Controls how much animation motion is shown. This is useful if you prefer less movement on screen or have a motion sensitivity.

| Option | What it does |
|---|---|
| **Follow system setting** | Respects your device's accessibility setting for reduced motion |
| **Always reduce motion** | Reduces animation movement regardless of your system setting |
| **Always show full motion** | Shows all animation motion regardless of your system setting |

---

## Playback

### General player offset

A fine-tuning slider that shifts when the animation events fire relative to the audio. If animations feel slightly early or late compared to the music, adjust this slider until they feel in sync. The default value of 0 works for most people.

### Record tap offset

A separate offset used during the song timing tools (not relevant for pure Explorer use). You can leave this at 0.

### Keep player controls visible

When enabled, the control bar stays on screen at all times during playback instead of fading out after a few seconds of inactivity. Handy if you switch songs or animations frequently.

### Show skip intro button

When enabled, a **Skip Intro** button appears at the start of a song if there is a notable gap before the content begins. Click it to jump straight to the first section. Disable this if you prefer to always hear the full intro.

### Show timing predictions

When enabled, a visual hint appears in the player indicating predicted timing. This is primarily useful when checking song timing data.

---

## Filler Events

These settings affect what happens when an animation is designed around musical events (like syllables, notes, or chords) but the current song does not have that data.

### Filler syllables

When enabled, placeholder syllables are generated automatically so that syllable-based animations still fire even for songs with no lyric data. Without this, those animations would show nothing.

### Syllable text

The text shown for each filler syllable. Options include **la** (default), **da**, **\*** (asterisk), a blank space, or **Random** (cycles through la, da, ba, na at random).

### Note pitch style

The pitch assigned to generated notes when a song has no pitch data.

| Option | What it does |
|---|---|
| **Fixed (C4)** | All filler notes use the same pitch |
| **Pentatonic random (C D E G A)** | Notes are chosen at random from a pentatonic scale |
| **Ascending scale** | Notes step up a scale as the song progresses |

### Filler chords

When enabled, a simple chord progression is generated for songs that have no chord data, so chord-responsive animations still have something to work with.

---

## Developer

These settings are for animation developers and advanced users.

- **Enable mobile debug console** — opens a developer console overlay on mobile devices, useful for debugging animations.
- **Developer mode** — unlocks additional navigation items and features intended for animation development.
- **Show FPS** — displays a frames-per-second counter on the animation viewer.

If you are just watching content, you can safely ignore this section.

---

## Storage

At the bottom of the Preferences page is a **Storage** section showing how many documents are cached locally on your device. Caching makes pages load faster on repeat visits.

Click **Clear local cache** to remove all cached documents. This does not delete any of your saved drafts or account data — only the downloaded content used for faster loading. After clearing, content will reload from the server on your next visit.
