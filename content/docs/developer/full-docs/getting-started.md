---
sidebar_position: 2
---

# Getting Started with Project G Development

Welcome to the development section of Project G! In this guide, you'll learn how to create animations and games that sync with music using the Project G platform. Development is entirely browser-based, so you won’t need to set up a local environment. Here's how you can get started:

## Key Concepts

Project G allows you to create both **animations** and **games**. The difference lies mainly in the interactivity level:

- **Animations** focus on visual effects triggered by music events.
- **Games** add interactive elements like mouse clicks or touch events and may include scoring logic or more complex event handling.

## Understanding Modules

In Project G, your development unit is a **module**, which combines JavaScript code, CSS, and HTML. Modules can be combined into a **module collection**, allowing for more complex layouts and interactivity. Each module encapsulates its CSS and HTML, ensuring that styles and markup do not interfere with other modules.

## Running Code in the Browser

You will develop your code online, directly in the Project G application. Each module runs directly in the browser through a special environment called the **Code Playground**, where you can test your animations and games alongside selected songs.
This includes three tabs where you can input:

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

Your modules will interact with built-in events triggered by the Project G framework (like play and pause) as well as custom events you define for your functionality (like scoring in a game). For now, the two main events you can handle are:

- **G.TYPE.PLAY**: Triggered when the song starts playing.
- **G.TYPE.PAUSE**: Triggered when the song is paused.

### Next Steps

Now that you have a basic understanding, let’s dive into the details of the event-based system!

## Advanced Details

For those interested in diving deeper into the concepts of Project G development, here are some additional details:

- **Module Structure**: Each module encapsulates its CSS and HTML, ensuring that styles and markup do not interfere with other modules.
- **Event Types**: You can handle built-in events triggered by the Project G framework and create custom events for specific functionality. For example, you might create events like "score" or "gameOver."

- **Module Collections**: A **module collection** consists of one or more modules combined together. You can also nest collections for more complex interactions and layouts.

- **Encapsulation and Interaction**: The JavaScript code can only access its own module's elements, promoting modular design and ensuring that interactions remain contained within their respective modules.

If you wish to learn more about these advanced topics, please refer to the [Event-Based System documentation](#) and the [Module Collections guide](#).

## Contributing to the Resource Center

The Resource Center documentation is open-source! Each page contains an "Edit this page" link that takes you to the page's GitHub repository.

### How to Contribute:

1. Fork the repository and make changes to the relevant Markdown files.
2. Create a new pull request with your edits.
3. Your changes will be reviewed and merged into the official documentation.

If you’ve never contributed to open source before, don’t worry—[GitHub's documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) provides helpful guides on how to create pull requests.
