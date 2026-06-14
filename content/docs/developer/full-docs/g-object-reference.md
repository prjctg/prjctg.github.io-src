---
sidebar_position: 6
title: "G Object Reference"
---

# G Object Reference

The `G` object is passed as the first argument to your module's default export function. It is your module's interface to the platform — for event handling, DOM access, data queries, and rendering utilities.

```javascript
export default function main(G, root, config) {
  // G      — the platform API object (this reference)
  // root   — the module's shadow root (HTMLShadowRoot)
  // config — read-only animation config values set by the user
}
```

`config` holds the current values of all configurable parameters defined for this animation. Keys match the `i` field of each config item (e.g. `config.speed`, `config.lyricsChannel`). It is read-only — writing to it has no effect. Read it inside your `G.TYPE.INIT` handler since that fires each time the animation is initialized or reinitialized after a config change.

See [Animation Configuration](./animation-config) for how to define parameters and which types are available.

---

## Event Subscriptions

### G.on(eventType, handler)
### G.on(eventType, options, handler)

Subscribe to an event. The handler is called each time the event fires.

```javascript
G.on(G.TYPE.BEAT, (data) => {
  // called on every beat
});

G.on(G.TYPE.SYL, { channel: 0, offset: -300 }, (syl) => {
  // called for each syllable on channel 0, 300 ms in advance
});
```

**Parameters:**

| Parameter | Type | Description |
|---|---|---|
| `eventType` | `G.TYPE.*` or string | A built-in event type constant or a plain string for custom events |
| `options` | object (optional) | Filtering and timing options (see below) |
| `handler` | function | Called with the event data payload each time the event fires |

**Options:**

| Option | Type | Applies to | Description |
|---|---|---|---|
| `channel` | number | lyric & note events | Lyric channel index |
| `stream` | number | lyric & note events | Sub-stream index within a channel |
| `offset` | number | lyric & note events | Time offset in ms (negative = receive event early) |
| `includeDash` | boolean | WORD, SYL | Include dash/punctuation separators (excluded by default) |
| `secId` | number | LINE, SLINE | Filter by section ID |
| `lineId` | number | SEGMENT, WORD, SYL | Filter to elements belonging to this line |
| `slineId` | number | SEGMENT, WORD, SYL | Filter to elements belonging to this stream-line |
| `segmentId` | number | WORD, SYL | Filter to elements belonging to this segment |
| `wordId` | number | SYL | Filter to syllables belonging to this word |
| `notes` | boolean | MEASURE | Attach a `notes` array to each measure event object |
| `syls` | boolean | NOTE | Attach syllable info to each note event object |
| `batchEvents` | boolean | any | Collect events sharing the same timestamp into an array and call handler once with the array |
| `jitter` | number | iterator only | Random time jitter (ms) applied to recycled items when the iterator wraps around |
| `prevSylLimit` | boolean | LINE, SLINE, SEGMENT | Clamp early-fire so the event cannot fire before the previous line's last syllable starts. See [Early-Fire Clamping](#early-fire-clamping). |
| `prevSylRatio` | number 0–1 (default `0.3`) | LINE, SLINE, SEGMENT | Fraction of the gap between the previous line's last-syllable start and the current line's nominal start available as early-fire headroom |
| `prevSylOffset` | number ms (default `0`) | LINE, SLINE, SEGMENT | Additional ms shift applied after clamping (positive = push later, negative = push earlier) |
| `parentLimit` | boolean | WORD, SYL | Clamp early-fire so the event cannot precede the resolved start of its parent LINE event. Requires `parentId`. |
| `parentId` | number | WORD, SYL | Zero-based index of the LINE subscription within the same `G.on` call whose resolved start is used as the floor for `parentLimit` |

You can register multiple handlers for the same event type. All handlers are called in registration order.

`G.on` must be called during module initialization (inside your `main` function, before `G.TYPE.INIT` fires, or inside the `G.TYPE.INIT` handler). Calling it outside of initialization context throws an error.

#### Early-Fire Clamping

Lyric modules often fire LINE events early (via a negative `offset`) so the UI can animate an incoming line before it starts singing. Without clamping, a large offset can make the new line fire while the previous line's last syllable is still active, causing visual overlap.

**`prevSylLimit` + `prevSylRatio` + `prevSylOffset`** — apply to LINE, SLINE, and SEGMENT subscriptions. When `prevSylLimit: true`, the resolved start is clamped to:

