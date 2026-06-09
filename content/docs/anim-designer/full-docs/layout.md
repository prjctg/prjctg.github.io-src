---
sidebar_position: 3
title: "Arranging the Layout"
---

# Arranging the Layout

## What is a layout?

The layout controls how your modules are positioned on screen at the same time. If your animation has only one module, it fills the entire screen automatically and you do not need to change the layout. Once you add a second module (or more), you choose a layout preset to decide how the screen is divided between them.

---

## Choosing a preset

Open the **Layout** tab to see the preset picker. Presets are grouped into two categories.

### Basic presets

| Preset | What it does |
|---|---|
| **Stack** | All modules occupy the full screen, layered on top of each other. Useful when modules are designed to blend or when one is a transparent overlay. |
| **Columns** | Modules are placed side by side in equal-width columns across the full height of the screen. |
| **Rows** | Modules are stacked in equal-height rows, one above the other, filling the full width. |

### Creative presets

| Preset | What it does |
|---|---|
| **PiP** | Picture-in-picture. The first module fills the entire frame as a background. The second module appears as a small panel in the bottom-right corner (about 28% of the frame width). |
| **Sidebar** | The first module takes the main area (roughly 70% of the width). The second module is a panel on the right side (30% of the width). |
| **Banner** | The first module takes most of the height. The second module is a strip along the bottom (20% of the height). |

Click any preset thumbnail to apply it. The **Layout Preview** updates immediately.

---

## The Slot Assignments list

Below the preset picker, the **Slot Assignments** section shows which module is assigned to each slot. Slots are labeled automatically (for example, `v1`, `v2`) when you add modules. You can rename a slot by expanding the module card in the **Modules** tab and editing the **Slot ID** field.

---

## The Layout Preview pane

The Layout Preview shows a live diagram of your current layout. Each slot appears as a labeled, outlined region so you can see at a glance how the screen will be divided and which module goes where.

- On **desktop**, the preview occupies the left side of the designer and is always visible.
- On **mobile**, the preview appears above the tab panel. Tap **Hide** to collapse it and give yourself more room to work, or tap **Show** to expand it again.

The preview updates automatically whenever you change a preset or add, remove, or reorder a module.

---

## Single-module animations

If your animation has exactly one module, the Layout tab shows a note:

> Single-module animations render full-size automatically. A layout is only needed if you add a second module.

You can still select a preset, but it will only take effect once you add another module.

---

## Custom layout

If none of the presets fit what you have in mind, the layout can be fully customized. Switching to a custom layout is an advanced feature available in developer mode — it lets you write your own HTML and CSS to position slots exactly as you want. If you are not a developer, the built-in presets cover the most common visual arrangements.

When you switch away from a custom layout to a built-in preset, a confirmation prompt will ask you to confirm, since the custom code will be discarded.
