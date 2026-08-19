# okVJ-Shared 0.9
This documentation is incomplete and sometimes out of date, we are working on it. If you find an problem in the docs please raise an issue on GitHub, and we will get it fixed. We'd be very grateful for your contributions on this.


In the okVJ-Shared folder, most UI elements are available as stand-alone toxes to be used outside of okVJ_UI, however, some of their functionality are limited in this mode.

- okVJ_UI - explained below.
- standAloneUIComponent - the okVJ_UI components as stand alone components to be used outside of okVJ_UI, however, some of their functionality are limited in this mode.
- mappings - Tools for mapping and live performance in domes
- fxRack - Visual effects for live performance. This section needs an overhaul and will be documented later.
- generators - Tools for generating visuals. - a shaderChanger and a sceneChanger.

---

# okVJ_UI.tox — User Manual

_Interactive modular VJ control surface for TouchDesigner_

---

## What is okVJ_UI?

Just drop it into your TD-project. You can only have one okVJ_UI tox in your project file.

okVJ_UI is a modular control surface that lives inside your TouchDesigner project. It lets you build a custom interface from components — sliders, sequencers, modulators, knobs, and buttons and more — and map them to your project parameters and MIDI devices quickly and easilly.

It runs in two modes: a live mode (default) and an **Edit** mode for building your layout.

---

## Perform Bar

The perform bar runs across the top of the UI and is always visible. From left to right: You can hide in the okVJ_UI parameters.

| Element          | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| FPS              | Current frames per second                                                |
| BPM              | Enter a BPM value, or use the Tap Tempo component                |
| Resolution X / Y | Global resolution reference. Use it in your project through parameter bindings |
| Midi Map         | Toggle MIDI map mode — `Ctrl+Shift+M`                                    |
| Edit Mode        | Toggle edit mode — `Ctrl+Shift+E`                                        |
| Hamburger Menu   | Global okVJ UI settings, including colors, resolution, and Match UI              |

---

## Edit Mode

### Entering & exiting

Toggle with the `Edit Mode` button (top right) or `Ctrl+Shift+E`. Same action gets you in and out.
Layout controls are disabled outside Edit mode. This helps prevent accidental changes during a performance.

### Adding a component

1. Double-click - or press TAB - in the UI panel to open the component picker
2. Select a component. It appears at the cursor position.
3. Drag the move bar to move the component. Drag the edges to resize it.
4. Use the X button to delete the component.
   > **Note:** If a component has `+` / `−` buttons, use them to add or remove elements inside that component.

### Moving & resizing

- Drag the **move bar** to reposition a component freely within the panel
- Drag any **edge** to resize
- If **Snap to Grid** is enabled, position and size both snap to your configured grid step (set this up in the STYLE page on okVJ_UI)
- Labels are editable in edit mode — you can tab through them

### Per-component controls

These are only visible in edit mode:

| Control        | Description                                               |
| -------------- | --------------------------------------------------------- |
| `×`            | Delete the component                                      |
| `+` / `−`      | Add or remove internal elements (on supported components) |
| Hamburger menu | Per-component settings                                    |

### Connecting controls to your TD network

Drag a parameter from a component into your TouchDesigner network to create a reference or binding. You can do this directly from the UI in Edit mode. Most interactive parameters support this method. It is the main way to connect UI controls to TouchDesigner operators without writing expressions manually.

You can also drag parameters from the component's parameters. Output values are found under the **VALUES** or **OUTPUTS** tab. There is also an output CHOP on okVJ_UI available if you prefer that approach, though drag-and-drop is generally cleaner.

---

## MIDI Map Mode

### Mapping a control

1. Press `Midi Map` in the top right, or `Ctrl+Shift+M`
2. Click a UI element to arm it — it will wait for input
3. Move a knob, fader, or button on your MIDI device — the mapping is created automatically.
4. Right-click a mapped element to remove its mapping, or press **Remove All Midi Mappings** in the okVJ_UI parameters under the **GENERAL** tab, to clear all
5.Under the **GENERAL** tab on okVJ_UI you have acess to more midi option.

### Preventing value jumps

When you switch presets or move a parameter with the mouse and then pick up a MIDI control, the value can jump abruptly. To prevent this, enable **MIDI Channel Pickup** under the **General** tab. The MIDI control won't take effect until its physical position crosses the current on-screen value.

### MIDI settings

Open the okVJ_UI parameters **General** tab to configure:

