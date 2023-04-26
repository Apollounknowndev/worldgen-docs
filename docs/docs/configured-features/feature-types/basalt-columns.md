---
layout: page
title: Basalt Columns
permalink: /docs/configured-features/feature-types/basalt-columns/
parent: Configured Features
grand_parent: Documentation
nav_order: 3
---

## Basalt Columns

<head>
    {% include field-type-colors.html %}
</head>
The `minecraft:basalt_columns` feature type is used to place clusters of basalt columns. In vanilla, this feature type is used to generate a lot of the basalt in the Basalt Delta biome.

{: .condition }
> This feature is only placed if its placement position is in air or in the lava ocean (block is lava and y-position is less or equal the sea level).
>
> Additionally, the feature is not placed if the block below the placement position is Air, Lava, Bedrock, Magma Block, Soul Sand, Nether Bricks, Nether Brick Fence, Nether Brick Stairs, Nether Wart, Chest, or Spawner.


### JSON format

<pre>
{
   "type": "minecraft:basalt_columns",
   "config": {
      "reach": 1,
      "height": 2
   }
}
</pre>

* <span int>[I]</span> `reach`: The radius of a cluster of basalt, as an integer provider between 0 and 3 (inclusive).
* <span int>[I]</span> `height`: The maximum height of a cluster of basalt, as an integer provider between 1 and 10 (inclusive).

Please note that multiple clusters of basalt can generate as one feature, so just because the `reach` value is 3 or below, it doesn't mean that the maximum radius for a basalt columns feature is 3.