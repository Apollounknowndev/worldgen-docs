---
layout: page
title: Scattered Ore
permalink: /docs/configured-features/feature-types/scattered-ore/
parent: Configured Features
grand_parent: Documentation
nav_order: 48
---

## Scattered Ore

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:scattered_ore` feature type is used to replace some blocks in an area with another blob of blocks. In vanilla, this is used to generate Ancient Debris.

### JSON format

<pre>
{
   "type": "minecraft:scattered_ore",
   "config": {
      "size": 10,
      "discard_chance_on_air_exposure": 0,
      "targets": [
         {
            "target": {
               "predicate_type": "minecraft:block_match",
               "block": "minecraft:netherrack"
            },
            "state": {
               "Name": "minecraft:nether_gold_ore"
            }
         }
      ]
   }
}
</pre>

* ‌<bl>[I]</bl> `size`: The size of the ore, as a value between 0 and 64. Higher size = large average ore size. The `size` value doesn't necesarily correlate to the number of blocks modified in the ore placement.
* ‌<ye>[F]</ye> `discard_chance_on_air_exposure`: The chance that an ore block will be discarded upon exposure to air, as a float between 0.0 and 1.0.
* ‌<re>[L]</re> `targets`: A list of targets for the ore feature.
    * `target`: The target predicate.
        * `predicate_type`: The rule test that needs to pass for the block in `state` to be placed.
        * `state`: The block state that gets placed if the aforementioned predicate passes.

### Additional info
While this feature is identical in configuration to the `minecraft:ore` feature, `minecraft:scattered_ore` scatters the blocks replaces over a area and doesn't replace every single block in an area.