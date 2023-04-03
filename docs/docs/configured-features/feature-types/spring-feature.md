---
layout: page
title: Spring Feature
permalink: /docs/configured-features/feature-types/spring-feature/
parent: Configured Features
grand_parent: Documentation
nav_order: 54
---

## Spring Feature

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:spring_feature` feature type is used to place a spring of a certain fluid that immediately begins to flow once the chunk the spring is in is within simulation distance. This is used in vanilla to place springs of water in the Overworld, and springs of lava in the Overworld and Nether.

### JSON format

<pre>
{
  "type": "minecraft:spring_feature",
  "config": {
    "state": {
      "Name": "minecraft:water",
      "Properties": {
        "falling": "true"
      }
    },
    "rock_count": 4,
    "hole_count": 1,
    "requires_block_below": true,
    "valid_blocks": "#minecraft:base_stone_overworld"
  }
}
</pre>

* `state`: The fluid state that this spring places.
* ‌<bl>[I]</bl> `rock_count`: The number of blocks in all directions to the starting position (excluding above the starting position) that must be from the `valid_blocks` block tag. This is an exact number and not a threshold; if `rock_count` is 3 and 4 blocks adjacent to the starting position are in the `valid_blocks` block tag, the spring will fail to place.
* ‌<bl>[I]</bl> `hole_count`: The number of blocks in all directions to the starting position (excluding above the starting position) that must be air. This is an exact number and not a threshold; if `hole_count` is 1 and 2 blocks adjacent to the starting position are air, the spring will fail to place.
* ‌<or>[B]</or> `requires_block_below`: Whether or not the block below where the spring attempts to generate needs to not be air. Defaults to true.
* `valid_blocks`: A block tag with the blocks that the spring will check for in the `rock_count` check.