---
layout: page
title: Disk
permalink: /docs/configured-features/feature-types/disk/
parent: Configured Features
grand_parent: Documentation
nav_order: 15
---

## Disk

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:disk` feature type is used to place disks of blocks. They're used in several places in vanilla; they're used for ice patches in Ice Spikes biomes, gravel/sand/clay patches in most biomes underwater, and grass block patches in Mangrove Swamp biomes.

### JSON format

<pre>
{
   "type": "minecraft:disk",
   "config": {
      "state_provider": {
         "fallback": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:clay"
            }
         },
         "rules": []
      },
      "target": {
         "type": "minecraft:true"
      },
      "radius": 3,
      "half_height": 1
   }
}
</pre>

* `state_provider`: The block the disk will place.
   * `fallback`: The block provider that will be used if none of the rules pass.
   * <span list>[L]</span> `rules`: (can be empty) The list of rules to check before using the state provided in `fallback`.
      * `if_true`: The [block predicate](/docs/misc/block-predicates/) that must be passed for the `then` block state to be used.
      * `then`: The block state that should be used if the block predicate from `if_true` passes.
* `target`: The [block predicate](/docs/misc/block-predicates/) that must be passed at the starting block position for the disk to be placed at all.
* <span int>[I]</span> `radius`: The radius of disk, as an integer provider between 0 and 8 (inclusive).
* <span int>[I]</span> `half_height`: Half of the disk's height, as an integer between 0 and 4 (inclusive).