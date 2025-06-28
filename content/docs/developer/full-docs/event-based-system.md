---
sidebar_position: 3
---

# Event-Based System

In Anı⃰mr, the Event-Based System allows your modules to react to various built-in and custom events. This functionality enables dynamic interactions within your animations and games, enhancing user experience and engagement.

## Built-in Events

Anı⃰mr provides several built-in events that are automatically triggered by the framework. Here are some key events you can handle in your modules:

- **G.TYPE.PLAY**: Triggered when the song starts playing.
- **G.TYPE.PAUSE**: Triggered when the song is paused.
- **G.TYPE.TICK**: Fired on every animation tick/frame, allowing for smooth updates.
- **G.TYPE.SEEK**: Triggered when seeking to a different part of the song.
- **G.TYPE.INIT**: Fired when the module is initialized.
- **G.TYPE.RESIZE**: Triggered when the browser window is resized.
- **G.TYPE.BEAT**: Triggered at each beat of the music.
- **G.TYPE.MEASURE**: Triggered at the start of each measure (e.g., the first beat of the measure).
- **G.TYPE.TIMESIG**: Fired at the beginning of the song or when there’s a change in time signature.
- **G.TYPE.KEY**: Triggered at the start or when the key changes.
- **G.TYPE.CHORD**: Triggered when a chord is played.
- **G.TYPE.SECTION**: Fired when a part of the song (like verse, chorus, bridge, etc.) begins, if defined.
- **G.TYPE.LINE**: Triggered at the beginning of each line of lyrics.
- **G.TYPE.SEGMENT**: Fired for parts of the line that were sung by one person.
- **G.TYPE.WORD**: Triggered for each word sung.
- **G.TYPE.SYL**: Fired for each syllable.
- **G.TYPE.NOTE**: Triggered when a musical note is played.

## Custom Events

In addition to built-in events, you can create custom events specific to your module’s functionality. For example, if you are developing a module to display an animated score, you could handle a custom `"score"` event. This event could contain data about the current score or any changes made to it.

### Emitting Custom Events

To emit a custom event, use the following syntax:

```javascript
G.emit(eventType, eventData);
```

You can define your custom event names freely, but it’s recommended to use camel case for readability.

## Handling Events

To listen for both built-in and custom events in your module, you can use the following method:

```javascript
G.on(eventType, (eventData) => {
  // handler
});
```

This method will allow your module to respond dynamically to the events that occur during the execution of your animation or game.

## Conclusion

Utilizing the Event-Based System effectively can lead to a more interactive and engaging experience in your animations and games. Understanding how to handle both built-in and custom events is crucial for taking full advantage of the Anı⃰mr platform.

For more details on how to structure your modules and collections, please refer to the [Module Collections guide](#).
