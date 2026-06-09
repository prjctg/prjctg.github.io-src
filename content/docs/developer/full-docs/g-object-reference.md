---
sidebar_position: 6
title: "G Object Reference"
---

# G Object Reference

The `G` object is passed as the first argument to your module's default export function. It is your module's interface to the platform — for event handling, DOM access, config values, and communication with sibling modules.

```javascript
export default function main(G) {
  // G is available here and in all closures that capture it
}
```

---

## G.on(eventType, handler)
## G.on(eventType, options, handler)

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

**Options object** (applicable to lyric and note events):

| Option | Type | Description |
|---|---|---|
| `channel` | number | Lyric channel index |
| `stream` | number | Sub-stream index within a channel |
| `offset` | number | Time offset in milliseconds (negative = receive event early) |

You can register multiple handlers for the same event type. All handlers are called in registration order.

`G.on` must be called during module initialization (inside your `main` function, before `G.TYPE.INIT` fires, or inside the `G.TYPE.INIT` handler). Calling it outside of initialization context throws an error.

---

## G.emit(eventType, data)

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

## G.getElementById(id)

Returns the DOM element with the given `id` from within this module's HTML scope. Because each module's HTML is encapsulated in a shadow root, `document.getElementById` will not find elements belonging to other modules. Always use `G.getElementById` to access your own elements.

```javascript
G.on(G.TYPE.INIT, () => {
  const canvas = G.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");
});
```

Returns `null` if no element with that `id` exists in this module's HTML.

---

## G.TYPE

A frozen object containing all built-in event type constants. Always reference events by constant name, not by raw value.

```javascript
G.TYPE.PLAY
G.TYPE.PAUSE
G.TYPE.BEAT
G.TYPE.MEASURE
G.TYPE.TIMESIG
G.TYPE.KEY
G.TYPE.CHORD
G.TYPE.SECTION
G.TYPE.SLINE
G.TYPE.LINE
G.TYPE.SEGMENT
G.TYPE.WORD
G.TYPE.SYL
G.TYPE.NOTE
G.TYPE.TICK
G.TYPE.SEEK
G.TYPE.INIT
G.TYPE.UNINIT
G.TYPE.RESIZE
```

See [Event-Based System](./event-based-system) for descriptions, payloads, and the complete list including deprecated constants.

---

## G.conf

A read-only object containing the current values of all configurable parameters defined for this animation. Keys match the `i` field of each config item.

```javascript
G.on(G.TYPE.INIT, () => {
  const speed = G.conf.speed;           // number (int type)
  const channel = G.conf.lyricsChannel; // number (mchannel type)
  const showText = G.conf.showText;     // boolean (check type)
  const label = G.conf.customLabel;     // string (text type)
});
```

Config values are set by the user through the animation settings panel. Read `G.conf` inside your `G.TYPE.INIT` handler — that handler fires each time the animation is initialized or reinitialized (including after config changes).

`G.conf` is read-only. Writing to it has no effect.

See [Animation Configuration](./animation-config) for how to define parameters and which types are available.

---

## Encapsulation

Each module runs in an isolated shadow DOM environment:

- **CSS** defined in your module does not affect other modules, and other modules' CSS does not affect yours.
- **HTML elements** are scoped to your module. Use `G.getElementById`, not `document.getElementById`.
- **JavaScript** — closures and module-level variables are private to your module instance. Other modules cannot read or write them.

When modules are combined into a collection, the only cross-module communication channel is the shared event bus: `G.emit` to broadcast, `G.on` with a string event type to receive. See [Module Collections](./module-collection) for details.

---

## External libraries

Modules can import from **jsDelivr** or **esm.sh**. Imports from other origins are blocked by the platform's Content Security Policy.

```javascript
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";
import anime from "https://cdn.jsdelivr.net/npm/animejs@3/+esm";
import confetti from "https://esm.sh/canvas-confetti@1";

export default function main(G) {
  G.on(G.TYPE.BEAT, () => {
    // use d3, anime, confetti, etc.
  });
}
```
