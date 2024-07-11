# A quick guide to workflow with TurbulenceFD

LightWave Layout is well known for allowing an artist to take many different routes to reach an end result. TurbulenceFD, because of how its various components work together, allows for a very flexible workflow. Generally, there is a basic "start to finish" path which we will discuss here, but there are things that should taken into consideration prior to starting a scene that will make use of TurbulenceFD.

## Basic Workflow Concepts - before you start!

Animation of objects in your scene should in most cases be undertaken first, but when TFD is going to be used, your shot or scene design needs to be considerate of a few initial factors.

One of the first considerations is how much an object, ie an emitter/collider or a ParticleFX emitter, moves and how far, over the course of your animation in terms of XYZ space. The reason for this comes down to the minimum TFD Fluid Container size required, the voxel resolution needed for a Fluid Container to encapsulate the fluid being emitted by your emitters, and any wind or pressure considerations that push your fluid around the container all while not clipping the boundaries of the container itself. Furthermore, one must also take into account how many fluid channels will be needed to calculate accurately the effect you want to simulate, within the CPU/GPU and disk space limitations that you have based on your computer system.

Another consideration is how you want your object to emit a fluid. More precisely speaking, through the use of masks applied to an object so that fluid channels emit from a specific portion of the object rather than all of its geometry. If for example, you want to have the tip of a torch or a portion of a floor or wall burning or smoking or a combination of the two, you will need to prepare your object for this either by creating a separate geometry layer that will just emit fluid, or by creating a UV texture that has a white (or greyscale) image applied to it for the area of the object that will emit fluid. We cover this process in our examples so please make sure to check those out.

Finally, object preparation is an important consideration when working with TFD for the purposes of optimization. Lower polygon count objects and objects that are "frozen" or tripled, rather than quads with sub patches - will perform better when it comes to simulation speed. The reason for this is that TurbulenceFD works to create simulations based on the OpenGL polygon evaluation of an object surface or ParticleFX particle emitted, plus a "radius" or distance from the polygon surface or particle point as set in the Emitter Panel. Essentially, low-resolution proxy objects are going to work better for simulation speed than high-poly objects. LightWave Modeler provides tools for doing polygon reduction and there are excellent third-party tools such as Mootool's Polygon Cruncher that work directly with Modeler or in stand-alone mode that can make quick work of doing polygon reduction while retaining a highly-accurate degree of the shape of an object. This is important for things like surface collisions of fluid or emission of fluid along the surface of the proxy object, closely matching a higher resolution version that would be used in your rendering.

Now that these considerations are in mind, let's walk through a quick set up of a scene that makes use of TurbulenceFD. We won't be getting too fancy here, just something simple.

## Starting with a Fresh Scene

Starting with a fresh scene working in LightWave Layout, we will want to hit ctrl+p to bring up the Render Properties Panel. In the tab labelled "Volumetrics", look for a button in the volume integrator settings, called "Use Legacy Volumetrics" and enable it. For now, TurbulenceFD is classified as a Legacy Volumetric Effect and we need to use this setting for TurbulenceFD to visibly render in VPR, F9, F10 or network renders.

![Layout_2023-11-20_11-51-54.width-500.png](UseLegacyVols.png)

Now that we have this enabled, we can move on to creating our scene.

## Emitters

We need some objects to be emitters and collision objects. In the example below, we have used Procedural Geometry to create a ground plane using the Grid Geometry node (set Scale to X=1000 and Z=1000); a cube reshaped to make a flat blocker (set Scale to X=20, Y=300 and Z=200) and two spheres. A collision sphere at default size and an emitter at 500 mm.


![SimpleStarterSceneGeometry.png](SimpleStarterSceneGeometry.png)

Next, let's set our emitter to a metre above the ground, animate the other sphere and the box over the course of 400 frames. Move your objects around, thinking of where you want your simulation to eventually be.

![preview2-15.gif](preview2-15.gif)

Now that we have some animation on these two collision objects, let's set them up as TFD Emitters.

