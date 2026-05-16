---
sidebar_position: 6
---

# G Object Reference

The `G` object is passed as the first argument to your module's default export function. It is your module's interface to the platform — for event handling, DOM access, config values, and communication with other modules.

```javascript
export default function main(G) {
  // G is available here and in all closures that capture it
}
```

---

## G.on(eventType, handler)

Subscribe to an event. The handler is called each time the event fires.

```javascript
G.on(G.TYPE.BEAT, (data) => {
  // called on every beat
});

G.on(G.TYPE.SYL, (data) => {
  // called for each syllable
});
```

`eventType` must be a value from `G.TYPE` (for built-in events) or a string (for custom events). See the [Event-Based System](./event-based-system) for the full list of built-in events and their `data` payloads.

You can register multiple handlers for the same event type. All handlers are called in registration order.

---

## G.emit(eventType, data)

Emit a custom event. All modules in the same collection that have subscribed to `eventType` will receive it.

```javascript
G.emit("score", { points: 10 });
```

`eventType` should be a camelCase string for custom events. Built-in `G.TYPE.*` events cannot be emitted via `G.emit`.

---

## G.getElementById(id)

Returns the DOM element with the given `id` from within **this module's HTML scope only**. Because each module's HTML is encapsulated, `document.getElementById` will not find elements in other modules; use `G.getElementById` instead.

```javascript
G.on(G.TYPE.INIT, () => {
  const canvas = G.getElementById("myCanvas");
  // use canvas normally
});
```

Returns `null` if no element with that `id` exists in this module.

---

## G.TYPE

An object containing all built-in event type constants. Always reference events by name rather than by raw value.

```javascript
G.TYPE.PLAY
G.TYPE.PAUSE
G.TYPE.BEAT
G.TYPE.SYL
// ... etc
```

See the [Event-Based System](./event-based-system) for the complete list and descriptions of each event.

---

## G.conf

An object containing the current values of all configurable parameters defined for this animation. Keys match the `i` field of each config item.

```javascript
G.on(G.TYPE.INIT, () => {
  const speed = G.conf.speed;           // number
  const channel = G.conf.lyricsChannel; // number (stream index)
  const showText = G.conf.showText;     // boolean
});
```

Config values are set by the user through the animation settings panel. Defaults are specified in the animation's config definition. See [Animation Configuration](./animation-config) for how parameters are defined and which types are available.

`G.conf` is read-only — writing to it has no effect.

---

## Notes on encapsulation

Each module runs in an isolated environment. This means:

- CSS defined in your module does not leak to other modules (and vice versa).
- HTML elements are scoped to your module — use `G.getElementById`, not `document.getElementById`.
- JavaScript closures and module-level variables are private to your module instance.

When modules are combined into a **module collection**, they communicate exclusively via `G.on` / `G.emit` through the collection's shared event bus. See the [Module Collections guide](./module-collection) for details on how event routing can be customized within a collection.
