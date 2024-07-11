# Preferences

## Intro

LightWave's preferences have been in the same shape since LightWave 6, with additions squeezed in where they made most
sense. We have reorganised how this panel is laid out in both Layout and Modeler, so that settings are more logically
arranged. The keyboard shortcuts of <shortcut>O</shortcut> and <shortcut>D</shortcut> still work as they did before.

Above the Search field, there is a Manage dropdown menu with five options:

![Preferences-manage.png](Preferences-manage.png){width="200"}{thumbnail=false}
* **Import Preferences** - Imports preferences for a single branch or a complete set.
* **Export All Preferences** - Export a complete set of preferences as a single .lwpref file.
* **Export Selected Branch** - Exports a single branch of preferences as a .lwpref file.
* **Reset All Preferences** - Sets preferences back to factory defaults.
* **Reset Selected Branch** - Kills just one branch of prefs so you can troubleshoot preferences problems.

Search field results will show you the page or pages that the word is on, but highlighting the search will be for a future version.


## Layout

![Preferences.gif](Preferences.gif)

### Current Scene

All settings in this group only affect the currently-loaded scene. Changes made here affect your scene immediately and are saved with your .lws file

### Other settings

Immediately affect any scene loaded, regardless if these settings were different when the scene was originally made. Settings are saved to 

> The UI magnification section on the Interface branch is PC-only. People with several screens at differing resolutions should continue to use the startup options in the icon arguments, as before. You can find those instructions [here](HiDPI-display-support.md).

### Defaults

Parameters changed here only affect scenes going forward. Changes will only be seen after clearing the scene. These changes are saved in the Preferences file.

## Modeler

![MPreferences.gif](MPreferences.gif)

Modeler Preferences is now in a single window, rather than the two from before. The same Manage and Search options are present. The same caveat for UI Magnification applies in Modeler.