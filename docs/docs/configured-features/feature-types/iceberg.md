---
layout: page
title: Iceberg
permalink: /docs/configured-features/feature-types/iceberg/
parent: Configured Features
grand_parent: Documentation
nav_order: 31
---

## Iceberg

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:iceberg` feature type is used to place an iceberg of a certain block. In vanilla, this is used in the Frozen Ocean and Deep Frozen Ocean biomes.

{: .position }
The feature will always place at the dimension's sea level.


### JSON format

<pre>
{
   "type": "minecraft:iceberg",
   "config": {
      "state": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:stone"
         }
      }
   }
}
</pre>

* `state`: The block state that will be used for the iceberg.