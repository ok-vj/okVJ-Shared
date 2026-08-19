# okVJ

`okVJ` is a toolkit for building interactive controls, scene systems, audio-reactive interfaces, presets, MIDI mappings, and other live-performance tools in [TouchDesigner](https://derivative.ca/).

Often when creating live performances, requirements change. Visions change. Deadlines are short. Technical requirements are not always fulfilled.

In order to build live performances powered entirely by TouchDesigner, we created `okVJ` as a toolkit.

It is a collection of the components we have needed and the components we reach for when preparing live shows. They are built to be modular and designed to fit different ways of organizing a set.

It is an evolving collection of tools that includes a UI builder, scene changer and shader changer - for creating content, FX racks for processing visuals, mapping tools, and more.

The toolkit is designed to make complex TouchDesigner systems easier to build, control, reuse, and perform with.

---

# Installation

Download the latest release using the green **Release** button.

Or clone the repository if you're feeling brave.

The repository contains the components.

Drag and drop the components you want to use into your TouchDesigner project.

We recommend starting with the `okVJ_UI` component and building from there.

---

# Design Philosophy

`okVJ` is built around a few principles.

## Ease of Use

Performing shouldn't involve a lot of menu diving.

It is easy to be stupid when performing. We are speaking from personal experience.

`okVJ` tries to limit your ability to do something dumb, so you can focus on performing well instead of focusing on not messing up.

**Too few parameters are better than too many.**

## Modular

Components should be useful independently, but should also work together as larger systems.

We don't want to dictate how you organize your TouchDesigner projects.

## Real Time Is King

Interactive systems should remain practical in real-time TouchDesigner projects.

They should run in real time.

## File Sizes Are Small

An often-overlooked benefit of procedural workflows is that entire project files can be developed across the world and passed back and forth over WhatsApp.

We aren't trying to demoscene this, but a project file should still fit on a thumb drive.

## Production-Oriented

The toolkit is designed around the needs of actual creative production rather than isolated demonstrations.

These are tools we use when making shows.

## Performative

Interfaces should work well for live interaction, including MIDI control, scene switching, presets, and audio-reactive workflows.

---

# okVJ_UI

`okVJ_UI` is the UI system at the center of the toolkit.

It provides a collection of reusable UI components and systems that can be combined to build interfaces for:

* Live visual performance
* VJ and audiovisual systems
* Installations
* Interactive media
* Generative graphics
* Audio-reactive systems
* Stage and show control
* Prototyping

The toolkit includes both simple controls and larger systems for managing scenes, presets, audio analysis, MIDI control, and shared parameters.

---

## Features

### Modular UI Components

Build interfaces from reusable components such as:

* Buttons
* Sliders
* Knobs
* Radio Buttons
* Hue Picker
* Notes
* OP Viewers
* XY Pads
* Preset Manager
* Audio Analysis and Mixer
* Step Sequencer
* And more

Components are designed to work independently while sharing a common structure and workflow.

### MIDI Mapping

Interactive parameters can be mapped directly to MIDI controllers with one click.

Mapping can also use non-MIDI CHOP sources, such as OSC or custom control systems.

### Preset Management

The toolkit includes preset functionality for storing and recalling UI states.

Presets can be recalled instantly or transitioned over time, making them suitable for both interactive tools and performance environments.

### Scene Changer

The Scene Changer provides a system for switching between complete custom scenes.

Scenes can be stored in Scene Banks and recalled quickly without rebuilding their state each time.

The system also includes configurable memory-management strategies and scene gating to help ensure that inactive scenes do not cook when they shouldn't.

A small preset manager is also included for quickly switching between different scene presets.

### Audio Analysis

Audio Analysis provides continuous values and triggers for:

* Low frequencies
* Mid frequencies
* High frequencies
* Total audio level

These values can be used throughout a project to create responsive visual and interactive systems.

### Audio Mixer

Audio Mixer combines the analyzed frequency bands into a controllable output.

This makes it possible to adjust the balance between low, mid, and high frequencies without hard-coding the mix into individual scenes.

### Shared Scene Parameters

Scene Banks can define parameters once and make them available to multiple scenes.

This allows a collection of scenes to share the same control system while remaining independent internally.

### Drag and Drop Connections

Many components support drag-and-drop connections directly in the TouchDesigner UI.

This makes it possible to build and connect systems without manually creating every parameter reference.

---

# Getting Started

A typical `okVJ_UI` project starts with the main UI component and one or more submodules.

Most submodules share a common structure:

* **COMMON** — General component settings
* **INTERACT** — Parameters controlled directly through the UI
* **VALUES** — Input and output values
* **FINE CTRL** — Additional control parameters
* **INPUTS** — Connections to other components
* **OUTPUTS** — Generated outputs
* **STYLE** — Visual styling

This common structure makes it easier to move between different components and understand how they are configured.

---

## Example: MIDI Mapping

1. Connect a MIDI In CHOP to the `midi_in` input.
2. Enter MIDI Map Mode.
3. Select the UI control you want to map.
4. Move a control on your MIDI device.
5. The UI control is now mapped.

MIDI mapping can also use other CHOP sources, allowing the same system to be used with OSC or custom control systems.

---

## Example: sceneChanger

The Scene Changer is designed for projects where multiple complete scenes need to be recalled quickly.

The basic workflow is:

1. Generate a Scene Bank using **Generate Scene Bank Comp**.
2. Build or connect your scenes inside the Scene Bank.
3. Make sure each scene provides a TOP named `out1`.
4. Connect the Scene Bank to the Scene Changer.
5. Change **Scene Index** to switch scenes.

Scenes can share common inputs defined by the Scene Bank.

The Scene Changer also provides configurable memory management for projects where VRAM usage is an important constraint. and a little preset manager, to recall presets of the scenes. 

## Examlpe: shaderChanger

a collection of lightweight simple audioreactive shaders that can be used as texture layers to drown in effects, or to mix in and out of scenes with.

---

# Documentation

The documentation covers the common systems and individual components included in `okVJ`.

Documentation is included in the repository and is intended to grow alongside the toolkit.

**Documentation contributions are especially welcome.**

---

# Contributing

Contributions are welcome, especially documentation.

If you find a bug, have an idea for an improvement, have a feature request, or want to contribute a component or documentation update:

1. Check the existing issues and documentation.
2. Open an issue describing the problem or proposal.
3. For code or documentation changes, open a pull request.
4. Include enough context for others to understand the change and test it.

We are particularly interested in contributions that make the toolkit easier to understand, use, and maintain.

---

# License

`okVJ` is released under the **MIT License**.

You are free to use, modify, distribute, and incorporate the software into your own projects, including commercial projects, subject to the terms of the license.

See [`LICENSE`](LICENSE) for the complete license text.

---

# TouchDesigner

`okVJ` is built for [TouchDesigner](https://derivative.ca/), the real-time visual development platform by Derivative.

---

# Status

`okVJ` is an actively developed toolkit.

It is an evolving collection of tools, and some components or documentation may be experimental, incomplete, and subject to change.

If something is broken, unclear, or missing, please let us know.

---

# Credits

Developed by **supermarket_sallad** and **VJ_BunBun**.

Built with TouchDesigner.

Special thanks to **jetXS (Michel Didier)**, who has helped us a lot during development.

---

**If you build something with `okVJ`, we'd love to see it.**
