okVJ_UI
This documentation is incomplete and sometimes out of date, we are working on it. If you find an problem in the docs please raise an issue on GitHub, and we will get it fixed. We'd be very grateful for your contributions on this.

okVJ_UI submodules:

common for all modules:

DRAG AND DROP

Common UI interactions:
move bar - line on top, drag to reposition in the UI.
x - press to destroy sub module
hamburger menu - open parameters for this submodule
+/- add or remove an operator inside the submodule.

STYLE page
Matches the okVJ_UI style page by default.
Toggle "Match UI" to set style individually for this submodule

COMMON page:
Edit Mode: read Only - tracks the state of UIs edit mode
Include in Preset: toggle to include in the preset manager
Page: which okVJ_UI page the element is displayed on
Show on all pages: toggle to show on all pages

INTERACT PAGE:
Contains the values that can be interacted with from the UI

VALUES PAGE:
the interactable values on sliders, buttons and knobs. both inputs and outputs.

OUTPUTS:
the outputs from the sub module

FINE CTRL:
special tweakable parameters with more fine controls
---------
SUBMODULES
------------

##Audio Analysis
Analyses audio and turns it into 4 float values and 4 triggers. low mid high and total.
Interact from the UI:
* main slider: sets the main attenuation
* trigger threshold low - mid - hig - total: sets the threshold, when audio crosses this threshold the corresponding trigger fires.
* drag and drop - drag from the audio bars to get the audio val (float) of the corresponding filter. drag from the spectrum triggers to get the trigger of the corresponding trigger.

PARAMETERS:
Interact: the parameters that can be set from the UI

FINCE CTRL:
Normalize Audio - normalize the input audio to 0-1 range, messes with fidelity a bit, but makes it easier to deal with volume changes, since it gets normalized.
Threshold - the threshold over which the normalizeation kicks in, keep above 0 to avoid a division by 0


Filter:
Three bands of filters one for each.
"Filter" - menu of filter type - low pass, band pass, high pass etc
Filter cutoff in hz
filter resonance
Rolloff - steepness of filter in db per octave
Attenuate - attenuation post filtering and RMS

Smoothing - the smoothness of the signal

OUTPUTS:
low, mid, high, total val - float value of analyzed audio
low, mid, high, total trigger - the trigger when the analyzed audio crosses the corresponding trigger threshold





