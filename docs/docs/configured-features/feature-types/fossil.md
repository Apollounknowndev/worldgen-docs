---
layout: page
title: Fossil
permalink: /docs/configured-features/feature-types/fossil/
parent: Configured Features
grand_parent: Documentation
---

## Fossil

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:fossil` feature type is used to place a small structure in the world. In vanilla, it is used to place fossils in the Desert and Swamp biomes.

{: .position }
> If necesarry, the placement position is moved downwards to the lowest position of the `OCEAN_FLOOR_WG` heightmap within the bounding box of the placed structure file.
>
> Afterwards, the position is moved further downwards by 10 to 25 blocks.


{: .condition }
> The `max_empty_corners_allowed` configuration affects whether this feature is be placed (see below). However, it is impossible to configure this feature to always be placed.



### JSON format

<pre>
{
   "type": "minecraft:fossil",
   "config": {
      "max_empty_corners_allowed": 4,
      "fossil_structures": [
         "minecraft:fossil/spine_1",
         "minecraft:fossil/spine_2"
      ],
      "overlay_structures": [
         "minecraft:fossil/spine_1_coal",
         "minecraft:fossil/spine_2_coal"
      ],
      "fossil_processors": "minecraft:fossil_rot",
      "overlay_processors": "minecraft:fossil_diamonds"
   }
}
</pre>

* <span int>[I]</span> `max_empty_corners_allowed`: The maximum corners of the structures that are allowed to not be buried, as an integer between 0 and 7.
* <span list>[L]</span> `fossil_structures`: A list of structure files that this feature uses.
* <span list>[L]</span> `overlay_structures`: A list of structure files that this feature overlays over the `fossil_structure` in the same index.
* `fossil_processors`: The processor list to run on the structure from the `fossil_structures` list.
* `overlay_processors`: The processor list to run on the structure from the `overlay_structures` list.