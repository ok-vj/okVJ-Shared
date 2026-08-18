# okVJ_UI Documentation

> **Note:** This documentation is incomplete and may be out of date. We are actively working on improving it.
> If you find an issue or something that is unclear, please open an issue on GitHub. Contributions are very welcome.

---

## Overview

`okVJ_UI` is a collection of UI components for TouchDesigner.

The following sections describe the common functionality shared by most modules, followed by documentation for individual submodules.

---

# Common Features

## MIDI Mapping

Most interactive UI elements can be mapped to MIDI.

### Setup

Connect a MIDI In CHOP to the `midi_in` input of the `okVJ_UI` component.

The input does not have to be MIDI. Any CHOP can be used if you want to map UI parameters from another source, such as OSC or a custom control system.

### Entering MIDI Map Mode

There are several ways to enter MIDI Map Mode:

* Click **MIDI Map** in the top-right corner of the UI.
* Press `Ctrl + Shift + M` on Windows/Linux.
* Press `Cmd + Shift + M` on macOS.
* Enable **MIDI Map** under the **GENERAL** page.

When MIDI Map Mode is active, a yellow outline appears around the UI component.

### Creating a MIDI Mapping

1. Enter MIDI Map Mode.
2. Click the UI element you want to map.
3. Move a MIDI control on your MIDI device.
4. The UI element is now mapped to that MIDI control.

To remove a mapping, right-click the mapped UI element.

### MIDI Settings

The **GENERAL** page contains the following MIDI settings:

| Parameter                    | Description                                                                                                                             |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **MIDI Map**                 | Enables or disables MIDI Map Mode.                                                                                                      |
| **MIDI Range**               | Defines the expected MIDI input range. Use `0-127` or `0-1`, depending on the source. An incorrect range can cause unexpected behavior. |
| **Toggle Behavior**          | Controls how toggle buttons respond to MIDI.                                                                                            |
| **View MIDI Map Table**      | Opens a table showing all current MIDI mappings.                                                                                        |
| **Remove All MIDI Mappings** | Removes all MIDI mappings from the UI.                                                                                                  |

### Toggle Behavior

Toggle buttons have two MIDI modes:

* **Toggle with MIDI** — The button toggles when it receives an ON message and toggles off when it receives another OFF message.
* **Follow MIDI** — The button follows the current state of the MIDI input.

---

# Preset Manager

Only **one Preset Manager** can be active in a project.

The Preset Manager can store and recall the state of UI elements.

Each submodule has an **Include in Preset** parameter on its **COMMON** page. Disable this parameter to exclude that submodule from preset storage and recall.

## Storing a Preset

1. Enter a preset name in the text field.
2. Press **Enter** or click **Learn Preset**.
3. The preset appears in the preset dropdown.

## Recalling a Preset

Select a preset from the dropdown.

The Preset Manager uses **flash recall**, meaning the UI immediately switches to the selected preset.

If you press the currently selected preset, if for example you want to switch back to the same preset after changing states, the UI starts fading toward that preset.

---

# Drag and Drop

Many `okVJ_UI` elements support drag-and-drop connections.

# Common UI Controls

### Move Bar

The line at the top of a submodule.

Drag it to reposition the module in the UI.

### X Button

Destroys the submodule.

### Hamburger Menu

Opens the parameters for the submodule.

### + / - Buttons

Add or remove operators inside the submodule.

---

# STYLE Page

By default, submodules use the style defined on the main `okVJ_UI` **STYLE** page.

Enable **Match UI** to override the style for an individual submodule.

---

# COMMON Page

Common parameters shared by submodules include:

| Parameter             | Description                                                         |
| --------------------- | ------------------------------------------------------------------- |
| **Edit Mode**         | Read-only parameter that reports the current UI Edit Mode state.    |
| **Include in Preset** | Determines whether the submodule is included in the Preset Manager. |
| **Page**              | Selects which `okVJ_UI` page displays the element.                  |
| **Show on All Pages** | Displays the element on every UI page.                              |

---

# INTERACT Page

Contains parameters that can be directly controlled through the UI.

---

# VALUES Page

Contains the input and output values of interactive controls such as:

* Sliders
* Buttons
* Knobs
* Other interactive elements

---

# OUTPUTS

Contains the output values generated by the submodule.

---

# FINE CTRL

Contains additional parameters for more precise control of the submodule.

---

# INPUTS

Some components receive inputs from other `okVJ_UI` submodules.

These inputs may be required for the component to have full functionality.

## Create Automatic Mappings

When **Create Automatic Mappings** is enabled, the component searches the current `okVJ_UI` and automatically creates references to compatible inputs.

This option is enabled by default.

---

# Submodules

## Audio Analysis

Analyzes an audio signal and generates four continuous values and four triggers:

* Low
* Mid
* High
* Total

### Interact

The following parameters can be controlled from the UI:

* **Main Slider** — Controls the main audio attenuation.
* **Trigger Threshold Low** — Threshold for the low-frequency trigger.
* **Trigger Threshold Mid** — Threshold for the mid-frequency trigger.
* **Trigger Threshold High** — Threshold for the high-frequency trigger.
* **Trigger Threshold Total** — Threshold for the total audio trigger.

When the audio level crosses a trigger threshold, the corresponding trigger fires.

### Drag and Drop

Drag from an audio level bar to obtain the corresponding audio value.

Drag from a spectrum trigger to obtain the corresponding trigger output.

### Parameters

#### Interact

Parameters that can be controlled directly from the UI.

#### Fine CTRL

**Normalize Audio**

Normalizes the input audio to a `0-1` range.

