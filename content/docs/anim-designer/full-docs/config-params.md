---
sidebar_position: 4
title: "Animation Parameters"
---

# Animation Parameters

## What are animation parameters?

Animation parameters are adjustable controls that appear in the animation's settings panel when someone watches it. They let viewers personalize the experience — for example, choosing which lyric language to display, switching between a dark and light style, or adjusting a speed or intensity value.

As the animation's author, you define which parameters exist, what type of control each one is, and what the default value is. Viewers can then change those values to suit their preference without affecting anyone else's experience.

---

## Managing parameters

Open the **Config** tab in the designer to see the list of parameters you have defined.

- To add a new parameter, click **Add Param**.
- To edit an existing parameter, click the pencil icon on its card.
- To delete a parameter, click the trash icon on its card and confirm the prompt.

---

## Adding or editing a parameter

Clicking **Add Param** (or the pencil icon) opens a small form. Fill in the fields:

- **ID** — A short internal name for the parameter, used to connect it to your modules. Required.
- **Name** — The label that appears in the viewer's settings panel. If you leave this blank, the ID is used as the label.
- **Type** — The kind of control to show. See below for the available types.
- **Default** — The value the parameter starts at before the viewer makes any changes. Not available for channel selector types (those are set at runtime based on the loaded song).

Click **Save** to add the parameter to your list.

---

## Parameter types

### Text

A plain text input. Use this for free-form string values such as a custom label or a search term.

### Number

A number input. You can optionally set a **Min** and **Max** value to restrict the range the viewer can enter.

### Color

A color picker accompanied by a text field. The viewer can click the color swatch to open a color picker or type a color value directly.

### Boolean

A true/false toggle rendered as a dropdown with **true** and **false** options. Use this for on/off settings such as "Show lyrics" or "Enable background animation".

### Lyrics Track

A dropdown that lists the lyric streams available in the currently loaded song. The viewer picks which language or voice track the animation should follow. The options are filled in automatically at runtime — you do not need to list them yourself.

### Translation Track

Similar to **Lyrics Track**, but lists the translation streams available in the currently loaded song instead of the original lyric streams.

### Select

A dropdown with a fixed list of options that you define. Click **Add option** in the form to add each choice; each option has a **value** (the internal identifier) and a **label** (what the viewer sees).

---

## What parameters look like to viewers

When a viewer opens your animation, they can access a settings panel that shows all the parameters you have defined. Each parameter appears with its **Name** as the label and the appropriate control for its type. The viewer's selections are saved locally so their preferences are restored the next time they watch the animation.

---

## Connecting parameters to modules

Defining a parameter in the **Config** tab makes it available across your whole animation. To wire it to a specific module setting, open the **Modules** tab, expand the module card, and use the **Param Mappings** section to link the global parameter to the module's own parameter. This lets a single viewer control affect multiple modules at once.
