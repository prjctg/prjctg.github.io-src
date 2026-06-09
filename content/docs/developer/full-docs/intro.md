---
sidebar_position: 1
title: "Concepts Overview"
---

# Concepts Overview

Before writing your first animation it helps to understand the three building blocks of the Animr developer platform: **Modules**, **Module Collections**, and the **G object**.

## Modules

A module is the smallest development unit. It consists of three parts:

- **JavaScript** — written as an ES Module. Your module's default export is a function that receives a `G` object as its first argument. All event subscriptions, DOM access, and inter-module communication go through `G`.
- **CSS** — styles scoped to this module. They do not affect other modules and cannot be affected by them.
- **HTML** — the markup structure for this module's content.

A minimal module looks like this:

```javascript
export default function main(G) {
  G.on(G.TYPE.BEAT, (data) => {
    // react to each beat
  });
}
```

Modules are self-contained. Each module's CSS and HTML are encapsulated — elements from one module are not accessible by another.

## Module Collections

A **module collection** is a grouping of one or more modules (or other nested collections) that share a layout and an event bus.

Collections define how their child modules are visually arranged. The HTML and CSS of the collection provides the layout; each module is slotted into a named element in that layout.

Because all modules in a collection share the same event bus, a module can broadcast a custom event via `G.emit` and any sibling module can receive it via `G.on`. This is the only sanctioned channel for inter-module communication — you cannot reach into another module's DOM or JavaScript scope.

See [Module Collections](./module-collection) for full details.

## The G Object

`G` is the interface between your module and the platform. It is passed as the first argument to your exported `main` function and is available inside any closure that captures it.

`G` provides:

- `G.on(eventType, handler)` — subscribe to platform events or custom events
- `G.emit(eventType, data)` — broadcast a custom event to sibling modules
- `G.getElementById(id)` — access DOM elements within your module's HTML scope
- `G.TYPE` — the object of all built-in event type constants
- `G.conf` — the current values of the animation's user-configurable parameters

See the [G Object Reference](./g-object-reference) for the complete API.

## Animation lifecycle

1. **INIT** — `G.TYPE.INIT` fires when the animation is loaded or reloaded. Read `G.conf` here to pick up config values.
2. **Playback events** — as the song plays, the platform fires events (BEAT, MEASURE, SYL, CHORD, etc.) matched to the music timeline. Your handlers receive a data payload for each event.
3. **TICK** — fires every animation frame while playback is active. Use this for smooth per-frame updates.
4. **PLAY / PAUSE / SEEK / RESIZE** — fire in response to player control actions and viewport changes.
5. **UNINIT** — fires when the animation is unloaded. Use this to release resources if needed.

## The event-based architecture

All synchronization with music happens through the event system. You do not poll for the current time or beat — you register handlers and the platform calls them at the right moment.

See [Event-Based System](./event-based-system) for the complete list of event types, their payloads, and how to emit and receive custom events.

## Allowable external libraries

You can import any library from **jsDelivr** (`https://cdn.jsdelivr.net/npm/`) or **esm.sh** (`https://esm.sh/`). Imports from other origins are blocked by the platform's Content Security Policy.

```javascript
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";
import confetti from "https://esm.sh/canvas-confetti@1";
```
