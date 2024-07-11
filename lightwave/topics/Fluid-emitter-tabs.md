# Fluid Emitters Panel

![TFD-Emitters.png](TFD-Emitters.png){width="600"}

<tabs>

<tab id="general" title="General">

![General tab](Emitter-general.png){width="600"}

- **Mode** - Specifies if the object emits at all and whether the object's children emit.
- **Disabled** -Do not emit anything. This can be useful when testing various combinations of emitters.
- **Single Object** - Emit only from the object itself, not from its children.
- **Include Children** - Emit from the object and its children.
- **Radius** - If Fill Object is not checked, the emitter will affect voxels in a region around the surface of the tagged object(s). If the radius is smaller than the voxel size of the fluid container, aliasing artefacts may occur. This can result in the emission to have gaps or disappear entirely. TurbulenceFD does not anti-alias the emission in order to make the simulation and shading results more robust against changes in voxel size.
- **Collision Object** - If checked, the object will act as an obstacle to the flow. The fluid will have to flow around it. A moving collision object pushes the fluid around. There is a special requirement for the geometry to work as an obstacle. To sample the object geometry on the voxel grid, the simulation has to determine whether a voxel is inside the object and or outside of it. A simple plane does not work for that reason - it doesn't have an "inside". Instead, you would have to create a wall using a scaled box. All parts of the object have to be large enough to cover at least one voxel. Structures thinner than the voxel size will not be resolved properly on the voxel grid.
- **Fill Object** - If checked, the tagged object(s) will be filled with the values specified in this tag. Otherwise, the values will be set only in a region around the surface of the object(s). There is a special requirement for the geometry to work as a filled emitter. To sample the object geometry on the voxel grid, the simulation has to determine whether a voxel is inside the object and or outside of it. A simple plane does not work for that reason - it doesn't have an "inside". Instead, you would have to create a wall using a scaled box. All parts of the object have to be large enough to cover at least one voxel. Structures thinner than the voxel size will not be resolved properly on the voxel grid.
- **Particle Property** - When using particles as emitters, you can modulate the emission intensity by any of the particle properties like Age, Mass, etc. This is highly dependent on PFX Emitter "Output size" and other settings as they feed this property.
- **Particle Randomization** - Adds noise to the particle property before mapping it to an emission intensity using the f-curve below. Some properties may be initialized too uniformly across all particles. You can use this parameter to break up the uniformity.
- **Intensity** - The F-curve allows you to customize the emission intensity based on the value of the particle property chosen from the drop-down box above.
 
</tab>

<tab id="texture" title="Texture">

![Texture tab](Emitter-texture.png){width="600"}

* **Surface Texture** - Use a texture on this parameter to control intensity of the emission across the surface of the emitter. This will control the emission within the band around the surface. For filling the inside of the emitter, only the procedural texture parameters below are used.
* **Volume Texture Scale** - The scale of the 4D noise texture that is applied to the emitter. The thumbnail on the left shows a preview of the noise as you change the settings.
* **Volume Texture Octaves** - The number of noise octaves for the texture. Each additional octave adds another, smaller scale of noise, while keeping the larger scales.
* **Volume Texture Contrast** - The lower the contrast value is, the more the noise texture will fade to a constant gray. A high contrast value makes the texture intensities vary less smooth.
* **Volume Texture Speed** - The noise texture is animated over time. You can see the animation in the preview thumbnail as you move through the timeline. This value specifies how fast the texture is animated.

</tab>

<tab id="force" title="Force">

![Force tab](Emitter-force.png){width="600"}

* **Velocity Scale** - Provides a method of changing the scale of the velocity of fluid emission. This setting works in conjunction with the Container> Simulation>Velocity Tab.
* **Velocity Weight** - When using particles as emitters, the particles can drag the fluid along their trajectory as they move. The larger this value, the more the particles will affect the fluid velocity.
* _Note that vice versa, you can also let the fluid drag along the particles by using the Particle Velocity Scale parameter (see Velocity)._
* **Normal Force** - The force that the object exerts on the fluid into direction of its surface normal. Normal Force requires more simulation time than the Direction Force below. It should be preferred for planar emitters that have the same normal everywhere like a plane or disc.
* **Direction Force X, Y, Z** - Emit a force that points into the direction specified here. While the Normal Force may change its direction across the emitter's surface, the Directional Force is not affected by the emitter's surface Normals.
* **Pressure** - Pressure can make the fluid expand or contract as it would in an explosion or black hole. Positive values cause expansion, negative values cause contraction.

</tab>

<tab id="channels" title="Channels">

![Channels tab](Emitter-channels.png){width="600"}

There are two ways how channel values (temperature, density, fuel, burn) are added to the fluid.

* **Add** - the object will emit the value set in this field, per second.
* **Set** - the channel values for the object will be held constant the value set in this field.

To understand the difference, think about temperature. Using Set mode, you specify the temperature the object has. Using Add mode, you specify by how much the object will heat up the fluid every second. In the later case, if the fluid wouldn't carry away the heat around the object (e.g. Buoyancy is 0), it will continue to heat up the fluid infinitely. While in Set mode the value stays constant.

Temp./Dens./Fuel/Burn

The value emitted per second (in Add mode) or to be set constant at the object (in Set mode). Each of these can be animated using envelopes.

</tab>

</tabs>
