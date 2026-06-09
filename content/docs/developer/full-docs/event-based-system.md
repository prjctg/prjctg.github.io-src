---
sidebar_position: 3
title: "Event-Based System"
---

# Event-Based System

Animr synchronizes your code with music through an event system. Instead of polling for the current beat or time, you register handlers and the platform calls them at precisely the right moment.

## Subscribing to events

```javascript
G.on(eventType, handler)
G.on(eventType, options, handler)
```

- `eventType` — a value from `G.TYPE` for built-in events, or any string for custom events
- `options` — an optional object with filtering and offset parameters (see below)
- `handler` — a function that receives the event data payload

You can register multiple handlers for the same event type. All handlers are called in registration order.

```javascript
export default function main(G) {
  G.on(G.TYPE.BEAT, (data) => {
    // fires on every beat
  });

  G.on(G.TYPE.SYL, { channel: 0 }, (syl) => {
    // fires for every syllable on lyric channel 0
  });
}
```

### Options for lyric and note events

For events that carry lyric or note data (SLINE, LINE, SEGMENT, WORD, SYL, NOTE), `G.on` accepts an options object as the second argument:

| Option | Type | Description |
|---|---|---|
| `channel` | number | Lyric channel index (selects which lyric stream to follow) |
| `stream` | number | Sub-stream index within a channel |
| `offset` | number | Time offset in milliseconds — receive the event this many ms early (positive) or late (negative) |

Example with offset (receive syllable events 300 ms before they occur):

```javascript
G.on(G.TYPE.SYL, { channel: 0, offset: -300 }, (syl) => {
  // prepare syl.syl text in advance
});
```

## G.TYPE — built-in event type constants

Always use the named constant; never use the raw numeric value.

### Playback events

These fire in response to player state changes and the animation frame loop.

| Constant | When it fires |
|---|---|
| `G.TYPE.INIT` | When the animation is loaded or reloaded. Read `G.conf` here. |
| `G.TYPE.UNINIT` | When the animation is unloaded. Release resources here if needed. |
| `G.TYPE.PLAY` | When playback starts. |
| `G.TYPE.PAUSE` | When playback is paused. |
| `G.TYPE.SEEK` | When the player seeks to a new position. |
| `G.TYPE.TICK` | Every animation frame while playback is active. Handler receives `(currentTimeMs, deltaMs)`. |
| `G.TYPE.RESIZE` | When the module's container is resized. Handler receives a `ResizeObserverEntry` array. |

### Music structure events

These fire at structural points in the song. Each event carries metadata from the song data.

| Constant | When it fires |
|---|---|
| `G.TYPE.BEAT` | At each beat of the music. |
| `G.TYPE.MEASURE` | At the start of each measure (the first beat of the measure). |
| `G.TYPE.TIMESIG` | At the start of the song or when the time signature changes. |
| `G.TYPE.KEY` | At the start of the song or when the musical key changes. |
| `G.TYPE.CHORD` | When a chord change occurs. |
| `G.TYPE.SECTION` | When a named song section begins (verse, chorus, bridge, etc.), if the song has section data. |

### Lyric events

These fire in hierarchical order from the largest lyric unit down to individual syllables.

| Constant | When it fires |
|---|---|
| `G.TYPE.SLINE` | At the start of a lyric section-line (a line grouped under a section). |
| `G.TYPE.LINE` | At the start of each line of lyrics. |
| `G.TYPE.SEGMENT` | At the start of a segment within a line (a continuous run sung by one person or voice). |
| `G.TYPE.WORD` | At the start of each word. |
| `G.TYPE.SYL` | At the start of each syllable. This is the finest-grained lyric event. |

### Note events

| Constant | When it fires |
|---|---|
| `G.TYPE.NOTE` | When a musical note begins. |

### Deprecated event types

The following constants exist in `G.TYPE` but are deprecated and will be removed in a future release:

| Deprecated constant | Replacement |
|---|---|
| `G.TYPE.WORD_` | Use `G.TYPE.WORD` with `{ includeDash: true }` |
| `G.TYPE.SYL_` | Use `G.TYPE.SYL` with `{ includeDash: true }` |

When you subscribe to a deprecated type, the platform logs a warning to the console.

## Custom events

Modules in the same collection can communicate by emitting and subscribing to custom events.

### Emitting a custom event

```javascript
G.emit(eventType, data)
```

`eventType` must be a plain string (not a `G.TYPE.*` constant). Use camelCase by convention. All modules in the same collection that have subscribed to that string will receive the call synchronously.

```javascript
// In a "game logic" module:
G.on(G.TYPE.BEAT, () => {
  G.emit("beatMissed", { streak: 0 });
});
```

### Receiving a custom event

```javascript
// In a "score display" module in the same collection:
G.on("beatMissed", (data) => {
  console.log("streak reset to", data.streak);
});
```

Built-in `G.TYPE.*` events cannot be emitted via `G.emit` — that method is for custom inter-module communication only.

## Event data payloads

Payloads are frozen objects. The exact shape depends on the event and the song data. Common fields include:

- **BEAT** — beat index and start time
- **MEASURE** — measure index and start time
- **TIMESIG** — numerator and denominator of the time signature
- **KEY** — key and mode information
- **CHORD** — chord name and structure
- **SECTION** — section name and boundaries
- **LINE / SLINE** — line text and timing boundaries
- **SEGMENT** — segment text, segment ID, line ID
- **WORD** — word text (`d` field), word ID, timing
- **SYL** — syllable text (`syl` field), syllable ID, word ID, timing
- **NOTE** — note pitch, duration, and timing
- **TICK** — `(currentTimeMs, deltaMs)` as positional arguments (not an object)
- **RESIZE** — `ResizeObserverEntry[]` from the ResizeObserver callback

Use `console.log` in your handler to inspect the full payload for a given song.
