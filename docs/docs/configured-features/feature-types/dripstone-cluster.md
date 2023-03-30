---
layout: page
title: Dripstone Cluster
permalink: /docs/configured-features/feature-types/dripstone-cluster/
parent: Configured Features
grand_parent: Documentation
nav_order: 16
---

## Dripstone Cluster

<head>
    {% include field-type-colors.html %}
</head>

{: .note }
The game's code needs to be checked to get the complete information to finish this page.

The `minecraft:dripstone_cluster` feature type is used to place clusters of dripstone on the floor or a ceiling of a surface. In vanilla, this is used in the Dripstone Caves biome.

{: .condition }
> This feature is only placed if the block at the placement position is Air or Water.

### JSON format

<pre>
{
   "type": "minecraft:dripstone_cluster",
   "config": {
      "floor_to_ceiling_search_range": 12,
      "height": 4,
      "radius": 5,
      "max_stalagmite_stalactite_height_diff": 1,
      "height_deviation": 3,
      "dripstone_block_layer_thickness": 3,
      "density": 0.5,
      "wetness": 0.4,
      "chance_of_dripstone_column_at_max_distance_from_center": 0.1,
      "max_distance_from_edge_affecting_chance_of_dripstone_column": 3,
      "max_distance_from_center_affecting_height_bias": 8
   }
}
</pre>

* ‌<bl>[I]</bl> `floor_to_ceiling_search_range`: The distance that will be searched for a floor or ceiling, as an integer between 1 and 512 (inclusive).
* ‌<bl>[I]</bl> `height`: The height of the dripstone cluster, as an integer provider between 1 and 128 (inclusive).
* ‌<bl>[I]</bl> `radius`: The radius of the dripstone cluster, as an integer provider between 1 and 128 (inclusive).
* ‌<bl>[I]</bl> `max_stalagmite_stalactite_height_diff`: An integer between 0 and 64 (inclusive).
* ‌<bl>[I]</bl> `height_deviation`: An integer between 1 and 64 (inclusive).
* ‌<bl>[I]</bl> `dripstone_block_layer_thickness`: An integer provider between 0 and 128 (inclusive).
* ‌<ye>[F]</ye> `density`: A float provider between 0.0 and 2.0 (inclusive).
* ‌<ye>[F]</ye> `wetness`: A float provider between 0.0 and 2.0 (inclusive).
* ‌<ye>[F]</ye> `chance_of_dripstone_column_at_max_distance_from_center`: A float between 0.0 and 1.0 (inclusive).
* ‌<bl>[I]</bl> `max_distance_from_edge_affecting_chance_of_dripstone_column`: An integer between 1 and 64 (inclusive).
* ‌<bl>[I]</bl> `max_distance_from_center_affecting_height_bias`: An integer between 1 and 64 (inclusive).