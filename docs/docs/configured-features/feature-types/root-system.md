---
layout: page
title: Root System
permalink: /docs/configured-features/feature-types/root-system/
parent: Configured Features
grand_parent: Documentation
nav_order: 47
---

## Root System

<head>
    {% include field-type-colors.html %}
</head>

{: .note }
The game's code needs to be checked to get the complete information to finish this page.

The `minecraft:root_system` feature type is used to place a system of roots from a cave up to the surface, and place a feature on top of it. In vanilla, this is used to place Rooted Dirt under Azalea trees.

### Json format

<pre>
{
   "type": "minecraft:root_system",
   "config": {
      "required_vertical_space_for_tree": 3,
      "root_radius": 3,
      "root_placement_attempts": 20,
      "root_column_max_height": 100,
      "hanging_root_radius": 3,
      "hanging_roots_vertical_span": 2,
      "hanging_root_placement_attempts": 20,
      "allowed_vertical_water_for_tree": 2,
      "root_replaceable": "#minecraft:azalea_root_replaceable",
      "root_state_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:rooted_dirt"
         }
      },
      "hanging_root_state_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:hanging_roots",
            "Properties": {
               "waterlogged": "false"
            }
         }
      },
      "allowed_tree_position": {
         "type": "minecraft:matching_blocks",
         "blocks": "minecraft:air"
      },
      "feature": {
         "feature": "minecraft:azalea_tree",
         "placement": []
      }
   }
}
</pre>

* ‌<bl>[I]</bl> `required_vertical_space_for_tree`: An integer between 1 and 64.
* ‌<bl>[I]</bl> `root_radius`: An integer between 1 and 64.
* ‌<bl>[I]</bl> `root_placement_attempts`: An integer between 1 and 256.
* ‌<bl>[I]</bl> `root_column_max_height`: An integer between 1 and 4096.
* ‌<bl>[I]</bl> `hanging_root_radius`: An integer between 1 and 64.
* ‌<bl>[I]</bl> `hanging_roots_vertical_span`: An integer between 0 and 16.
* ‌<bl>[I]</bl> `hanging_root_placement_attempts`: An integer between 1 and 256.
* ‌<bl>[I]</bl> `allowed_vertical_water_for_tree`: The maximum amount of water the top feature can generate in, as an integer between 1 and 64.
* `root_replaceable`: A block tag that roots can replace.
* `root_state_provider`: The block state provider for the roots to use.
* `hanging_root_state_provider`: The block state provider for the hanging roots to use.
* `allowed_tree_position`: The block predicate that must pass at the surface for the root system and feature on top to be placed.
* `feature`: The placed feature to place on top of the root system.