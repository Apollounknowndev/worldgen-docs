---
layout: page
title: Vegetation Patch
permalink: /docs/configured-features/feature-types/vegetation-patch/
parent: Configured Features
grand_parent: Documentation
nav_order: 58
---

## Vegetation Patch

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:vegetation_patch` feature type is used to place a patch of a block on a surface, and generate vegetation features on top of it. In vanilla, it is used in the generate of some vegetation in the Lush Caves biome.

### JSON format

<pre>
{
   "type": "minecraft:vegetation_patch",
   "config": {
      "surface": "floor",
      "depth": 3,
      "vertical_range": 2,
      "extra_bottom_block_chance": 0.8,
      "extra_edge_column_chance": 0.7,
      "vegetation_chance": 0.05,
      "xz_radius": 3,
      "replaceable": "#minecraft:lush_ground_replaceable",
      "ground_state": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:clay"
         }
      },
      "vegetation_feature": "minecraft:dripleaf"
   }
}
</pre>

* <span str>[S]</span> `surface`: The surface this vegetation patch is placed on. Can be either `floor` or `ceiling`.
* <span int>[I]</span> `depth`: An integer provider between 1 and 128.
* <span int>[I]</span> `vertical_range`: An integer between 1 and 256.
* <span float>[F]</span> `extra_bottom_block_chance`: The chance that an extra block from the `ground_state` will be added into the surface, as a value between 0.0 and 1.0.
* <span float>[F]</span> `extra_edge_column_chance`: The chance that an extra block on the edge of the vegetation patch will generate, as a value between 0.0 and 1.0.
* <span float>[F]</span> `vegetation_chance`: The chance for each block that the feature in `vegetation_feature` will be placed on the block, as a value between 0.0 and 1.0.
* <span int>[I]</span> `xz_radius`: The radius of the vegetation patch, as an integer provider.
* `replaceable`: A block tag for the blocks that the `ground_state` can replace.
* `ground_state`: The block state provider for the vegetation patch to place.
* `vegetation_feature`: The placed feature for the vegetation patch to place.

### Additional Info

This feature is identical to the `minecraft:waterlogged_vegetation_patch` feature in configuration. The different is that the `minecraft:vegetation_patch` feature does not waterlog all non-surface edge blocks, while the `minecraft:waterlogged_vegetation_patch` feature does. 