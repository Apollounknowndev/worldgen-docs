---
layout: page
title: Sea Pickle
permalink: /docs/configured-features/feature-types/sea-pickle/
parent: Configured Features
grand_parent: Documentation
nav_order: 50
---

## Sea Pickle

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:sea_pickle` feature type is used to place a patch of sea pickles. In vanilla, this is used in the Warm Ocean biome.

{: .position }
> The placement position of this feature is moved to the height of the `OCEAN_FLOOR` heightmap.
>
> The change in position of where the sea pickles is placed on the x and z coordinates relative to the starting point functions identically to an `xz_spread` of 7 with the `minecraft:random_patch` feature type.

### JSON format

<pre>
{
   "type": "minecraft:sea_pickle",
   "config": {
      "count": 20
   }
}
</pre>

* <span int>[I]</span> `count`: The number of sea pickes to be generated, as an integer provider between 0 and 256.