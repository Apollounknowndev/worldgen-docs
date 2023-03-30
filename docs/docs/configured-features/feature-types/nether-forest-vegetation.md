---
layout: page
title: Nether Forest Vegetation
permalink: /docs/configured-features/feature-types/nether-forest-vegetation/
parent: Configured Features
grand_parent: Documentation
nav_order: 37
---

## Nether Forest Vegetation

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:nether_forest_vegetation` feature type is used to place a patch of plants in the Nether. In vanilla, it's used in the Nether. Shocking, right?

{: .condition }
> This feature is only placed if the block below the placement position is in the `minecraft:nylium` block tag.

### Json format

<pre>
{
   "type": "minecraft:nether_forest_vegetation",
   "config": {
      "state_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:crimson_roots"
         }
      },
      "spread_width": 8,
      "spread_height": 4
   }
}
</pre>

* `state_provider`: The block state provider that the feature places.
* ‌<bl>[I]</bl> `spread_width`: The horizontal radius that the feature places the plants in, as a positive integer.
* ‌<bl>[I]</bl> `spread_height`: The vertical radius that the feature places the plants in, as a positive integer.