There are two ways to tag the objects as TFD emitters. The easiest way is - with one of the objects selected - go to the TurbulenceFD tab at the top of your interface in Layout and look for the button that says Make Emitter. We will do this with the smaller sphere. The other way is to hit the properties button (p) with the object selected, go to the "Appearance" Tab and from the Add Custom Object Dropdown, select Fluid Emitter. For now, though, we will just use the button on the TFD Menu list. Doing so should bring up the Fluid Emitters window with the object listed in the section under Object Name. In our example, that is the Sphere object. In the displayed General Tab, the defaults are pretty good here but we may want to enable Collision Object, depending on what your animation is doing. So we will do that here as well.

Next, let's select the Cube object and choose the button, Make Collision from the TFD Menu panel in Layout, then the bigger sphere. This will add the cube and sphere to the list of objects in the Fluid Emitters window and you will notice that it is already set with the "Collision Object" button enabled. Now let's do the same with the ground plane. At the end of this step, you should see something similar in your list.

![AddingEmittersCollisionObjects.png](AddingEmittersCollisionObjects.png)

For this next step, let's select the smaller emitting sphere in the Object Name list and then move through the panels as we set it up to emit fluid.

In the Texture Tab, we have five settings, broken up into two areas. The first is called "Surface Texture" with a default of 100% and you will notice it has a value mini-slider to the right of it and an E for envelope, and T for texturing. Should you wish to make use of these functions and want to learn more, we have some example scenes that work with these properties for you to check out. For now, though, the settings we are interested in are in the second section. Let's change Volume Texture Scale to a higher value such as .5m (500mm). You will notice that the white preview of the texture has now become partially covered with gray or darker areas, similar to how the Turbulence texture looks, part of the reason why this tool is called TurbulenceFD. This pattern is what will be "wrapped" around your object as a Fluid emission surface area. The brighter areas will emit fluid at 100% of the value setting in the channels tab, with darker areas going down to black at 0%. If you want to see what this pattern actually does over time, you can scrub through your timeline with the Fluid Emitter window open and the preview box area will change.

You can play around with the contrast, octaves and speed settings to see what they do to the preview box area and get an idea of how that will affect fluid emission from your object.

![SphereTextureTabSettings.png](SphereTextureTabSettings.png)

Next up is the "Force" Tab. We'll set the Velocity Scale to 900.0 for this example, but you can look for a setting called "Pressure" and change that from the default of 0.0 to something much higher. You can even put an envelope on it and make use of a channel modifier like "Noisy Channel".

![SphereForceTabSettings.png](SphereForceTabSettings.png)

Next, we need to emit some fluid. For that, we will go to the Channels tab. To keep things simple for this example, we will set "Temperature" and "Density" to 1.0. Leave all other settings as their defaults.

![SphereChannelTabSettings.png](SphereChannelTabSettings.png)

Once you have these settings entered, we can move the Fluid Emitters window off to the side or even close it. We can come back to it later if need be. It's time to set up our Fluid Container!

## Containers

As with Fluid Emitter tags being applied to an object, there are two ways to create a Fluid Container. Fluid Containers in general are really just null objects with the Custom Object Fluid Container tag in the Appearance Tab of Object Properties. Let's take the short route to make a container and simply hit the "Add Container" button in the TurbulenceFD menu. When you hit this button, a "Build Fluid Container" window will pop up with a Title text entry field pre-filled for you with "Fluid Container". You can change this name to whatever you want and then hit the "Ok" button.

Once you do that, you should be presented with something similar to the image below, but we will need to change the settings and placement of the container.

![DefaultFluidContainerSettingsApperance.png](DefaultFluidContainerSettingsApperance.png)

As you can see, the default creation Fluid Container settings have placed the white wire frame "cube" directly in the center of the scene and it is too small to encapsulate our objects. We need to fix this as well as change some other settings immediately. Since we know our ground plane object is 5m x 5m, let's increase the "Grid Size" in this panel to match X and Z, and we will obviously need some height so let's set each value to 5m. This will give us a 5m x 5m x 5m "Fluid Container". We will also need to provide a Grid Offset value in the Y axis. To get the container to essentially rest on the ground plane, let's use Y=2.5m. 

