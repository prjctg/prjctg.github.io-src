---
sidebar_position: 1
---

# Project G Full Developer Documentation

Welcome to the **Project G Full Developer Documentation**! This guide is designed to help developers create dynamic animations and games that are synchronized with music, all within a browser-based environment. Whether you're creating simple visual effects or complex interactive games, this documentation will walk you through the core concepts and advanced techniques for building on the Project G platform.

## What is Project G?

Project G is a platform for creating and running music-driven animations and games. Each creation is made up of **modules**, which are built using JavaScript (as ES Modules), CSS, and HTML. These modules respond to events triggered by the music, allowing for seamless synchronization between visuals, interactions, and sound.

## Why Develop with Project G?

Project G offers a fully browser-based development environment, so you don’t need to set up any local tools or environments. The platform provides a code playground where you can write, run, and test your code directly in the browser, along with a selected song. Here are some reasons why developers might choose Project G:

- **Real-Time Sync with Music**: Your animations and games react to events in the song, such as beats, measures, and lyrical lines.
- **Event-Driven Development**: Project G modules handle both built-in music events and custom events, giving you full control over the interactivity.
- **Modular Design**: By building with encapsulated modules, you can create reusable components that can be combined into more complex layouts.
- **No Setup Required**: All development happens online. There's no need for local environments, making it quick and easy to start coding.

## Key Concepts

Before you dive into development, it's important to understand the core building blocks of the Project G platform:

### 1. Modules

A **module** is the smallest development unit in Project G. It consists of:

- **JavaScript**: Implemented as a JavaScript ES Module. Each module exports a main function that is responsible for controlling the animation or game logic.
- **CSS**: For styling your module.
- **HTML**: Defines the structure of your module's elements.

Modules are self-contained and encapsulated, meaning each module's code can only access its own elements.

### 2. Module Collections

A **module collection** is a group of modules (or other module collections) combined together. Module collections allow for complex layouts and interactions between different modules. They also manage event routing, so that modules within a collection can communicate with one another.

### 3. Event-Based System

Project G is powered by an **event-based system**. Modules respond to events triggered by the platform (like when the music plays or pauses) and can also emit and handle custom events. This makes it possible to create interactive games or animations that are tightly coupled with the music being played.

### 4. Code Playground

The **Code Playground** is where you'll write and run your code. It consists of three main tabs:

- **JavaScript**: For your ES Module code.
- **CSS**: For your styles.
- **HTML**: For your module's structure.

Once you've written your code, simply select a song and click "Run" to see your animation or game in action.

## What You’ll Learn

Throughout this documentation, you’ll find detailed guides and references covering the following topics:

### 1. **Getting Started**

- Learn how to set up and run your first Project G module.
- Understand the basic structure of modules and the Code Playground environment.

### 2. **Event-Based System**

- Dive deeper into the event system in Project G, including both built-in music events and custom events.
- Learn how to trigger and respond to events in your modules.

### 3. **Module Collections**

- Explore how to group modules together using collections.
- Learn about layout control, event routing, and interaction between modules within a collection.

### 4. **Advanced Topics**

- Discover advanced concepts such as customizing event handling, encapsulation, and more.
- Find examples and techniques to build more sophisticated animations and games.

### 5. **Code Examples & Tutorials**

- Access sample code and tutorials to help you get started quickly.
- Learn how to implement different types of animations and games step-by-step.

### 6. **Reference Guides**

- Detailed API reference for working with the `G` object, which is used to interact with the platform.
- Comprehensive lists of available built-in events, constants, and methods provided by Project G.

## Allowable Imports & Libraries

When developing with Project G, you are free to use external libraries, provided they are hosted on **jsDelivr** or **esm.sh**. There are no restrictions on which libraries you can use, allowing for flexibility in your development process. This ensures security while also giving you the freedom to choose the best tools for your project.

## How to Contribute

While Project G itself is not open-source, the **Resource Center documentation** is! If you'd like to contribute to improving the documentation, every page contains an "Edit this page" link that will take you to the corresponding Markdown file on GitHub. From there, you can fork the repository, make changes, and submit a pull request.

For detailed instructions on contributing, refer to the [Contributing Guide](#).

## Next Steps

Ready to start developing? Head over to the [Getting Started](./getting-started) guide to begin building your first animation or game module. You’ll learn how to structure your code, run it in the browser, and handle basic events triggered by the music.

Let’s get started!
