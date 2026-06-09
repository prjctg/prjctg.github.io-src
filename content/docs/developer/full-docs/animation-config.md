---
sidebar_position: 5
title: "Animation Configuration"
---

# Animation Configuration

Animations can expose configurable parameters that users adjust without touching the code. You define these parameters in the animation's config array, and the platform renders the appropriate input controls automatically.

## Accessing config values

Config values are available on `G.conf`. Keys match the `i` field of each parameter definition.

```javascript
export default function main(G) {
  G.on(G.TYPE.INIT, () => {
    const speed = G.conf.speed;
    const channel = G.conf.lyricsChannel;
    // use config values to initialize your animation
  });
}
```

`G.conf` is read-only — writing to it has no effect.

Config values reflect the user's current settings. Read them inside your `G.TYPE.INIT` handler, which fires whenever the animation is initialized or reinitialized (including after the user changes a config setting).

## Defining config parameters

Config parameters are defined in the animation's `c` array. Each entry describes one parameter:

```js
{
  i:  "speed",         // (string, required) parameter key — used in G.conf
  n:  "Speed",         // (string, optional) display label; auto-generated from i if absent
  t:  "int",           // (string, required) type — drives the rendered input control
  d:  50,              // (any,    optional) default value
  o:  [...],           // (array,  optional) options list — used by select type
  mn: 0,               // (number, optional) minimum — used by int type
  mx: 100,             // (number, optional) maximum — used by int type
}
```

## Config types

### `int` — Numeric input

Renders a number input. Use `mn` and `mx` to constrain the range. The value is always a number.

```js
{ i: "speed", t: "int", d: 50, mn: 0, mx: 200 }
```

Access: `G.conf.speed` → `number`

### `check` — Checkbox

Renders a checkbox. Set `d` to `true` or `false`.

```js
{ i: "showLyrics", t: "check", d: true }
```

Access: `G.conf.showLyrics` → `boolean`

### `select` — Static dropdown

Renders a dropdown with fixed options. `o` must be an array of `[value, label]` pairs.

```js
{
  i: "colorScheme",
  t: "select",
  d: "dark",
  o: [["dark", "Dark"], ["light", "Light"], ["auto", "Auto"]]
}
```

Access: `G.conf.colorScheme` → the selected value (e.g. `"dark"`)

### `mchannel` — Lyrics channel selector

Renders a dropdown populated with the available lyric streams from the currently loaded song. The value is a zero-based channel index. Use this when your animation needs to follow a specific language or voice track.

```js
{ i: "lyricsChannel", t: "mchannel", d: 0 }
```

Access: `G.conf.lyricsChannel` → `number` (channel index)

Pass this value as the `channel` option when subscribing to lyric events:

```javascript
G.on(G.TYPE.SYL, { channel: G.conf.lyricsChannel }, (syl) => {
  // ...
});
```

### `tchannel` — Timing channel selector

Similar to `mchannel` but selects a timing stream rather than a lyric content stream.

```js
{ i: "timingChannel", t: "tchannel", d: 0 }
```

Access: `G.conf.timingChannel` → `number`

### `channel` — Generic channel selector

A generic channel selector. Uses the same dropdown presentation as `mchannel` and `tchannel` but without automatic channel-type filtering.

```js
{ i: "eventChannel", t: "channel", d: 0 }
```

Access: `G.conf.eventChannel` → `number`

### `text` — Text input

Renders a plain text input. Use this for free-form string parameters.

```js
{ i: "customLabel", t: "text", d: "Hello" }
```

Access: `G.conf.customLabel` → `string`

Any `t` value not listed above also renders a plain text input.

## Label auto-generation

If `n` is omitted, the display label is derived from `i` by splitting on camelCase boundaries and capitalizing the first letter:

| `i` value | Auto-generated label |
|---|---|
| `speed` | `Speed` |
| `showLyrics` | `Show Lyrics` |
| `lyricsChannel` | `Lyrics Channel` |
| `colorScheme` | `Color Scheme` |

Provide `n` explicitly if you want a different label.

## Config persistence

The platform saves each animation's config to local storage. When a user returns to the same animation, their previous settings are restored automatically. A **Reset to Defaults** button is always available to restore the original `d` values.
