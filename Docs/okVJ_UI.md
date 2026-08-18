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

INPUTS
Some components take inputs from other sub-modules in the okVJ_UI, and they only have full functionality if they have something referenced to their inputs.
if ** Create Automatic Mappings ** is toggeled, the component will search the okVJ_UI and create automatic references. This is toggeled on by default.


---------
SUBMODULES
------------

## Audio Analysis
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



## Audio Mixer
A component that allows you to channel mix the analyzed audio values. So you don't need to hardcode low/mid/high in your scenes. It can be changed on the fly

Interact from the UI:
    from left to right - low - mid - high attenuation

INPUTS:
    by default maps from audio analysis component
    Low, Mid, High Val

INTERACT:
    low - mid - high attenuation

OUTPUTS:
    Audio Val - the sum of low mid high post attenuation.

## Buttons
    simple buttons, momentary or toggle

SET UP:
    Max per line: the amount of buttons before it swaps line. if you want 8 knobs on 2 lines - set max per line to 4

    Spacing (px): set the spacing between operators in panel units (px)

Button Mode: Set buttons to toggle or momentary

Styling:Set styling of button

Values:
    The input and output values and parameters of the buttons
    parameter name: Buttons{i}press

## Hue Picker
    an HSV Selector
Interact:
    Hue, Saturation, Value

Outputs:
    RGB - hsv value in rgb
    drag from the hue selector to drop the RGB parameter 

Fine CTRL:
    Hue Range - select a specific part of the hue spectrum to isolate
    Hue steps - the amount of steps in the hue
    Smoothing - the smoothness (filtering) of the change
    
    

## Knobs
    a bank of rotary knobs

SET UP:
    Max per line: the amount of buttons before it swaps line. if you want 8 knobs on 2 lines - set max per line to 4
    Spacing (px): set the spacing between operators in panel units (px)
    Reset Val - the value that resets by right clicking

Styling:
    Set styling of button

Values:
    The input and output values and parameters of the buttons
    parameter name: Knobs{i}val

## Notes
    A component to type and display notes

## opViewer
    Display any OP from touchdesigner
    Toggle interactive to make it interactive

## paletteGenerator
    (slightly depreciated)
    generate a color ramp from a base color and harmonies

    select a base color with the hsv selector.
    toggle different color harmonies with the buttons.

## Radio Buttons
    a collection of radio buttons.
    only one of the buttons can be selected at the time - outputs a zero indexed integer index about what button in currently on.

SETUP:
    Max per line: the amount of buttons before it swaps line. if you want 8 knobs on 2 lines - set max per line to 4

    Spacing (px): set the spacing between operators in panel units (px) 
    Styling:Set styling of button

    DAT Table:
        link a dat table. it will create buttons based on table.numRows
        the content of each row will fill the labels.

        Toggle * exlude fist row *  if you have a header

        Collumn index: which collumn to read a label from

        You can also drag and drop a dat table or DAT parameter object to the UI

        You can also drag a menu parameter from touchdesigner, and it will create a dat table for it.
        NOTE: if you drag a menu parameter - this will not update if the menu parameter updates

    Drag from any button to get the Index parameter

## Sliders
    A collection of sliders

    Spacing (px): set the spacing between operators in panel units (px)
    Orientation: the orientation of the slider
    Reset Val - the value that resets by right clicking

VALUES:
    The input and output values and parameters of the buttons
    parameter name: Sliders{i}val
    
    
## stepSeq
 INPUTS: Audio Triggers low mid high total
    by default linked to the audio analysis component

## timeKeeper
    





