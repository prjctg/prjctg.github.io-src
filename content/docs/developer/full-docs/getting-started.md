---
sidebar_position: 2
---

# Getting Started with Project G Development

Welcome to the development section of Project G! In this guide, you'll learn how to create animations and games that sync with music using the Project G platform. Development is entirely browser-based, so you won’t need to set up a local environment. Here's how you can get started:

## Key Concepts

Project G allows you to create both **animations** and **games**. Both types of modules share the same structure and are implemented using JavaScript, CSS, and HTML. The difference lies mainly in the interactivity level:

- **Animations** focus on visual effects triggered by music events.
- **Games** add interactive elements like mouse clicks or touch events and may include scoring logic or more complex event handling.

## Running Code in the Browser

In Project G, your code runs directly in the browser through a special environment called the **Code Playground**. This includes three tabs where you can input:

- **JavaScript ES Module**: The core logic for your animation or game.
- **CSS**: For styling your animation.
- **HTML**: The structure or layout of elements.

### Key Steps:

1. **Write Your Module**: You will implement your module as a JavaScript ES Module, exporting a main function. This function receives an object conventionally named `G` as the first argument, which contains methods and constants to interact with the platform. You’ll use this object to control animation initialization and event handling.

2. **Run Your Code**: After inputting your code in the Code Playground, hit the "Run" button. Your code will run alongside the currently selected song, and music events will trigger the appropriate handlers in your code. If no song is selected, you'll need to pick one before running the code.

3. **Debugging**: Any errors or exceptions will be shown directly on the running page as well as in your browser’s Developer Tools console.

#### Example:

```javascript
export default function main(G) {
  // Your animation or game logic here
  G.on(G.TYPE.PLAY, () => {
    console.log("Music started playing!");
  });

  G.on(G.TYPE.PAUSE, () => {
    console.log("Music is paused!");
  });
}
```

## Allowable Imports and External Libraries

You can import any external libraries you need, provided they are hosted on **jsDelivr** or **esm.sh**. This ensures security and browser compatibility. There are no restrictions on which libraries to use—you're free to explore and choose the best tools for your project.

## Running Your Code with Music

Once a song is selected and your code is running, the Project G platform will trigger your code based on music events. You can use the `G` object to handle these events and synchronize your animations or game actions with the music.

For now, the two main events you can handle are:

- **G.TYPE.PLAY**: Triggered when the song starts playing.
- **G.TYPE.PAUSE**: Triggered when the song is paused.

## Contributing to the Resource Center

While Project G itself is not open-source, the Resource Center documentation is! Each page contains an "Edit this page" link that takes you to the page's GitHub repository.

### How to Contribute:

1. Fork the repository and make changes to the relevant Markdown files.
2. Create a new pull request with your edits.
3. Your changes will be reviewed and merged into the official documentation.

If you’ve never contributed to open source before, don’t worry—[GitHub's documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) provides helpful guides on how to create pull requests.