This makes the system less sensitive to changes in input volume, but can reduce some signal fidelity.

**Threshold**

Defines the level above which normalization is applied.

Keep this value above `0` to avoid division-by-zero issues.

### Filter

Each frequency band has its own filter.

Available parameters include:

* **Filter** — Selects the filter type, such as low-pass, band-pass, or high-pass.
* **Filter Cutoff** — Filter cutoff frequency in Hz.
* **Filter Resonance** — Controls filter resonance.
* **Rolloff** — Controls filter steepness in dB per octave.
* **Attenuate** — Applies attenuation after filtering and RMS calculation.
* **Smoothing** — Controls smoothing of the output signal.

### Outputs

| Output            | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| **Low Val**       | Low-frequency audio level.                                    |
| **Mid Val**       | Mid-frequency audio level.                                    |
| **High Val**      | High-frequency audio level.                                   |
| **Total Val**     | Total analyzed audio level.                                   |
| **Low Trigger**   | Trigger generated when the low level crosses its threshold.   |
| **Mid Trigger**   | Trigger generated when the mid level crosses its threshold.   |
| **High Trigger**  | Trigger generated when the high level crosses its threshold.  |
| **Total Trigger** | Trigger generated when the total level crosses its threshold. |

---

## Audio Mixer

Combines the analyzed audio values into a single output.

This allows you to change the balance between low, mid, and high frequencies without hard-coding the mix in your scenes.

### Inputs

By default, the inputs are automatically connected to the **Audio Analysis** component:

* Low Val
* Mid Val
* High Val

### Interact

Three attenuation controls are available:

* Low
* Mid
* High

The controls are arranged from left to right as:

**Low → Mid → High**

### Output

**Audio Val**

The combined low, mid, and high values after attenuation.

---

## Buttons

A collection of simple buttons.

Buttons can operate in either **Momentary** or **Toggle** mode.

### Setup

**Max Per Line**

Defines how many buttons are displayed before starting a new line.

For example, to display 8 buttons across 2 lines, set **Max Per Line** to `4`.

**Spacing (px)**

Sets the spacing between buttons in panel units/pixels.

**Button Mode**

Selects between:

* Toggle
* Momentary

### Styling

Controls the visual style of the buttons.

### Values

Contains the input and output values of the buttons.

Button parameters use the following naming convention:

```text
Buttons{i}press
```

Where `{i}` is the button index.

---

## Hue Picker

An HSV color selector.

### Interact

The following values can be controlled:

* Hue
* Saturation
* Value

### Output

**RGB**

Outputs the selected HSV color converted to RGB.

You can drag from the hue selector to create an RGB parameter connection.

### Fine CTRL

**Hue Range**

Limits the selectable hue range.

**Hue Steps**

Defines the number of discrete steps in the hue range.

**Smoothing**

Controls smoothing/filtering of the color changes.

---

## Knobs

A bank of rotary knobs.

### Setup

**Max Per Line**

Defines how many knobs are displayed before starting a new line.

For example, to display 8 knobs across 2 lines, set **Max Per Line** to `4`.

**Spacing (px)**

Sets the spacing between knobs.

**Reset Val**

Defines the value applied when the knob is right-clicked.

### Styling

Controls the visual style of the knobs.

### Values

Contains the input and output values of the knobs.

Knob parameters use the following naming convention:

```text
Knobs{i}val
```

Where `{i}` is the knob index.

---

## Notes

A text component used to enter and display notes.

---

## opViewer

Displays any TouchDesigner OP.

Enable **Interactive** to allow interaction with the displayed OP.

---

## paletteGenerator

> **Status:** Slightly deprecated.

Generates a color ramp from a base color and selected color harmonies.

### Usage

1. Select a base color using the HSV selector.
2. Enable the desired color harmonies using the buttons.
3. The component generates the corresponding color ramp.

---

## Radio Buttons

A collection of radio buttons where only one button can be selected at a time.

The output is a **zero-indexed integer** representing the currently selected button.

### Setup

**Max Per Line**

Defines how many buttons are displayed before starting a new line.

For example, to display 8 buttons across 2 lines, set **Max Per Line** to `4`.

**Spacing (px)**

Sets the spacing between buttons.

**Styling**

Controls the visual style of the buttons.

### DAT Table

A DAT table can be linked to the Radio Buttons component.

The component creates one button for each row in the table.

The contents of each row are used as button labels.

#### Parameters

**Exclude First Row**

Enable this if the DAT contains a header row.

**Column Index**

Selects which column is used for the button labels.

### Drag and Drop

You can drag and drop the following into the Radio Buttons component:

* A DAT table
* A DAT parameter object
* A TouchDesigner menu parameter

When a menu parameter is dropped, it is converted into a DAT table.

> **Note:** A DAT table created from a menu parameter will not automatically update when the original menu parameter changes.

### Output

Drag from any radio button to create a connection to the **Index** parameter.

The Index is a zero-based integer representing the selected button.

---

## Sliders

A collection of sliders.

### Setup

**Spacing (px)**

Sets the spacing between sliders.

**Orientation**

Controls the orientation of the sliders.

**Reset Val**

Defines the value applied when a slider is right-clicked.

### Values

Contains the input and output values of the sliders.

Slider parameters use the following naming convention:

```text
Sliders{i}val
```

Where `{i}` is the slider index.

---

## stepSeq

A step sequencer.

### Inputs

By default, the component receives audio triggers from the **Audio Analysis** component:

* Low Trigger
* Mid Trigger
* High Trigger
* Total Trigger

---

## timeKeeper
speed generator - can be used instead of absTime.seconds for eg
> Documentation to be added.
