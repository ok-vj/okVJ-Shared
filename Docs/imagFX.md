# IMAG FX

These effects were originally developed for use with IMAG, but they can be used for regular content.

---

## fluidLike

Runs a 2D shallow fluid sim. Uses optical flow to construct the input vectors.

### Setup

| Parameter | Description |
|---|---|
| **DRY/WET** | The dry/wet mix of the effect. |
| **Data Downsample** | How much to downsample the input for optical flow. |
| **Reset** | Resets the sim. |

### Params

| Parameter | Description |
|---|---|
| **Falloff** | The falloff of the colors. |
| **Luma Weight** | Brings in more of the input over the displaced color, based on luminance. |
| **Input Velocity** | The strength of the input velocities. |
| **Vorticity** | The curliness of the fluid sim. |

### Fine Ctrl

| Parameter | Description |
|---|---|
| **Sub Frame Passes** | The number of times the fluid sim runs each frame. |
| **Vertical Grid Scale** | The scale of the fluid sim grid. The horizontal scale is based on the aspect of the input. |

---

## jumpFloodFX

Uses David Braun's JFA component to create jump flood effects.

| Parameter | Description |
|---|---|
| **DRY/WET** | The dry/wet mix of the effect. |
| **Threshold** | The threshold of the input. |
| **Original Img** | The amount of the original image underlaid beneath the output of this effect. |
| **Edge Color / Edge Alpha** | The color (and alpha) of the edge. |

---
## sillyDither
## sillyDither
Creates a dither effect based on a physics sim.

| Parameter | Description |
|---|---|
| **DRY/WET** | The dry/wet mix of the effect. |
| **Vertical Grid Count** | The scale of the sim grid. The horizontal scale is based on the aspect of the input. |
| **Reset** | Resets the sim. |
| **Temporal Smoothing Radius** | Sets the smoothing over time. |
| **Velocity Decay** | A higher value means the velocity decays faster. |
| **Min/Max Radius** | The minimum and maximum radius. Gets divided by the grid scale. |
| **Home Force** | How much each point moves toward its original position. |
| **Repulsion Force** | The strength of repulsion between points. |
| **Original Color** | Multiply the points by their original chroma. |
| **Circle Radius** | The radius of the circles — not accounted for in the sim. |