| Setting             | Description                                                                                                                           |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| MIDI Range          | Choose 0–1 or 0–127 input range                                                                                                       |
| MIDI Channel Pickup | When on, a MIDI control only takes effect after its value crosses the current on-screen value — prevents jumps when switching presets |
| Toggle Behavior         | Set the toggle Behavior, when "toggle with midi" a button press will toggle a toggle button. when "follow midi", it will be the same value as the midi, so it won't have internal toggle logic.
|View Midi Map Table | view the table of midi mappings
|Remove All Midi Mappings|removes ALL midi mappings

---

## Presets Manager

Open the preset manager from the hamburger menu. It appears at your current cursor position. All components with **Include in Preset** enabled will be stored and recalled.

This component wraps Alpha Moonbase's [Tau Ceti](https://github.com/PlusPlusOneGmbH/TauCeti) preset engine, with minor internal edits marked clearly inside. Components are added to the Tau Ceti stack automatically. To opt a component out, toggle **Include in Preset** off under its **COMMON** page.

**Using the preset manager:**

- Type a preset name in the text field and press **Learn** to save
- Select a preset from the scroll list.
- Use the transition time slider to set the transition duration.
- **RECALL** — recall a preset; **STOP** — cancel a transition in progress
- Toggle **Flash Recall** on to switch immediately as soon as a new preset is selected
- You can also remove, rename, or replace the selected preset, or remove all presets.

Use **MIDI Channel Pickup** to smoothly transition from a recalled preset back to physical MIDI control without value jumps.

---

## UI Parameters (Hamburger Menu)

| Parameter                  | Description                                                               |
| -------------------------- | ------------------------------------------------------------------------- |
| UI Resolution              | Sets the resolution of the UI panel                                       |
| Color Themes               | Apply a premade color theme to all components                             |
| Match all elements with UI | Pushes the current style settings to all components with Match UI enabled |
| Snap to Grid               | Quantizes component position and size to a grid                           |
| Edit Mode                  | Toggle edit mode                                                          |
| Midi Map                   | Toggle MIDI map mode                                                      |

### Color themes

Select a color theme from the hamburger menu — colors update across all matching components. Components with **Match UI** enabled will sync automatically. You can also adjust colors per-component or override them globally from the okVJ UI settings page.

### Snapping

When **Snap to Grid** is enabled, component positions and sizes are quantized to the grid step size you set. Useful for keeping a clean, aligned layout.

---

## Sub-Components

All okVJ component outputs and expected inputs and outputs are normalized to a **0–1 range**.
Most sub-components share these traits:

- **MIDI-mappable** — can be assigned to a MIDI control in MIDI Map mode
- **Presettable** — values are saved and recalled by the preset manager
- **Labels** — each element displays an editable label; you can tab through them in edit mode
- **Add / remove elements** — use the `+` / `−` buttons in edit mode to change the number of elements inside the component

## The outputs are found under the VALUES or OUTPUTS tab

### Knobs

A group of rotary knobs.

| Parameter    | Description                              |
| ------------ | ---------------------------------------- |
| Max per Line | How many knobs appear per row            |
| Spacing      | Space between knobs                      |
| Reset Val    | Value each knob resets to on right-click |

---

### Sliders

A group of sliders.

| Parameter   | Description                                |
| ----------- | ------------------------------------------ |
| Orientation | Horizontal or vertical layout              |
| Spacing     | Space between sliders                      |
| Reset Val   | Value each slider resets to on right-click |

---

### Buttons

A group of buttons.

| Parameter    | Description                           |
| ------------ | ------------------------------------- |
| Max per Line | How many buttons appear per row       |
| Spacing      | Space between buttons                 |
| Button Mode  | **Toggle** (default) or **Momentary** |
| Styling      | Visual style of the buttons           |

> **Note on MIDI + Toggle mode:** When a toggle button is MIDI-mapped, it reads the raw incoming MIDI value rather than flipping its own state — so all buttons effectively behave as momentary from the MIDI side. Configure your MIDI controller to send toggle values if you need latching behaviour. Or set the **Toggle Behavior** in the midi settings to "toggle with midi - toggleOn"

---

### XY Pad

A bank of two-axis XY pads. Each pad outputs two values (X and Y), both normalized 0–1.

| Parameter    | Description                     |
| ------------ | ------------------------------- |
| Max per Line | How many XY pads appear per row |
| Spacing      | Space between pads              |

> **MIDI mapping an XY pad:** Enter MIDI Map mode, click the pad to arm it, then move one MIDI control to map X — the pad will immediately wait for a second control to map Y.

---

### Radio Buttons

An array of buttons where only one can be active at a time. Outputs the zero-indexed **integer index** of the selected button.