Make sure Layout is in Textured Shaded Solid mode (any other will do, just not VPR). Hit Start in the Container window and wait for it to end. You can speed up calculations by turning off the Update button. This will give us a first look at our fluid dynamics.

Once you have look at the mesmerising blue-green swirls, change the voxel size to 10mm to match our emitter and collision objects. 

![FluidContainerRes.gif](FluidContainerRes.gif)

You will notice that the container voxel Max Memory Usage numbers have changed wildly from 1.4 GB to 10.4 GB for CPU and from 886.1 MB to 6.8 GB on the GPU. This is also for only with "Cache Temperature" enabled. We need at least Temperature and Density so these may not be settings that work for you on your system. Alternatively, we can reduce the Max Memory Usage, by increasing the Voxel Size to 15 mm. This cuts memory requirements down a lot and because our objects are animated, their chances of "activating" a voxel accurately are pretty good at these settings. The basic requirement is that the smaller the voxel size, the more detailed the simulation but the bigger the memory requirement and the longer it will take to calculate and play back; you just need to find the sweet spot for your project. Next let's set a location for our Cache Directory, and then move to the simulation tab and make sure we have "Active" enabled on the Density tab. Once you have that set, start the caching process again.

![FluidContainerAdjustments.png](FluidContainerAdjustments.png)

Next we need to go to the "Viewport Preview" tab and depending on what channel you wish to have visualized in OpenGL (for now TurbulenceFD can only display on type of Fluid Channel in Layout at a time), you will need to select it and a shader for it. For Temperature, select the Shader "Fire Shader" in the drop-down menu. You should have it set to what is shown in the image below.

## Simulation

Now we get to the fun part - Simulation! We can hit the start button here and watch the simulation calculate over the course of our animation. If you are prompted with a "Overwrite Cache?" warning, you can safely ignore this by hitting "Yes" for the time being, we are only playing.

![ViewPortPreviewChannelFireShaderSelection.png](ViewPortPreviewChannelFireShaderSelection.png)

As you can see in the image above, the simulation is calculating and we can see the Fire Shader, applied to the Temperature Channel, emitting from the Sphere. It should, depending on your animation, also interact with the other two objects as they will collide with any channels of fluid generated by the emitting sphere. It may be hard to see what it's doing "gas" wise, so if you go back into the Viewport Preview Tab, you can change the Channel and Shader type. Don't be alarmed if some of your objects disappear visually when the simulation is running. They will return once the simulation is complete. TurbulenceFD does this to optimize simulation speed while displaying the update to Layout over time.

Now that we have a simulation, we can move on to shading our temperature and density channels with the Fire and Smoke Shaders respectively so that they show up in a render.

## Smoke Shader

For this next step, let's go to the Rendering Tab in the Fluid Container window and jump to the Smoke Shader sub-tab. The default as you will see is set to "none" in the Channel dropdown menu. Let's change this to Density.

Next, let's change the mapping curve for the density so that the F-Curve end point is brought in on the F-Curve Graph to a little past 0.4 on the X axis and peaking at 1.0 on the Y axis.

After we set that, let's jump to the Color & Opacity sub-tab and set our Thickness to 100.0, leave brightness at its default of 100% but set the smoke color to something much darker such as RGB = 0.16, 0.16, 0.16 (in integer RGB 41, 41, 41). We can also remove the Texture (shift-click LMB on the button) to the right of this field as we will not be making use of it.

Turn on VPR and you should see something like this.

![BasicShadedExampleVPR.jpg](BasicShadedExampleVPR.jpg)

We can see that our container isn't quite big enough to not cut off the smoke at the edges and everything is a bit soft. We can fix this later. If we do it now, we'd just get bogged down with long calculation times.

Talking of which, let's look at why cache calculation times are so long. A voxel is a three-dimensional pixel. If you visit the Container Viewport preview tab, you'll the Show Grid button. This gives you an idea of the grid being used for your scene. The smaller the grid square, the longer the calculation will take.

