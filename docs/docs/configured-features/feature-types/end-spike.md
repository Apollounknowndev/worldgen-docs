---
layout: page
title: End Spike
permalink: /docs/configured-features/feature-types/end-spike/
parent: Configured Features
grand_parent: Documentation
---

## End Spike

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:end_spike` feature type is used to place end pillars in the center end island. Yes, they're called spikes and not pillars. In vanilla, this feature is used in The End biome. Not the dimension, just the biome named The End. Makes sense, right?

### JSON format

<pre>
{
   "type": "minecraft:end_spike",
   "config": {
      "crystal_invulnerable": false,
      "crystal_beam_target": [
         0,
         127,
         0
      ],
      "spikes": [
         {
            "centerX": 0,
            "centerZ": 0,
            "radius": 3,
            "height": 95,
            "guarded": true
         }
      ]
   }
}
</pre>

* <span bool>[B]</span> `crystal_invulnerable`: Determines whether or not the end crystal on top of the spike(s) are invulerable.
* `crystal_beam_target`: (optional) The coordinates that the end crystal will generate a beam towards. If this field is empty, no beam comes out of the end crystal.
* <span list>[L]</span> `spikes`: (optional) A list of spikes that this feature places.
    * <span int>[I]</span> `centerX`: The x-coordinate that the end spike is centered on.
    * <span int>[I]</span> `centerZ`: The z-coordinate that the end spike is centered on.
    * <span int>[I]</span> `radius`: The radius of the end spike.
    * <span int>[I]</span> `height`: The y-coordinate that the end spike generates up to. This starts from the bottom y-coordinate of the world.
    * <span bool>[B]</span> `guarded`: Determines whether or not the end crystal on top of the spike is guarded by iron bars.