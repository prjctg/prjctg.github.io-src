---
sidebar_position: 2
title: "Working with Modules"
---

# Working with Modules

## What is a module?

A module is a self-contained visual effect or display — for example, a karaoke-style lyric display, a chord chart, or an abstract background animation. Each module is a piece of code written by a developer and published to Animr. Your job in the designer is to pick the modules you want and combine them.

Your animation can have one module or several. A single module fills the entire screen automatically. When you add more than one module, the **Layout** tab controls how they are arranged.

---

## Adding a module

1. Open the **Modules** tab in the designer.
2. Click **Add Module**.
3. In the dialog that appears, choose a module type:
   - **Code Module** — A standalone visual component.
   - **Animation** — An existing animation to embed as a layer inside yours.
4. Browse or search the list and click the item you want.

The module is added to your list and its card expands automatically so you can review its settings.

---

## The module card

Each module appears as a card in the list. The card header shows the module's name, its type, and its assigned slot ID. Click a card header to expand or collapse the settings panel below it.

Inside the expanded panel you will find:

- **Slot ID** — A short label that identifies where this module lives in the layout. Slot IDs only matter when your animation has more than one module; for a single-module animation you can leave the default value.
- **Default Values** — Override default settings that the module's developer defined. If you leave these empty, the module uses its built-in defaults.
- **Param Mappings** — Connect a global animation parameter (from the Config tab) to a setting inside this module. This lets a single viewer control affect multiple modules at once.

---

## Reordering modules

Inside an expanded module card, use the **up arrow** and **down arrow** buttons at the bottom of the panel to change the module's position in the list. The order matters for layout presets that stack modules on top of each other.

---

## Replacing a module

To swap a module for a different one without losing its slot assignment:

1. Expand the module card.
2. Click **Change** at the bottom of the panel.
3. Pick a replacement from the dialog that opens.

The module is replaced in place; its slot ID and any mappings you set are preserved.

---

## Removing a module

1. Expand the module card.
2. Click **Remove** at the bottom of the panel.
3. Confirm the prompt.

---

## Module warnings

The designer shows warning badges and banners when a module needs attention. These warnings must be resolved before you can save your animation to the server.

### Draft module

A badge labeled **Draft** appears on the card header. A banner at the top of the designer reads:

> **Contains draft modules.** Can only be saved as a draft until all draft modules are replaced with published versions.

**What it means:** This module is a draft that lives only in your browser — it has not been published to Animr. Drafts cannot be included in a published animation.

**What to do:** Replace the module with a published version using the **Change** button on the card.

---

### Unversioned code module

A banner at the top of the designer reads:

> **Contains unversioned code modules.** Pin each code module to a specific version (e.g., module@1.0) before saving to server.

**What it means:** The code module is referenced by name only, without a pinned version number. Animations saved to the server must point to a specific version so that playback stays consistent even if the module is updated later.

**What to do:** Contact the developer of the module, or replace the module with one that specifies a version.

---

### Missing module

A badge labeled **Missing** appears on the card header. A banner at the top of the designer reads:

> **Missing modules detected.** Some referenced drafts no longer exist. Expand the module card to replace them.

**What it means:** A draft module that was previously in your animation has been deleted and can no longer be found.

**What to do:** Expand the module card and click **Change** to replace it with a different module.
