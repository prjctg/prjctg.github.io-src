---
sidebar_position: 1
title: "Designer Overview"
---

# Designer Overview

The Anim Designer is the visual editor for building animations on Animr. It gives you a full-screen workspace divided into two areas: a **Layout Preview** pane on the left (or top on mobile) and a tabbed panel on the right where you do most of your work.

---

## The three tabs

The tabbed panel contains three sections. Click any tab to switch between them.

### Modules

The **Modules** tab is where you build the list of visual pieces that make up your animation. Each item in the list is a module — a self-contained visual effect or display created by a developer. You add, remove, and reorder modules here, and expand any module card to adjust its slot assignment and default settings.

See [Working with Modules](./modules) for the full guide.

### Layout

The **Layout** tab controls how multiple modules are arranged on screen. You choose from a set of visual presets — such as stacking modules on top of each other, splitting them into columns or rows, or using a picture-in-picture arrangement — and a live preview updates immediately to reflect your choice.

See [Arranging the Layout](./layout) for the full guide.

### Config

The **Config** tab is where you define adjustable controls that viewers can use when they watch your animation. For example, you might add a dropdown to let viewers choose a lyric language, or a number input to adjust a speed setting.

See [Animation Parameters](./config-params) for the full guide.

---

## The Layout Preview pane

The Layout Preview shows a live diagram of your current layout. Each module's slot appears as a labeled, outlined region so you can immediately see how the screen will be divided. The preview updates automatically whenever you change a preset or add a module.

On mobile, the preview is collapsible. Tap **Hide** to collapse it and free up screen space for the editing panel, or tap **Show** to bring it back.

---

## The Playground

The **Playground** is a safe space to experiment with the designer before committing to anything. Changes you make in the Playground stay in your browser session until you explicitly save them to the server. Nothing is published or shared until you choose to do so.

To try the designer in the Playground, go to the **Playground**, select the **Anim** mode, and click the **Design** tab.

---

## Saving and publishing

When you are happy with your animation:

- **Save as draft** — Stores your work privately so you can return and continue editing. Drafts are not visible to other users.
- **Save to server** — Makes the animation available. Note: if any of your modules carry a warning (draft reference, unversioned module), the designer will alert you before you can save to the server.

---

## How the designer relates to developer tools

Modules are the building blocks of every animation. A developer writes the code that powers each module — the logic that listens to the music and draws visuals on screen. The Anim Designer's job is to assemble those already-written modules into an animation, configure how they appear, and expose settings to viewers. You do not need to write or understand any code to use the designer.

If you do want to inspect or hand-edit the underlying animation data, the designer has an escape hatch: each animation has **JSON**, **CSS**, and **HTML** tabs alongside the **Design** tab. Switching to those tabs shows the raw module collection format, and any changes you make there are reflected back in the designer when you return. This round-trip is lossless for all features the designer supports.
