# Procedural Geometry

## Editor

This Mesh Modifier handler allows for creating geometry per frame using nodes. Many operations include names to separate or combine the geometry into named bins of geometry.
Each named bin is a vector containing one or more geometry objects. Each geometry object contains the vertex and polygon data as well as object info such as a transform matrix.

Procedural Geometry is available in the Object Properties window > Primitive tab > Add Modifier menu. When added, three nodes are present by default and a cube will appear in Layout's viewport. On the left - in the Node Editor that appears when you double-click the Procedural Geometry modifier - Primitive Geometry is fed into an Add Geometry node and then the right-most root node: a single input of Procedural Geometry.

### Node operations nodal flow

This represents the results of the node operations nodal flow as it is evaluated from right to left.

### Nodal flow bin

Double-clicking the root node will open a Panel showing the objects in each named bin. Clicking the left check box will enable/disable the polygon creation for that bin. The objects can be cached in memory using the cache checkbox. LWObjects can be saved to disk at each from using the Save LWO Sequence, playing through the frames, and turning it off when finished.
LWO objects can also be saved using the save current object in the save menu.

### LWO Objects

Surface names are created for each named object in the bin.


