# okVJ fxStacks

## General for These FX Stacks

### FX Stack

- **Enable/disable effects** — Toggle individual effects on or off in the FX Stack.
  - Toggling forces a shader recompile. Compilation is threaded, so this is safe to do live — but for smooth live mixing, prefer adjusting the **Amt** sliders instead of toggling effects on/off.
- **Order** — Sets the sequence in which effects are applied within the stack.
  - Higher values = applied later in the chain.
  - Changing order also triggers a recompile.
  - If two effects share the same order value, the resulting order is unpredictable (though it will not cause runtime glitches).
- **Amt slider** — Each effect has an `Amt` slider controlling its strength/intensity.

### Masking

- A monochrome mask can be linked under the **MASK** tab.
  - Uses the mask's **red channel**.
  - White = effect at full strength; black (0) = effect not applied; values in between are interpolated.
- **Mask Strength** slider — controls the overall influence of the mask.

### Fine Control

Under **FINE CTRL**, additional variables can be adjusted:

- **General Variables** — e.g. `Time`, `Seed`
- **Per-effect fine controls** — additional parameters specific to each effect in the stack

---

## displacementFXStack

| Effect | Description |
|---|---|
| **noiseDisplace** | Displaces the input image using a noise field. Noise parameters are configured under **FINE CTRL**. |
| **noiseItter** | Iteratively displaces the input image using a noise field, applied over multiple steps. Noise parameters are set under **FINE CTRL**. More iteration steps = better quality, but more expensive to compute. |
| **lumaDisplace** | Displaces the image based on the slope (gradient) of its luminance. |
| **painterlyLuma** | Creates a painterly effect by iteratively displacing the image, weighted by its own luminance. Iteration steps are set under **FINE CTRL**. More iteration steps = better quality, but more expensive to compute. |

---

## glitchFXStack

| Effect | Description |
|---|---|
| **horSlices** | Creates horizontal slices. Slice size can be set under **FINE CTRL**. |
| **vertSlices** | Creates vertical slices. Slice size can be set under **FINE CTRL**. |
| **scanLines** | Creates lines emulating scanlines on VCR displays. |
| **chromaShift** | Chromatic aberration with lens distortion. |
| **lumaShake** | Shakes the image with amplitude based on luminance. |
| **strobeGlitch** | Creates glitchy offsets that sometimes invert, based on a seed (set under **GENERAL VARIABLES**). Inversion can be turned off under **FINE CTRL**. |
| **decimate** | A quadtree pixelation effect. Outline strength, max depth, and fractal dimension can be set under **FINE CTRL**. |
| **sliceUV** | Creates a clamped UV. Direction can be set under **FINE CTRL**. |

---

## toonFXStack

> `toonFXStack` has a hardcoded FX order — this allows outlines and halftone to be used at the same time.

| Effect | Description |
|---|---|
| **posterize** | Creates a posterization effect. Number of posterization steps is set under **FINE CTRL**. Also under **FINE CTRL**: "Posterize Random Chroma" applies a random color to each posterization step — can be used together with **multiRecolor** for clean recolorization (seed also configurable there). |
| **outline** | A Sobel edge effect — follows posterization in the order. Edge color can be set under **FINE CTRL → Outline Color**. |
| **Halftone** | A halftone effect, applied in parallel with the edge — follows posterization. Grid scale can be set under **FINE CTRL**. |
| **Only Outline** | Displays only the outline. |
| **mirror and flip** | Mirrors and/or flips the image. |

---

## Feedback FX Stack

Creates feedback effects, trails, and feedback warps.

- **Feedback Amt** — sets the amount of feedback trails.
- **Warp Amt** — sets the amplitude of the warp.

### Warp Settings

- **Noise Type** — the type of noise that creates the warp.
- **Vector Mode** — how the noise vector is constructed:
  - `offsets` — regular RGB noise
  - `sinCos` — `v = vec2(sin(noise), cos(noise))`
  - `curl` — curl noise
- **Composite Mode** — sets the composite mode used in the feedback:
  - `over` — the input gets alpha-composited over the previous frame
  - `under` — the input gets alpha-composited under the previous frame
  - `balancedMix` — the sum of input strength and "Feedback Amt" equals 1
- **Feedback Transform** — sets transforms applied each frame; these values are delta-timed.

### Settings

- **Feedback Precision** — sets the precision of the feedback passes. 16-bit float is usually sufficient and performs better than 32-bit float.
- **Time Step** — the time step of the component. Set to `1.0/me.time.rate`, `absTime.stepSeconds`, or something custom.

---

## strobeFXStack

> This component requires certain inputs to work correctly, set under the **Inputs** tab.
> Link a CHOP value to **StrobePulse1**, **StrobePulse2**, **Low Audio**, and **High Audio**. These values should be in the range 0–1.

Each strobe style has a menu to choose which of these inputs it uses. Some strobe styles also have a **Strobe Type** menu:

- `onStrobe` — the value is full when the input == 1
- `blackStrobe` — the input is inverted

| Effect | Description |
|---|---|
| **Base Strobe** | A basic strobe. |
| **Invert Strobe** | Inverts the colors on strobe hit. |
| **Sobel Strobe** | Keeps an outline of the colors while the strobe is off. |
| **Bloom Strobe** | Strobes a bloom effect. |
| **Smear Strobe** | Smears the input image on strobe hit — good for kicks. |

---

## COMPOSITOR

Used to composite several layers.

- Add more layers with the **sequence** button — the component will show more or fewer inputs accordingly.
- Uses **alpha blend (over)** by default; layer order is set via **z-index**.

| Parameter | Description |
|---|---|
| **Opacity** | Sets the opacity of the layer. |
| **Warp Mask Contribution** | Sets how much this layer warps the other layers, based on luminance. |
| **z-index** | Sets the order — a higher number means the layer is more in front. |

### Composite Modes

**Difference** and **Darken** have sliders and can be applied continuously rather than discretely. These two modes only apply to layers that have opacity.

**Darken** mode (configured under **FINE CTRL**) has three sub-options:
- **Luma Compare** — compares luminance and picks the darkest layer
- **Minimum** — takes the minimum of the layers
- **Multiply** — multiplies the layers

---

## multiRecolor

Takes an input and recolors it according to a palette. The palette is defined via rampKeys from a **rampTOP**. It looks up the hue and saturation from the input image and remaps them to a color from the palette.

| Parameter | Description |
|---|---|
| **DRY/WET** | The amount of recoloration. |
| **HSV Rotate** | Rotates the color lookup ramp; "reset position" resets the color rotation position. |
| **rampKeys** | Link a DAT from a rampTOP. Colors don't need to have dark values — hue and saturation can be set here, but the component uses the *value* from the input image. |
| **Primary Weight** | The first color of the ramp is the primary color; sets how much influence it has over the output. |
| **Pre Saturation Boost** | Boosts saturation before lookup. |
| **Post Saturation Boost** | Boosts saturation of the output. |