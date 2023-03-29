---
layout: page
title: Fossil
permalink: /docs/configured-features/feature-types/fossil/
parent: Configured Features
grand_parent: Documentation
nav_order: 23
---

## Fossil

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:fossil` feature type is used to place a small structure in the world. In vanilla, it is used to place fossils in the Desert and Swamp biomes.

### Json format

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

* ‌<bl>[I]</bl> `max_empty_corners_allowed`: The maximum corners of the structures that are allowed to not be buried, as an integer between 0 and 7.
* ‌<re>[L]</re> `fossil_structures`: A list of structure files that this feature uses.
* ‌<re>[L]</re> `overlay_structures`: A list of structure files that this feature overlays over the `fossil_structure` in the same index.
* `fossil_processors`: The processor list to run on the structure from the `fossil_structures` list.
* `overlay_processors`: The processor list to run on the structure from the `overlay_structures` list.