![VoxelGridSize.gif](VoxelGridSize.gif)

We need to set some things in the Sub-Grid Detail sub-panel for our smoke so let's do that now. Increase the Smoke Noise Intensity to 100 mm from its default of 0 m. Next, let's make sure that our Smoke Noise Smallest Size is set to or below our voxel size. This will ensure that during render over time there is no "popping" in the smoke. This will however increase render times. To help compensate for that, let's move over to the Illumination Tab.

The defaults here are "Voxelized Fast" Scattering, Anisotropy 0.0 and Illumination Resolution set to 100%. We can drop the Illumination Resolution to 75% and you will see that render times decrease. If you are not seeing much smoke, the main reason might be you need more in the Density Channel of your Emitter. Set the emitter to push out 3 units of Density and reduce the dissipation percentage. Do that, resimluate and check the results.

![Resim with more Density Emission and Lower Dissipation.jpg](Resim_with_more_Density_Emission_and_Lower_Dissipation.jpg)

We have much more "Smoke" that lives longer as it emits from the Sphere. We can now also start to see the Sub-Grid Detail come out that we set in the Smoke Shader. You will notice however that even with the default Distant and Environment Light in the scene, that the dark areas of the smoke are really dark. To help "illuminate" this problem, we can enable Multiple Scattering and use a few different settings that the defaults. Let's set max depth to 2 and fall off to 50 %. It may be wise to turn VPR off for this until you are done, as enabling Multiple Scattering will cause a refresh and lighting calculation based on the settings found in the Multiple Scattering section. Once you are ready with your new settings, you can re-enable VPR. The end result will show your scene with a much more appealing and realistic scattering of light into and through the smoke shader, refracting as it goes, turning those really dark (i.e. black) areas, more naturally gray. It will take longer to render.

## Fire Shader

Let's move on to the Fire Shader settings. In order to speed things up for interactivity, we can disable the Smoke Shader - go into the Smoke Shader Mapping sub-tab and set the Channel to None - and just work on tweaking our Fire Shader values in the Fire Shader Sub-Grid Detail Sub-tab. 

Let's increase the Fire Noise Intensity to 500 mm from the default of 0m and set the Fire Noise Smallest Size to 10 mm and Largest Scale to 90 mm. We will also make some adjustments to the Fire Shader F-Curve while we are at it.

![FireShaderSubgridSettingsAndF-CurveAdjustmentsNoSmoke.png](FireShaderSubgridSettingsAndF-CurveAdjustmentsNoSmoke.png)

As you can see in the image above with the suggested adjustments to the F-Curve and Sub-grid detail on the Fire Shader, our Fire has more "tooth" and has a better overall color gradient. We can improve the color however by going to the Color & Opacity Sub-Tab and changing "Opacity" from the default of 1.0 to 0.25. This helps a lot.

Now let's see what it all looks like together by re-enabling the Smoke Shader.

Yous should now have, scrubbing through the timeline a little bit, smoke and fire interacting with the Sphere and flattened Cube (as they are set to be collision objects) and its shaded pretty nicely, but we can improve the look and render speed by doing a couple of things. First off, do we really need to have the smoke illuminated by the default Environment Light? Generally, the answer is no as the multi-scattering function provides a form of "radiosity" from other directional lights in the scene. Second, smoke in nature is made up of carbon particles which are effectively "black" (thus the black body fire shading mode) and we need to reduce the smoke color to a very low setting near "super black" (in video and computer graphics terms) and let just the Distant light do the work for us along with the Fire Shader contributing "light" and thus color to the Smoke Shader. In the image below, we have set the Fluid Container to exclude the Environment Light and we have change the smoke color to float RGB = 0.02, 0.02, 0.02 (in integer RGB 05, 05, 05). This improves the look of not only the Smoke but also the Fire.

![Final-test-Render](Final-test-Render.png)

A satisfying final test result. Now time to increase our resolution by decreasing voxel size and resimulating. Turbulence takes some learning. We have some great scenes for you to learn with on the Asset store.