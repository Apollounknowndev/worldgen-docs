---
layout: page
title: Underwater Magma
permalink: /docs/configured-features/feature-types/underwater-magma/
parent: Configured Features
grand_parent: Documentation
nav_order: 57
---

## Underwater Magma

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:underwater_magma` feature type is used to place a patch of magma underwater. In vanilla, this feature is used in the Overworld to place Magma Blocks in aquifers.

### JSON format

<pre>
{
   "type": "minecraft:underwater_magma",
   "config": {
      "floor_search_range": 5,
      "placement_radius_around_floor": 1,
      "placement_probability_per_valid_position": 0.5
   }
}
</pre>

* <span int>[I]</span> `floor_search_range`: The amount of blocks the game will search for a cave floor, as an integer between 0 and 512.
* <span int>[I]</span> `placement_radius_around_floor`: The radius around the cave floor that magma can be placed, as an integer between 0 and 64.
* <span float>[F]</span> `placement_probability_per_valid_position`: The probability for each valid position that magma blocks will actually be placed. Float between 0.0 and 1.0.