```
clampedStart = prevSylStart + prevSylRatio × (nominalStart − prevSylStart) + prevSylOffset
```

where `prevSylStart` is the *start time* of the last syllable of the previous line. `prevSylRatio` controls how much of the gap can be used as headroom (0 = fire right as the previous syllable begins; 1 = fire at the current line's nominal start; default 0.3). The result is pinned to at least `prevSylStart + 1 ms`.

**`parentLimit` + `parentId`** — apply to WORD and SYL subscriptions. When `parentLimit: true`, the event's resolved start is clamped to be no earlier than its parent LINE event's resolved start. `parentId` is the zero-based index of that LINE subscription within the same `G.on` call.

```javascript
// Line fires up to 1 s early, but never before the previous line's last syllable
G.on(G.TYPE.LINE, { offset: -1000, prevSylLimit: true, prevSylRatio: 0.3 }, (line) => { … });

// Word fires up to 1.5 s early, but never before its parent LINE fires (subscription 0)
G.on(G.TYPE.LINE, { offset: 0 },                                        (line) => { … });
G.on(G.TYPE.WORD, { offset: -1500, parentLimit: true, parentId: 0 },    (word) => { … });
```

---

### G.off(eventType, options, handler)

Register a handler that fires when an event **ends** (the negative / off transition). Mirrors `G.on` in signature and options.

```javascript
G.off(G.TYPE.SYL, { channel: 0 }, (syl) => {
  // called when each syllable ends on channel 0
});
```

The `G.TYPE.*` system events (TICK, PLAY, PAUSE, SEEK, INIT, UNINIT, RESIZE) cannot be used with `G.off` — it has no effect on them.

---

## Data Access

These methods query the full event data array at initialization time. Call them inside your `G.TYPE.INIT` handler (or the body of `main`) to read and pre-process event objects before playback begins.

### G.forEach(type, options, callback)

Iterate over every matching event object.

```javascript
G.on(G.TYPE.INIT, () => {
  G.forEach(G.TYPE.WORD, { channel: 0 }, (word) => {
    console.log(word.d); // word text
  });
});
```

Accepts the same `options` as `G.on`.

---

### G.map(type, options, callback)

Map over every matching event object and return a new array.

```javascript
G.on(G.TYPE.INIT, () => {
  const labels = G.map(G.TYPE.SYL, { channel: 0 }, (syl) => syl.d);
});
```

If `callback` is omitted, returns the raw event objects.

---

### G.iterator(type, options, mapper?)

Returns an iterator that yields one event object per call, advancing sequentially through the data. Designed for staggered-reveal patterns where each new event activates a new element.

```javascript
G.on(G.TYPE.INIT, () => {
  const iter = G.iterator(G.TYPE.WORD, { channel: 0 });
});

G.on(G.TYPE.WORD, { channel: 0 }, () => {
  const { value, done } = iter.next();
  // value — the next word object; done — true when array is exhausted
});
```

When exhausted, subsequent calls recycle a random item (with optional `jitter` applied to its timing) so the display never goes blank.

---

## Event Types

### G.TYPE

A frozen object containing all built-in event type constants. Always reference events by constant name, not by raw value.

| Constant | Description |
|---|---|
| `G.TYPE.TICK` | Fires every animation frame. Handler receives `(timeMs, deltaMs)`. |
| `G.TYPE.INIT` | Fires when the module initializes (and on every reinit after config change). |
| `G.TYPE.UNINIT` | Fires when the module is torn down. |
| `G.TYPE.PLAY` | Fires when playback starts. Handler receives the start time in ms. |
| `G.TYPE.PAUSE` | Fires when playback pauses. |
| `G.TYPE.SEEK` | Fires when the playhead jumps to a new position. |
| `G.TYPE.RESIZE` | Fires when the viewer element is resized. Handler receives `ResizeObserverEntry[]`. |
| `G.TYPE.BEAT` | Fires on each musical beat. |
| `G.TYPE.MEASURE` | Fires on each measure (bar). |
| `G.TYPE.TIMESIG` | Fires when the time signature changes. |
| `G.TYPE.KEY` | Fires when the musical key changes. |
| `G.TYPE.CHORD` | Fires on each chord change. |
| `G.TYPE.SECTION` | Fires at section boundaries (verse, chorus, etc.). |
| `G.TYPE.SLINE` | Fires for each stream-line (a line within a specific lyric stream). |
| `G.TYPE.LINE` | Fires for each lyric line (across all streams). |
| `G.TYPE.SEGMENT` | Fires for each lyric segment within a line. |
| `G.TYPE.WORD` | Fires for each word. Excludes dash/separator words unless `includeDash: true`. |
| `G.TYPE.SYL` | Fires for each syllable. Excludes dash syls unless `includeDash: true`. |
| `G.TYPE.NOTE` | Fires for each pitched note. |

See [Event-Based System](./event-based-system) for full payload shapes.

---

## Time & Playback

### G.currentTime()

Returns the current playback position in milliseconds.

```javascript
G.on(G.TYPE.TICK, (timeMs) => {
  // timeMs and G.currentTime() are equivalent here
  const t = G.currentTime();
});
```

---

### G.toBeat(timeMs)

Converts a millisecond timestamp to a fractional beat number, accounting for tempo changes.

```javascript
const beat = G.toBeat(G.currentTime()); // e.g. 4.75
```

---

### G.toMs(beat)

Converts a beat number back to milliseconds.

```javascript
const timeMs = G.toMs(8); // ms at the start of beat 8
```

---

### G.seek(timeMs)

Seek the player to the given position (milliseconds). Triggers a seek event.

```javascript
G.seek(30000); // jump to 30 seconds
```

---

### G.play()

Trigger playback from the current position.

---

### G.pause()

Pause playback.

---

### G.getPlaybackRate()

Returns the current playback rate multiplier (1.0 = normal speed).

```javascript
const rate = G.getPlaybackRate(); // e.g. 0.75
```

---

### G.setConfig(updates)

Send a partial config update to the platform. The platform merges the update, then reinitializes the animation with the new config. Can only be called after initialization.

```javascript
G.setConfig({ speed: 2 });
```

---

## Song Data

### G.getSongData()

Returns a wrapped, read-only object with song metadata.

```javascript
const song = G.getSongData();
song.title        // string
song.artist       // string
song.duration     // number (ms)
song.beat.bpm     // number — first-region BPM (or constant BPM)
song.streamCount  // number — number of lyric stream groups
```

---

## DOM & Canvas

### G.getElementById(id)

Returns the DOM element with the given `id` from within this module's shadow root. Use this instead of `document.getElementById` — elements are scoped to the shadow DOM and invisible to the global document.

```javascript
G.on(G.TYPE.INIT, () => {
  const canvas = G.getElementById("myCanvas");
});
```

Returns `null` if no element with that `id` exists in this module's HTML.

---

### G.clientRect()

Returns the viewer element's `DOMRect` (position and size in the page).

```javascript
const { width, height } = G.clientRect();
```

---

### G.context2d(width, height, dpi?, opt?)

Creates an off-screen `<canvas>` and returns its 2D context, pre-scaled for the given DPI. If `dpi` is omitted, `devicePixelRatio` is used.

```javascript
G.on(G.TYPE.INIT, () => {
  const ctx = G.context2d(800, 400); // 800×400 CSS pixels
  ctx.fillText("hello", 10, 20);
});
```

The returned context's canvas `width`/`height` attributes reflect the physical pixel size; the context's transform is already scaled so you can draw in CSS pixel coordinates.

---

### G.fit(ctx, initCallback?)

Register a resize handler that scales the given canvas context to fill the viewer on every resize (maintaining the canvas's original aspect ratio). Also runs once immediately.

```javascript
G.on(G.TYPE.INIT, () => {
  const ctx = G.context2d(800, 400);
  G.fit(ctx, (ctx) => {
    // re-draw after resize
  });
});
```

---

### G.measureText(text, font?)

Measure the rendered width of a string. Uses a shared off-screen canvas. `font` defaults to `"12px"`.

```javascript
const metrics = G.measureText("Hello", "bold 24px sans-serif");
console.log(metrics.width);
```

---

### G.svg(tag, attrs?)

Create an SVG element with the correct namespace. Shorthand for `document.createElementNS('http://www.w3.org/2000/svg', tag)`.

```javascript
const circle = G.svg("circle", { cx: 50, cy: 50, r: 20, fill: "red" });
root.querySelector("svg").appendChild(circle);
```

---

## Lyric Utilities

### G.toString(obj)

Convert a lyric event object (syl, word, segment, or line) to its plain text string.

```javascript
G.on(G.TYPE.LINE, { channel: 0 }, (line) => {
  console.log(G.toString(line)); // full line text
});
```

Also accepts an array — joins all results.

---

### G.toChars(obj)

Split a lyric object (or plain string) into an array of Unicode grapheme clusters. Handles complex scripts including Myanmar virama sequences.

```javascript
const chars = G.toChars(syl); // ["h", "e", "l", "l", "o"]
```

Accepts: a syl object, a word object (via its `syls`), a string, or an array of any of the above.

---

### G.wrap(wordArr, targetLines)

Wrap an array of word objects into `targetLines` balanced lines, splitting at natural word boundaries.

```javascript
G.on(G.TYPE.INIT, () => {
  const words = G.map(G.TYPE.WORD, { channel: 0 });
  const lines = G.wrap(words, 2); // [ [word, word, ...], [word, word, ...] ]
});
```

Returns an array of arrays. Each inner array is a line containing word objects.

---

## Math & Animation Utilities

### G.lerp(a, b, t)

Linear interpolation between `a` and `b` at position `t` (0..1).

```javascript
const x = G.lerp(0, 100, 0.25); // 25
```

---

### G.clamp(v, lo, hi)

Clamp `v` to the range `[lo, hi]`.

```javascript
const safe = G.clamp(progress, 0, 1);
```

---

### G.ease(t, type?)

Apply an easing curve to `t` (automatically clamped to 0..1).

| `type` | Curve |
|---|---|
| `'in'` | Quadratic ease-in |
| `'out'` | Quadratic ease-out |
| `'inOut'` | Quadratic ease-in-out (default) |
| `'cubic'` | Cubic ease-in-out |

```javascript
G.on(G.TYPE.TICK, (timeMs) => {
  const t = G.progress(syl, timeMs);
  const eased = G.ease(t, 'out');
  el.style.opacity = eased;
});
```

---

### G.progress(event, timeMs)

Returns a 0..1 progress value for an event object `{ s, e }` at the given time. Returns 0 before the event starts, 1 at or after it ends.

```javascript
G.on(G.TYPE.TICK, (timeMs) => {
  const p = G.progress(currentSyl, timeMs);
});
```

---

## Lookup & Collections

### G.lookup(type, options?)

Like `G.map` but returns a `Map<id, item>` keyed by each item's `id`. Useful for O(1) lookups by ID.

```javascript
G.on(G.TYPE.INIT, () => {
  const wordMap = G.lookup(G.TYPE.WORD, { channel: 0 });
  const word = wordMap.get(someWordId);
});
```

---

### G.shuffle(array)

Fisher-Yates in-place shuffle. Mutates and returns the array.

```javascript
const items = G.map(G.TYPE.WORD, { channel: 0 });
G.shuffle(items);
```

---

### G.randGen(seed?)

Returns a deterministic seeded pseudo-random number generator. Each call to the returned function yields a new number in `[0, 1)`.

```javascript
const rng = G.randGen(42);
const x = rng(); // deterministic random
const y = rng();
```

If `seed` is 0 or omitted, defaults to 1.

---

## Custom Events

### G.emit(eventType, data)

Emit a custom event. All modules in the same collection that have subscribed to `eventType` via `G.on` will receive it synchronously.

```javascript
G.emit("scoreChanged", { score: 10, streak: 3 });
```

**Parameters:**

| Parameter | Type | Description |
|---|---|---|
| `eventType` | string | A plain camelCase string. Must not be a `G.TYPE.*` constant. |
| `data` | any | The payload passed to each subscribed handler |

Built-in `G.TYPE.*` events cannot be emitted via `G.emit`. Use this method for custom inter-module communication only.

---

## Encapsulation

Each module runs in an isolated shadow DOM environment:

- **CSS** defined in your module does not affect other modules, and other modules' CSS does not affect yours.
- **HTML elements** are scoped to your module. Use `G.getElementById`, not `document.getElementById`.
- **JavaScript** — closures and module-level variables are private to your module instance. Other modules cannot read or write them.

When modules are combined into a collection, the only cross-module communication channel is the shared event bus: `G.emit` to broadcast, `G.on` with a string event type to receive. See [Module Collections](./module-collection) for details.

---

## External Libraries

Modules can import from **jsDelivr** or **esm.sh**. Imports from other origins are blocked by the platform's Content Security Policy.

```javascript
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";
import anime from "https://cdn.jsdelivr.net/npm/animejs@3/+esm";
import confetti from "https://esm.sh/canvas-confetti@1";

export default function main(G, root, config) {
  G.on(G.TYPE.BEAT, () => {
    // use d3, anime, confetti, etc.
  });
}
```
