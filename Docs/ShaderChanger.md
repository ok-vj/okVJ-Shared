# Shader Changer

A component that lets you pick shaders from a collection. Shaders are compiled on the fly, so you can keep a large library of simple content for very little VRAM cost — the number of shaders in the collection doesn't affect VRAM usage.

You can use the premade shader collections, or build your own (see [Writing a Shader](#writing-a-shader) below).

Why are so many of the shaders clown vomit colored?
It is made to run well with the multiRecolor component from okVJ that can recolor the shaders to a set color palette.

## Parameters

### Setup

| Parameter | Description |
|---|---|
| **Resolution** | Sets the output resolution. |
| **Shader Collection** | A component containing a collection of shaders, each stored in a Text DAT. |
| **Shader Index** | The index of the shader from the collection. Changing this value triggers a shader change. |
| **Names DAT** *(read only)* | A Table DAT listing the shader names. The second column contains formatted names (underscores removed) for display purposes. |
| **Current Shader Name** | The formatted name of the currently active shader. |
| **Pixel Format** | The internal pixel format of the TOPs. Should be 16- or 32-bit float, since many shaders rely on feedback. The final output is always 8-bit fixed, for performance. |
| **Debug Mode** | Adjusts compile behavior and enables the info DAT on the active GLSL TOP, making it easier to write or debug shaders. Shader and compilation info can be found in the operator "shaderInfo"|

### Uniforms

| Parameter | Description |
|---|---|
| **Audio Val** | An audio-reactive value (0.0–1.0). Link this to the output of an Audio Mixer or Audio Analysis, or from `okVJ_UI`. |
| **Trigger Val** | A trigger value (0.0–1.0) used for trigger effects. Link this to the output of a Step Sequencer, or from `okVJ_UI`. |
| **Time** | The time value. Use `absTime.seconds`, or the output of a Time Keeper, or from `okVJ_UI`. |
| **Use Manual XY** | If **off**, XY values are randomly generated on trigger from Trigger Val. If **on**, feed in your own XY values manually, or use the `okVJ_UI` XY Modulator. The premade shaders expects XY values in range 0 to 1|

### Post

A post-processing stack. Controls **HDR Brightness** and the **tone map** that converts the image from 32-bit float down to 8-bit fixed range.

---

## Writing a Shader

Write a shader for a GLSL TOP. If you don't override the built-in uniforms, you can use the preprocessors and uniforms provided automatically.

Put the shader's text in a Text DAT inside a Base COMP, then link that Base COMP to the **Shader Collection** parameter.

### Built-in Uniforms

```glsl
uniform int   u_triggerCount; // an increasing counter each time the trigger hits

uniform float u_time,
              u_audioVal,
              u_triggerVal,
              u_aspect;

uniform vec2  u_xyVal;

uniform vec3  u_xyValVelocity; // velX, velY, velMagnitude
```

### Built-in Defines

```glsl
#define prevFrame_tex   sTD2DInputs[0]        // previous frame, from a feedback TOP
#define u_resolution    (uTDOutputInfo.res.zw)
#define u_texelSize     (uTDOutputInfo.res.xy)
#define PI              3.14159
```