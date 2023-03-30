---
layout: page
title: Large Dripstone
permalink: /docs/configured-features/feature-types/large-dripstone/
parent: Configured Features
grand_parent: Documentation
nav_order: 34
---

## Large Dripstone

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:large_dripstone` feature type is used to place a large stalagnate of dripstone. In vanilla, this is used in the Dripstone Caves biome.

{: .condition }
> This feature is only placed if the block at the placement position is Air or Water.

### Json format

<pre>
{
  "type": "minecraft:large_dripstone",
  "config": {
    "floor_to_ceiling_search_range": 30,
    "column_radius": {
      "type": "minecraft:uniform",
      "value": {
        "min_inclusive": 9,
        "max_inclusive": 13
      }
    },
    "height_scale": 1.2,
    "max_column_radius_to_cave_height_ratio": 0.33,
    "stalactite_bluntness": 0.6,
    "stalagmite_bluntness": 0.7,
    "wind_speed": 0.15,
    "min_radius_for_wind": 4,
    "min_bluntness_for_wind": 0.6
  }
}
</pre>

* ‌<bl>[I]</bl> `floor_to_ceiling_search_range`: (optional) The range that a cave floor or ceiling is searched for from the starting position, as an integer between 1 and 512. Defaults to 30.
* ‌<bl>[I]</bl> `column_radius`: An integer provider for the minimum and maximum radius of the column. Instead of one random value being chosen from the provider, the minimum and maximum values from the provider are used.
* ‌<ye>[F]</ye> `height_scale`: The height scale of the stalagnate, as a float provider between 0.0 and 20.0. 
* ‌<ye>[F]</ye> `max_column_radius_to_cave_height_ratio`: The ratio of the maximum column radius to the cave height, as a float between 0.0 and 1.0.
* ‌<ye>[F]</ye> `stalactite_bluntness`: How much height gets truncated from the stalactite, as a float provider between 0.1 and 10.0.
* ‌<ye>[F]</ye> `stalagmite_bluntness`: How much height gets truncated from the stalagmite, as a float provider between 0.1 and 10.0.
* ‌<ye>[F]</ye> `wind_speed` The slant of the stalagnate, as a float provider between 0.1 and 2.0.
* ‌<bl>[I]</bl> `min_radius_for_wind`: The minimum radius of the column for wind to take effect, as an integer between 0 and 100.
* ‌<ye>[F]</ye> `min_bluntness_for_wind`: The minimum bluntness value for wind to take effect, as a float between 0.0 and 5.0.