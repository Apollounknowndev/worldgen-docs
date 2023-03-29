---
layout: page
title: Multiface Growth
permalink: /docs/configured-features/feature-types/multiface-growth/
parent: Configured Features
grand_parent: Documentation
nav_order: 36
---

## Multiface Growth

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:multiface_growth` feature type is used to place a small patch of either glow lichen or sculk. In vanilla, this is used in all Overworld biomes for Glow Lichen and the Deep Dark for Sculk.

### Json format

<pre>
{
   "type": "minecraft:multiface_growth",
   "config": {
      "block": "minecraft:glow_lichen",
      "search_range": 20,
      "chance_of_spreading": 0.5,
      "can_place_on_floor": false,
      "can_place_on_ceiling": true,
      "can_place_on_wall": true,
      "can_be_placed_on": "#minecraft:base_stone_overworld"
   }
}
</pre>

* `block`: (optional) The block that gets placed. This must be either `minecraft:glow_lichen` or `minecraft:sculk_vein`. Defaults to `minecraft:glow_lichen`.
* ‌<bl>[I]</bl> `search_range`: (optional) The range that will be searched for a valid placement, as a value between 1 and 64. Defaults to 10.
* ‌<ye>[F]</ye> `chance_of_spreading`: (optional) The change that the block will grow onto other faces of the block, as a float between 0.0 and 1.0. Defaults to 0.5.
* ‌<or>[B]</or> `can_place_on_floor`: (optional) Determines whether or not the block can be placed on the floor. Defaults to false.
* ‌<or>[B]</or> `can_place_on_ceiling`: (optional) Determines whether or not the block can be placed on the ceiling. Defaults to false.
* ‌<or>[B]</or> `can_place_on_wall`: (optional) Determines whether or not the block can be placed on the walls. Defaults to false.
* `can_be_placed_on`: A block tag (or list of blocks) that the block can be placed on in world generation.