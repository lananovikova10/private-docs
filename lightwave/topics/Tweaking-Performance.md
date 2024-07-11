# Tweaking Performance

### General tips:

* Store/Load the sim caches to/from the fastest drive you have (e.g. an SSD, M.2). Avoid network drives unless you're on a high-end network and file server (10GbE, etc.).
* Make sure your virus scanner does not scan .bcf files on read/write.
* Close all other applications during sim/render.

### Simulation Performance:

* Don't run simulations that exceed your available memory.
* Make sure you don't sim and/or cache channels you don't need for rendering.
* Use only low values like 1 or 2 for sub-frame or pressure iteration steps unless you see artifacts.
* Don't use collision objects unless they're essential to your effect.
* Don't use very high-poly objects as emitters. Use low-poly proxies instead.
* Don't use large numbers of octaves for noise on emitters, turbulence, etc. unless you're sure you need them.
* Disable the preview(s) and/or timeline update during simulation.
* When using several emitter objects, parenting them under a null with one emitter tag is faster than adding a separate tag to each object.

### To optimize render times, consider this:

* Use Sub-Grid Detail only if absolutely necessary. Use a low or no distance between the Largest and Smallest Scale.
* Avoid sections of mapping curves that have values close to zero. This often happens when strongly bending a curve segment, such that one part of it seems to touch zero, but it actually doesn't.
* Use Voxelized Fast Illumination.
* Lower the Illumination Resolution until you see artifacts.
* For multiple scattering illumination, lower the Depth and Directional Resolution until you see artifacts.
* Make sure Adaptive Step Size is enabled.
![AdaptiveStepSize.width-800.png](AdaptiveStepSize.png)
* Increase the Step Size and Shadow Step Size until you see artifacts.
* For Motion Blur use a low number of Sub-Steps.
