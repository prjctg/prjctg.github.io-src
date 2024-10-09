---
sidebar_position: 4
---

# Module Collections

In Project G, a **module collection** is a grouping of one or more modules or even other module collections. It serves to organize and define the layout of these modules while also managing event routing within the collection.

## Structure of a Module Collection

A module collection can contain:

- Individual modules
- Other module collections

By nesting module collections, you can create complex layouts and hierarchical structures. Each module collection has its own ID, allowing for reference and reuse in other module collections.

## Layout and Default Behavior

Module collections can define their own HTML and CSS for layout purposes. If no custom HTML or CSS is defined, the framework applies default settings:

- **HTML**: Elements for each module are placed sequentially, with the first module being placed in an element with the ID `#0`, the second module in `#1`, and so on.
- **CSS**: Modules will take up the full height and width of their parent container and will be layered on top of each other. The first module will be at the bottom, and subsequent modules will be layered on top.

Example default layout:

- Module 0 is placed in the element `#0`.
- Module 1 is placed in the element `#1`, on top of module 0.

Custom layouts can be defined using your own HTML structure and CSS, allowing for more flexible designs if needed.

## Using IDs in Module Collections

Each module collection has an ID that can be used to reference it. This is particularly useful when you need to refer to another module collection as part of a larger collection. You can define the "modules" property in a collection by referring to the IDs of other collections or individual modules.

## Event Routing in Module Collections

By default, all modules within a collection are connected to an event bus. This means that events emitted by any module can be handled by other modules within the same collection.

The event routing can be customized if needed. For example, you might want to:

- Route events to specific modules
- Change the event names as they pass through the collection
- Transform event data before passing it along to other modules

This flexibility allows for more complex and dynamic event-driven behavior within your module collections.

## Encapsulation and Interaction

The elements within each module are encapsulated. This means that you should not access elements from another module directly. For example, using `document.getElementById` to reference an element from another module will not work.

Instead, you should use the Project G framework’s method `G.getElementById(id)` to access elements within your own module. This ensures encapsulation and maintains a clean separation between modules.

## Conclusion

Module collections in Project G provide a flexible way to organize and manage groups of modules, offering control over layout, event routing, and interaction. By using these collections, you can build complex animations or games that are easy to manage and extend.
