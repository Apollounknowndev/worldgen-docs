---
layout: page
title: Bamboo
permalink: /docs/configured-features/feature-types/bamboo/
parent: Configured Features
grand_parent: Documentation
---

## Bamboo

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:bamboo` feature type is used to place a pillar of bamboo that is 5-16 blocks tall, and occasionally a disk of podzol. In vanilla, this feature type is used to generate bamboo in the Jungle biomes.

{: .condition }
> This feature is only placed if the placement position is air and a bamboo block can survive at this location.

{: .position }
> The disk of podzol is always placed at the height of the `WORLD_SURFACE` heightmap.

### JSON format

<pre>
{
   "type": "minecraft:bamboo",
   "config": {
      "probability": 0.5
   }
}
</pre>

* <span float>[F]</span> `probability`: The chance that a podzol disk will generate under the bamboo, as a value between 0.0 and 1.0 (inclusive).