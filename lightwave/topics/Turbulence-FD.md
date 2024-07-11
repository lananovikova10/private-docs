# Turbulence FD

## Introduction
### Quick start

The best way to get started quickly is to load any of the example projects in the Examples sub-folder of your TurbulenceFD installation and experiment with the settings. To create a scene from scratch, follow the following steps:

1. Press Ctrl+P to open Render Properties or go to the Render Properties button on the Render tab. In there, go to the Volumetrics tab and check Use Legacy Volumetrics![UseLegacyVolumetrics.png](UseLegacyVolumetrics.png)
2. Select Add Container from the TurbulenceFD menu
3. To define the shape of your emitter
4. load an .lwo object
   1. or create geometry using Modeler, Layout's Modeler Tools/Geometry or the new Procedural Geometry tools
   2. or create a particle system using Items/Dynamic Obj/Particle
5. With the new object selected, choose Make Emitter from the TurbulenceFD menu
6. In the Channels tab of the Fluid Emitter popup, set Temperature to 1.0
7. Press the Start button in the TurbulenceFD main dialog
8. A dialog with a progress bar appears as the simulation is being computed.
9. After simulating, you can render the result

## Painting Fluid
![PaintingFluid.png](PaintingFluid.png){style="block"}
One important aspect of controlling a fluid simulation (if not the most important one) is to create the right emitter setup.

You can think of the emitter as a brush used to paint a pixel image. In fact, the container works pretty much like a 3D pixel image. You paint into one or more of the fluid channels (similar to painting into the RGB and/or A channels of an image) using emitters.

The fluid simulation will then add velocities that let your "paint" flow, curl and/or expand. Essentially the result will be what you painted at the source. You'll want to try various settings for the emitter texture scale, octaves and contrast. Maybe use several small objects instead of a single big one, use particles, animate the intensity of the emission, etc.

You can start by using only the temperature channel (disable the others) and see what different effects you can get just by varying the emission pattern and animation. You may not even need more than one channel for an effect - even in a high-quality production.

## Fire simulation
![FireSimulation.png](FireSimulation.png){style="block"}
Fire can be simulated in several ways. All you need is one or two fields as a basis to set up your fire shader, which is what you will most likely spend the most time with. You can even use the most straightforward density simulation and turn it into a nice flame by only using good shading parameters. The density-based flame example project shows how this works. See the next section for more details on shading fire.

There are several ways to get more control over your fire simulation. They are based on the Fuel channel. Objects can emit fuel that will burn if the temperature at a voxel is above the Ignition Temperature. When fuel burns, the air heats up and expands, as specified by the Expansion parameter. This is the essential control for explosions and large fireballs. Another effect of burning fuel is the Heat Creation and Density Creation. These parameters control how much is added to the temperature and density channels per unit of burnt fuel. Heat Creation is how a fire keeps itself burning, that is keeps the temperature above the ignition temperature after the initial ignition.

Fuel may move slower than the rest of the fluid. This gives you some additional control over the shape of the flames. So does the Fuel Diffusion parameter, which will essentially blur the fuel field, letting fuel spread slowly in all directions regardless of the movement in the fluid.

The Fire channel provides an alternative channel to render fire. Fire values are large wherever fuel burns and diminish the farther away from the burning fuel they are. This creates a field that allows you to shade the flame based on the distance to the flame core. The next section will go into more detail on shading fire.

## Shading fire
![ShadingFire.png](ShadingFire.png){style="block"}
From a visual perspective, fire is essentially hot gas and soot particles that emit light. Most flames consist mostly of soot which is Carbon. Carbon is what is called a Black Body. A Black Body absorbs all light that hits it, hence it is black. However, when its temperature rises to over about 600 Kelvin, it starts to emit light in a very characteristic way. This is where the familiar red/orange/yellow/white colors come from. Because fire mostly consists of soot particles, this is what dominates the color of flames.

Since soot particles emit the light of a flame, that means that the more soot particles there are, the brighter the flame will be. On the other hand, since Black Bodies also absorb light, more soot particles also make the flame more opaque. These two effects are exactly what is controlled by the Opacity group of the Fire Shader. This is what you use to control the shape of the flame.

To control the color you have two options. One is to specify a color gradient directly and the other is to use the physical model that describes the colors of a radiating Black Body. The latter will give you an easy way to obtain realistic colors, while the former gives you full artistic freedom. When using the custom gradient, take care that you use a high dynamic range of colors (also make sure that the Clamp checkbox is not checked). Look at the intensity values of the default color gradient as an example. It actually has a constant orange color. Only the intensity runs from 0% to 2000%.

As mentioned above, you can shade fire using several different simulation channels. The density-based flame example uses the temperature field to drive the color and the density channel for the opacity. While the fuel-based flame shows pretty much the same using the Fuel and Fire channels. The Fuel channel gives you more freedom to simulate a reaction, but it behaves the same when it comes to shading. In these examples, the mapping of the Opacity group creates the typical flame shape. A rising plume of fuel will only burn at the outer contour where there is enough oxygen. That means that most light is also emitted only from these areas. The mapping function curve exploits the property of Density and Fire fields with large values inside the plume/flame and smaller values outside. By creating a peak in the mapping you specify where the surface of the flame should be that emits most of the light. See the F-Curve editor for more details on how you can design mapping curves.

You can also use the Fire channel to drive the color, the opacity or both. You can even shade flames without using an opacity channel at all - note that in this case, you won't have alpha information to composite your flame later on. You can still composite such a flame by using the brightness of the flame as a matte channel - remember that the brighter the flame is, the more soot particles there are and the more opaque the flame will be.

