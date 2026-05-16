---
sidebar_position: 5
---

# Animation Configuration

Animations can expose configurable parameters that users adjust without touching the code. You define these parameters in the animation's config array, and the platform renders the appropriate input controls automatically.

## Accessing Config Values

Config values are available on the `G` object:

```javascript
export default function main(G) {
  G.on(G.TYPE.INIT, () => {
    const speed = G.conf.speed;
    const channel = G.conf.lyricsChannel;
    // use config values to initialize your animation
  });
}
```

Config values reflect the user's current settings. They are read once at init time — if you need to respond to config changes, re-read `G.conf` inside your `G.TYPE.INIT` handler (which fires whenever the animation is (re)initialized).

## Defining Config Parameters

Config parameters are defined in the animation's `c` array on the backend. Each entry describes one parameter:

```js
{
  i:  "speed",         // (string, required) parameter key — used in G.conf
  n:  "Speed",         // (string, optional) display label; auto-generated from i if absent
  t:  "int",           // (string, required) type — drives the rendered input
  d:  50,              // (any,    optional) default value
  o:  [...],           // (array,  optional) options list — used by select types
  mn: 0,               // (number, optional) minimum — used by int type
  mx: 100,             // (number, optional) maximum — used by int type
}
```

## Config Types

### `int` — Numeric slider / number input

Renders a number input. Use `mn` and `mx` to constrain the range.

```js
{ i: "speed", t: "int", d: 50, mn: 0, mx: 200 }
```

### `check` — Checkbox

Renders a checkbox. Default is `true` or `false`.

```js
{ i: "showLyrics", t: "check", d: true }
```

### `select` — Static dropdown

Renders a dropdown with fixed options. `o` must be an array of `[value, label]` pairs or plain scalar values.

```js
{ i: "colorScheme", t: "select", d: "dark", o: [["dark", "Dark"], ["light", "Light"], ["auto", "Auto"]] }
```

### `mchannel` — Lyrics channel selector

Renders a dropdown populated with the available lyric streams from the currently loaded song. The value is a zero-based stream index. Use this when your animation needs to follow a specific language or voice track.

```js
{ i: "lyricsChannel", t: "mchannel", d: 0 }
```

### `tchannel` — Time channel selector

Similar to `mchannel` but used to select a timing stream rather than a lyric content stream.

```js
{ i: "timingChannel", t: "tchannel", d: 0 }
```

### `channel` — Generic channel selector

A generic channel selector. Uses the same dropdown style as `mchannel`/`tchannel` but without automatic channel-type filtering.

```js
{ i: "eventChannel", t: "channel", d: 0 }
```

### Text fallback

Any type string not listed above renders a plain text input. This is useful for free-form string parameters.

```js
{ i: "customLabel", t: "text", d: "Hello" }
```

## Label Auto-Generation

If `n` is omitted, the label is derived from `i` by splitting on camelCase boundaries:

- `lyricsChannel` → `Lyrics Channel`
- `showLyrics` → `Show Lyrics`
- `speed` → `Speed`

## Config Persistence

The platform saves each animation's config to local storage. When a user returns to the same animation, their previous settings are restored. A **Reset to Defaults** button is always available to restore the original `d` values.
