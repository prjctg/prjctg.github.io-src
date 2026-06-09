---
sidebar_position: 4
title: "Module Collections"
---

# Module Collections

A **module collection** is a grouping of one or more modules — or other nested collections — that share a visual layout and a common event bus. Collections are how you build multi-module animations.

## What a collection provides

- **Layout** — the collection's HTML and CSS define how child modules are positioned relative to each other
- **Slot assignment** — each child module is mapped to a named element in the layout HTML
- **Shared event bus** — modules in the same collection can communicate by emitting and subscribing to custom events via `G.emit` and `G.on`

## Default layout

If you define a collection without custom HTML, the platform generates a default layout:

- Each module gets a container `<div>` whose `id` is derived from the module's position in the list
- All containers are stacked on top of each other using absolute positioning and fill the parent 100%

This default is useful for layered effects where modules share the same space (e.g. a background visualizer behind a foreground lyric display).

## Custom layout

You can provide your own HTML and CSS for the collection. The HTML defines the structure; each child module is rendered into a named slot element. The CSS controls sizing, position, grid layout, or any other arrangement.

Example: a two-column layout where one module shows lyrics and another shows a visualizer:

```html
<!-- collection HTML -->
<div id="lyrics-slot"></div>
<div id="visualizer-slot"></div>
```

```css
/* collection CSS */
:host {
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100%;
}
#lyrics-slot, #visualizer-slot {
  height: 100%;
}
```

Each child module is then assigned to one of those slot IDs in the Anim Designer.

## Nesting collections

A collection can contain other collections as children. Nested collections follow the same rules: they define their own layout, and their modules share their own inner event bus. Events emitted inside a nested collection do not automatically propagate out to the parent collection's bus.

## Inter-module communication

The only way for modules to communicate is through the collection's event bus:

```javascript
// Module A: emit a custom event
G.emit("scoreChanged", { score: 42 });

// Module B (in the same collection): receive it
G.on("scoreChanged", ({ score }) => {
  G.getElementById("score-display").textContent = score;
});
```

You cannot access another module's DOM elements or JavaScript variables. Encapsulation is enforced — `document.getElementById` will not find elements that belong to a different module. Use `G.getElementById` to access elements within your own module's HTML scope.

## Building collections visually

The **Anim Designer** (Playground > Anim) is the non-code interface for assembling collections. It lets you:

- Add and remove modules
- Assign modules to layout slots
- Define the collection's HTML and CSS layout
- Nest sub-collections
- Preview the result alongside a song

Each module in the designer has its own code editor where you write its JavaScript, CSS, and HTML.
