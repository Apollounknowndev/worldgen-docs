---
layout: page
title: Ore
permalink: /docs/configured-features/feature-types/ore/
parent: Configured Features
grand_parent: Documentation
nav_order: 41
---

## Ore

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:ore` feature type is used to replace a blob of blocks with another blob of blocks. In vanilla, this is used to generate all ores (excluding ores in the massive copper/iron ore veins and ancient debris).

### JSON format

<pre>
{
   "type": "minecraft:ore",
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