| Parameter    | Description                     |
| ------------ | ------------------------------- |
| Max per Line | How many buttons appear per row |
| Spacing      | Space between buttons           |
| Styling      | Visual style of the buttons     |

**DAT Table:**

Reference a DAT table to drive the button array dynamically:

- The number of buttons is set by the number of rows in the table
- Labels are read from a chosen column — set which one with **Column Index**
- Toggle **Include First Row** off to skip a header row
- you can drag and drop a DAT table to the UI to reference it.
- you can also drag a menu parameter to create a button list from it

---

## Complex Components

The following components are more complex operators that perform logic and can automatically map and interact with each other.

**INTERACT** — parameters that can be controlled from the UI, via mouse, MIDI, or the preset manager.

**INPUTS** — for components that require an input. If **Create Automatic Mappings** is enabled, okVJ will automatically map to compatible components in the panel. You can also create manual mappings under the INPUTS tab — toggle Automap off in that case. Certain UI elements will be disabled until something is linked to their parameters.

Some components also have a **FINE CTRL** tab for more specialized controls.

---

### Audio Analysis

Analyzes an audio signal and outputs:

- 4 float values — low, mid, high, and total
- 4 audio triggers — low, mid, high, and total

The audio input source is configured in the component itself. Use the **Coarse Audio** knob to set input level, and the FINE CTRL band settings to isolate the frequency ranges you want to react to.

**INTERACT:**

| Parameter    | Description                                                                                                       |
| ------------ | ----------------------------------------------------------------------------------------------------------------- |
| Coarse Audio | Coarse control of audio input level                                                                               |
| Trigger Vals | Threshold values — when the audio signal crosses a threshold, an audio trigger fires (visible on the UI spectrum) |

**FINE CTRL:**

Three frequency bands (low, mid, high), each with:

| Parameter        | Description                    |
| ---------------- | ------------------------------ |
| Filter Type      | Lowpass, bandpass, or highpass |
| Filter Cutoff    | Cutoff frequency in Hz         |
| Filter Resonance | Resonance amount               |
| Filter Rolloff   | Rolloff in dB per octave       |
| Attenuate        | Per-band output attenuation    |

**Drag & drop:** Drag audio values from the audio bars; drag triggers from the indicator on the spectrum visualizer.

---

### Step Sequencer

> Recommended: Add an Audio Analysis component to the panel for full functionality.

The sequencer can run without Audio Analysis — if no audio triggers are connected or **BPM Mode** is on, it clocks from the global BPM instead.

**INPUTS:**

4 trigger inputs — low, mid, high, and total. If none are provided, or if BPM Mode is enabled, the sequencer uses the global BPM as its clock.

**INTERACT:**

| Parameter               | Description                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------- |
| BPM Mode                | Toggle between BPM clock and audio trigger clock                                   |
| Trigger Index (LMHT)    | Which trigger input is used as the clock source — also selectable via UI buttons   |
| Reset                   | Reset the sequence to step zero                                                    |
| Release                 | Envelope release time in seconds                                                   |
| Selected Sequence Index | Zero-indexed — selects which of the four sequences is active                       |
| Sequence ID             | Current sequence as an integer (read-only) — used by the preset manager for recall |

> **Note:** Sequence step buttons are not MIDI-mappable. All other UI elements are.

**OUTPUTS:**

- Selected sequence envelope
- Selected sequence gate
- All four sequences are individually available for reference

**FINE CTRL:**

| Parameter       | Description                          |
| --------------- | ------------------------------------ |
| Sequence Length | Number of steps                      |
| BPM Subdivision | Clock subdivision relative to BPM    |
| Gate Mode       | Output a trigger or a sustained gate |

**Drag & drop:** Drag from the sequence selection panel to use the sequence envelope elsewhere in your network.

---

### XY Modulator

> Recommended: Add Audio Analysis and Step Sequencer to the panel for full functionality.

To set up the XY Modulator to react to your sequencer, add both a Step Sequencer and an Audio Analysis to the panel and make sure **Create Automatic Mappings** is enabled. okVJ will wire the sequencer's gate output to the XY Modulator's trigger input automatically.

**INTERACT:**

| Parameter   | Description                |
| ----------- | -------------------------- |
| Audio React | Toggle audio reactivity    |
| Speed       | Movement speed             |
| Amplitude   | Movement amplitude         |
| Smooth      | Amount of output smoothing |

**Type select:**

