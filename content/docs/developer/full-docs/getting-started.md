---
sidebar_position: 2
title: "Getting Started"
---

# Getting Started

This guide walks you through writing and running your first animation in the Code Playground.

## Prerequisites

The Code Playground is only visible when developer mode is enabled. Turn it on in your account preferences before continuing.

## Opening the Code Playground

Navigate to **Playground** in the top bar. The Playground has three mode tabs: **Song**, **Anim**, and **Code**. Select **Code**.

## The editor tabs

The Code editor has four tabs:

| Tab | Purpose |
|---|---|
| **ES Module** | Your JavaScript — must export a `main(G)` function as the default export |
| **CSS** | Styles scoped to your module |
| **HTML** | Markup that your JavaScript can query via `G.getElementById` |
| **Preview** | Runs your code alongside the selected song |

## Selecting a song and running

1. Switch to the **Song** tab in the Playground to pick a song. Any song on the platform works.
2. Return to the **Code** tab and write your module.
3. Click the **Preview** tab (or navigate to it). Your code runs immediately.

If no song has been selected, the player will be empty and music events will not fire until you select one.

## Your first module

Here is a minimal working example. It listens for the `G.TYPE.BEAT` event and flashes the background color on every beat:

**ES Module tab:**

```javascript
export default function main(G) {
  G.on(G.TYPE.INIT, () => {
    const box = G.getElementById("box");
    box.style.transition = "background 100ms";
  });

  G.on(G.TYPE.BEAT, () => {
    const box = G.getElementById("box");
    box.style.background = "#ff4444";
    setTimeout(() => {
      box.style.background = "#111";
    }, 80);
  });
}
```

**HTML tab:**

```html
<div id="box"></div>
```

**CSS tab:**

```css
#box {
  width: 100%;
  height: 100%;
  background: #111;
}
```

Click Preview and start playback. The box flashes on every beat.

## Subscribing to more events

You can register as many handlers as you like. They are all called each time the event fires:

```javascript
export default function main(G) {
  G.on(G.TYPE.PLAY, () => console.log("playing"));
  G.on(G.TYPE.PAUSE, () => console.log("paused"));

  G.on(G.TYPE.SYL, (syl) => {
    // syl contains data about the current syllable
    console.log(syl);
  });
}
```

See [Event-Based System](./event-based-system) for the full list of event types and their payloads.

## How errors are displayed

If your module throws an error during initialization or inside a handler, the error message and stack trace appear directly in the preview area. The same information is logged to the browser's developer console.

Open DevTools (`F12` or `Ctrl+Shift+I`) to see all console output from your module, including anything you log with `console.log`.

## Importing external libraries

You can import any library hosted on **jsDelivr** or **esm.sh**:

```javascript
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";

export default function main(G) {
  G.on(G.TYPE.TICK, (time) => {
    // use d3 here
  });
}
```

Imports from other origins are blocked by the platform's Content Security Policy.

## Saving your work

Use the **Save Draft** button in the Code Playground toolbar to save your work as a named draft. From there you can continue editing in the full code editor or prepare it for publishing as an animation.

## Next steps

- Read [Event-Based System](./event-based-system) to see all available events and their payloads
- Read [Animation Configuration](./animation-config) to expose user-adjustable parameters in your animation
- Read [Module Collections](./module-collection) to combine multiple modules into one layout
- Read [G Object Reference](./g-object-reference) for the complete API surface
