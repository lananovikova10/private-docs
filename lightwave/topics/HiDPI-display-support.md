# HiDPI display support

As LightWave transitions to a resolution-independent user interface, methods have been put in place to scale parts of
the user interface using LightWave's existing graphics toolkit (how the user interface looks) for bigger screens. For
macOS, such scaling is specified by the Displays category of System Preferences.

For Windows machines, if you don't have two displays at the same resolution, Windows 10 has per monitor scaling for
elements:

![Windows10_Font-Scaling.png](Windows10_Font-Scaling.png)

In Windows 7 and 8 there is only a general Display scaling window that can lead to text being too small on one screen
and overblown on the next:

![Windows_Font-Scaling.png](Windows_Font-Scaling.png)

![Windows8_Font-Scaling.png](Windows8_Font-Scaling.png)

LightWave 2024 has the following Screen Scale argument when launching Layout and/or Modeler:

`--ui_screen_scale_factors=2;1`

The above code will add a scaling factor for a two-monitor system where the first monitor is UHD at a resolution of 3840
x 2160 and the second monitor is HD at a resolution of 1920 x 1080

While title bars and other windows will still be small on the above multi-monitor display, LightWave UI elements will be
sized correctly on this 2560*1440 screenshot:

![Windows7_grab.png](Windows7_grab.png)


> This page is a part of continuing efforts to make the LightWave documentation complete
> {style="note"}