| Index | Mode          | Description                                                                                                  |
| ----- | ------------- | ------------------------------------------------------------------------------------------------------------ |
| 0     | Sin/Cosine    | Circular motion using a sine/cosine pair                                                                     |
| 1     | Noise         | Sparse noise — shape adjustable in FINE CTRL                                                                 |
| 2     | Sample & Hold | Jumps to a random position on each trigger (from sequencer gate, BPM, or audio triggers in Audio React mode) |
| 3     | Manual        | Use the XY pad directly, or bind MIDI to ManualX / ManualY                                                   |

Outputs two normalized float values: **X** and **Y**.

---

### Palette Generator

Generates a color palette and outputs ramp keys for a Ramp TOP. You can save and recall the palette with the preset manager.

Select a base color with the color picker. Set its saturation and value. Turn on harmony modes, such as complementary or analogous, to generate additional colors.

**INTERACT:**

| Parameter       | Description                                       |
| --------------- | ------------------------------------------------- |
| Color Picker    | Set the base hue                                  |
| Saturation      | Base color saturation (MIDI-mappable)             |
| Value           | Base color brightness (MIDI-mappable)             |
| Harmony Toggles | Complementary, analogous, and other harmony modes |

**FINE CTRL:**

| Parameter       | Description                     |
| --------------- | ------------------------------- |
| Transition Time | Fade time between color changes |

**Drag & drop:** Drag from the bottom ramp preview to a Select DAT to get the ramp keys.

---

### Tap Tempo

Tap to set the global BPM. Cooldown time between taps is configurable in the okVJ_UI parameters.

---

### Notes

A notepad for notes during setup or live performance.

---

### topViewer

A panel for previewing TOPs. Drag and drop a TOP into the panel.

> **Known issues:** If topViewer is set to fit the aspect of the content, it cannot be resized horizontally. It may also flicker slightly while resizing.

---

### opViewer

A panel for viewing any operator in TD. a CHOP, DAT, COMP, TOP etc etc

Toggle "interactive" if you want to interact with the panel.

### huePicker
an HSV color picker

## Automatic Mappings

Some components, such as Step Sequencer and XY Modulator, support automatic mapping. When you add one of these components, okVJ UI looks for compatible source components, such as Audio Analysis, and connects them automatically with parameter expressions.

Automatic mappings are refreshed when you add or remove a component that uses the mapping system.

---

## SAVING A UI-LAYOUT
You can save a UI Layout if for example the is an okVJ update.
under the Layout tab - press **Save Current Layout**

This will create a component that you can save or copy and paste.

you can add this component to the **Layout Comp** parameter and press **Load Layout**
to load that layout.

Presets and midimappings will not persist in layout saves (yet).

## Frequently Asked Questions

AI Generated FAQ:

**How do I connect a UI control to a parameter in my TD network?**
Drag directly from the control (or from the VALUES/OUTPUTS tab in the component's hamburger menu) into your TouchDesigner network. This creates a reference or binding without needing to write expressions manually. You can also use the UI output CHOP, but drag-and-drop is recommended for simpler networks.

**Why are some UI elements greyed out or disabled?**
Complex components like the XY Modulator or Step Sequencer disable certain controls until inputs are connected. Either enable **Create Automatic Mappings** so okVJ wires things up for you, or manually link inputs under the INPUTS tab.

**The values jump when i move my MIDI device after having moved it with the mouse — how do I prevent this?**
Enable **MIDI Channel Pickup** in the hamburger menu → General tab. The MIDI control won't take effect until its physical position crosses the current on-screen value.

**Can I save and recall my control values?**
Yes — use the Preset Manager (accessible from the hamburger menu). Make sure **Include in Preset** is enabled on each component you want stored. The preset manager uses the Tau Ceti module by alpha moonbase

**Can the Step Sequencer run without an Audio Analysis component?**
Yes — if no audio triggers are connected or BPM Mode is on, the sequencer clocks from the global BPM instead.

**How do I remove a MIDI mapping?**
Right-click the mapped element while in MIDI Map mode, or use **Remove All Midi Mappings** under the General tab to clear everything at once.

**What audio does Audio Analysis listen to?**
The audio input source is configured in the component. Use the Coarse Audio knob for input level and the FINE CTRL band settings (filter type, cutoff, resonance, rolloff) to isolate the frequency ranges you want to react to.

**How do I set up the XY Modulator to react to my sequencer?**
Add both a Step Sequencer and an Audio Analysis to the panel, and make sure **Create Automatic Mappings** is enabled. okVJ will wire the sequencer's gate output to the XY Modulator's trigger input automatically.

---

https://okvj.live/docs/
