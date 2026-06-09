---
sidebar_position: 1
title: "Developer Guide"
---

# Developer Guide

This guide is for JavaScript developers who want to build music-reactive content on the Animr platform — whether that means karaoke displays, instrument guides, rhythm games, or abstract visualizers.

## What you can build

Animr gives your code a live feed of music events: beats, measures, lyrics, chords, notes, and more. You react to those events with JavaScript, CSS, and HTML to produce whatever you want on screen.

Typical uses include:

- **Karaoke and lyric displays** — highlight syllables, words, or lines in sync with vocals
- **Instrument guides** — show chord shapes or tablature tied to the chord events in a song
- **Rhythm games** — spawn targets on beats, score hits using custom events between modules
- **Visualizers and generative art** — react to beat and tick events to drive canvas animations

## Two entry points

### Code Playground

The fastest way to experiment. Navigate to **Playground > Code** in the app. Write JavaScript in the ES Module tab, add CSS and HTML if needed, pick a song, and click Preview. No account publishing required — your code runs immediately in the browser alongside the selected song.

The Playground is gated to developer mode. Enable developer mode in your account preferences first.

### Anim Designer + IDE

The full workflow for publishable animations. Use the **Anim Designer** to visually arrange a Module Collection — define the layout, assign modules to slots, nest sub-collections. Each module's code lives in the code editor (IDE) attached to that module. When you publish, the animation becomes available to all users of the platform.

## Next steps

Head to the [Full Developer Documentation](./full-docs) for concepts, the complete event reference, config parameter docs, and the G object API reference.
