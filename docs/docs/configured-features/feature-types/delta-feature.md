---
layout: page
title: Delta Feature
permalink: /docs/configured-features/feature-types/delta-feature/
parent: Configured Features
grand_parent: Documentation
---

## Delta Feature

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:delta_feature` feature type is used to place a delta. In vanilla, this is used to place Magma Blocks and Lava in the Basalt Deltas biome.

### JSON format

<pre>
{
   "type": "minecraft:delta_feature",
   "config": {
      "contents": {
         "Name": "minecraft:lava",
         "Properties": {
            "level": "0"
         }
      },
      "rim": {
         "Name": "minecraft:magma_block"
      },
      "size": 5,
      "rim_size": 1
   }
}
</pre>

* `contents`: The block provider that will be used for the delta.
* `rim`: The block provider that will be used for the rim around the delta.
* <span int>[I]</span> `size`: The radius of the delta, as an integer provider between 0 and 16 (inclusive).
* <span int>[I]</span> `rim_size`: The size of the delta rim, as an integer provider between 0 and 16 (inclusive).