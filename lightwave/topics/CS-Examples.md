# Examples

## I love the sound of Breaking Glass {collapsible="true"}

### The scene as it initially loads in ChronoSculpt: {collapsible="true"}

![BreakingGlass-01.png](BreakingGlass-01.png){style=block}

### Those bits of glass in the centre of the pane seem to be stuck {collapsible="true"}

![BreakingGlass-02.png](BreakingGlass-02.png){style=block}

### Yes, they are indeed. Do we need to go back and resimulate? {collapsible="true"}

![BreakingGlass-03.png](BreakingGlass-03.png){style=block}

### Not with ChronoSculpt to hand! Use the Transform tool and grab the offending shards of glass, there should be four in total. {collapsible="true"}

![BreakingGlass-04.png](BreakingGlass-04.png){style=block}

### Move each piece down in the Y ao it's under the frame and then stretch the end out to reach the end of the scene {collapsible="true"}

![BreakingGlass-05.png](BreakingGlass-05.png){style=block}

Now, click on the Ease Out button and move the yellow dot all the way to the right. You should see that the initial pyramid shape has changed to give an incoming slope, but the pose is held until the end of the scene.

![BreakingGlass-06.png](BreakingGlass-06.png){style=block}

Now that you have moved one piece, do the other three. You morphed the object’s vertices and can move the morphs nearer the start of the scene by dragging on each of the four yellow circles in the timeline. By changing the Ease In curve you can dictate how the shards all fall.

![BreakingGlass-07.png](BreakingGlass-07.png){style=block}

## Controlled Explosion {collapsible="true"}

In a similar vein to the previous example, your director suddenly decides that the bridge you’ve slaved over getting the dynamics just right needed to be arched. There isn’t the time to rebuild the bridge, it’s going to be in the distance, so you can get away with stuff. Here’s how ChronoSculpt can help save the day. Here’s the bridge. It has an MDD file of the explosion already loaded, but we’re going to go into Setup mode to alter the base geometry before it gets destroyed.

![Bridge_demolish-01.png](Bridge_demolish-01.png){style=block}

In Setup Mode we have used the Drag tool to change the shape of the bridge, to give the hump the director wants.

![Bridge_demolish-02.png](Bridge_demolish-02.png){style=block}

The bridge’s center legs have been stretched down a little to keep them on the ground.

![Bridge_demolish-03.png](Bridge_demolish-03.png){style=block}

The deformed bridge is destroyed for the 3-second shot at no additional cost for remodeling or redoing the dynamics. Job done.

![Bridge_demolish-04.png](Bridge_demolish-04.png){style=block}

## Cloth Penetration {collapsible="true"}

The Sculpt tool can be used to solve those tricky cloth penetration issues swiftly, even if the car geometry is changed.

![clothpenetration.gif](clothpenetration.gif){style=block}

## Ill-equipped soldier {collapsible="true"}

Go into Setup mode (01), select the gear you want to remove

![ill-equipped-01.png](ill-equipped-01.png){width=400 style=block}

...and move it offscreen one-by-one

![ill-equipped-02.png](ill-equipped-02.png){width=400 style=block}

Exit setup mode

![ill-equipped-03.png](ill-equipped-03.png){width=400 style=block}

### Ill-Proportioned Soldier {collapsible="true"}

You can, of course, create some variation if you need several soldier objects, to keep them looking different. This is all the same object and the MDD cache plays back no matter how the soldier looks.

![Variations.gif](Variations.gif){style=block}