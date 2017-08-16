# PCB

* [Library Framework](#library-framework)
* [Schematic Draft](#schematic-draft)
* [Value and Partno](#value-and-partno)
* [BOM](#bom)
    * [Firefox Browser Extension](#firefox--browser-extension)
    * [RunWith](#runwith)
    * [Buttonize Digi-Key Part Number](#buttonize-digi-key-part-number)
* [Finalize Schematic](#finalize-schematic)    
* [Finishing Board](#finishing-board)   
* [View in Gerbv](#view-in-gerbv)
* [Text API](#text-api)
    * [Side note on LineBreak](#side-note-on-linebreak)
* [File API](#file-api)

## Library Framework

We use this framework of library folders:
* Eagle
* Projects
* Ex

## Schematic Draft

Draw schematic draft:
* Find as much components (with correct footprint) as you can.
* [Which Oscillator Output Signal is Best for Your Application?](http://blog.bliley.com/selecting-the-best-signal-type-for-your)

## Value and Partno

Based on partlist and BOM excel sheet:
* use: `D:\EAGLE-Tools\bom-ex\value-partno\write-sheets.js`.

## BOM

Two websites: https://octopart.com/, DigiKey

### Firefox Browser Extension

Please refer to:
* [Your first extension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Your_first_WebExtension)
* To install: Open `about:debugging` in Firefox, click `Load Temporary Add-on` to select your extension.

### RunWith

Please refer to:
* [Runs the selected string as a command line parameter of a local program via right-click or Tools menu.](https://addons.mozilla.org/en-US/firefox/addon/runwith/)
* This method is deprecated: as it is not compatible with new version Firefox.

### Buttonize Digi-Key Part Number

We copy/modify example of "native-messaging":
* [Example extensions](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Examples)
* D:\EAGLE-Tools\bom-ex\runwith-native-messaging\add-on-new: `manifest.json`
* --- background.js: connect to `ping_pong` app
* --- find-dknumber.js: `buttonize` Digi-Key part number.
* Windows Registry for ping_pong app:
* --- [App Manifest Location](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_manifests#Manifest_location)
* --- D:\EAGLE-Tools\bom-ex\runwith-native-messaging: `ping-pong.reg`
* D:\EAGLE-Tools\bom-ex\runwith-native-messaging\app: `ping_pong.json`
* --- which calls: `ping_pong_win.bat`
* --- which calls: `D:\EAGLE-Tools\bom-ex\Grab-Bag-master\Bom-ex\new-addDKPartToBom-ex.py`
* --- which adds to: `D:\EAGLE-Tools\bom-ex\*-db.txt`

> **Note**: to jump to a given line number, you can directly use:
> `$text->setCurrentLineNumber($x);`.

## Finalize Schematic

Finalize schematic:
* Collect all components to `D:\EAGLE-Tools\bom-ex\*-db.txt`
* Replace components with correct attributes: `value`, `PARTNO` (manufacturer)
* `PARTNO` (manufacturer) is the keyword for matching items in database
* Check with `D:\EAGLE-Tools\bom-ex\mybom-ex.ulp`: click `Load DB`

## Finishing Board

Please refer to:
* [How to change font size throughout brd](https://www.element14.com/community/thread/31231/l/how-to-change-font-size-throughout-brd?displayFullThread=true)
* [How do I change all fonts to vector on the same PCB at once?](https://www.element14.com/community/thread/18176/l/how-do-i-change-all-fonts-to-vector-on-the-same-pcb-at-once?displayFullThread=true)

To smash all the parts, try:
* display none tOrigin bOrigin;
* group all;
* smash (>0 0);
* display last;

To change the font and ratio, try:
* display none tNames bNames;
* group all;
* change font vector (>0 0);
* change size 40mil (C>0 0);
* change ratio 15 (>0 0);
* display last;

## View in Gerbv

Please refer to:
* [drill layer wrong size](https://www.element14.com/community/thread/55005/l/drill-layer-wrong-size?displayFullThread=true)
* Right click main.drd layer, and select `Edit file format` dialog.
* Turn off auto detect and set 5 digit.

## Text API

One of the main entity:

> **Important**: `lines` is an array of string stripped from their line break
> character.

If you need to manipulate a simple string you can use `Text::fromString`:

> **Important**: please note that upon creation, the current line number is
> initialized to the first line: `0` (array indexed).

### Side note on Line Breaks

A `StringUtil::detectLineBreak` method is used to find the line break, this is
done using the following rules:

* `\r\n` for windows
* `\n` for any other operating system
* `PHP_EOL` if no line ending has been found

## File API

The other main entity:

## Next readings

* [Vocabulary](04-vocabulary.md)
* [Extending](05-extending.md)
* [Exceptions](06-exceptions.md)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
