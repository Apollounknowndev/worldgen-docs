---
layout: page
title: Twisting Vines
permalink: /docs/configured-features/feature-types/twisting-vines/
parent: Configured Features
grand_parent: Documentation
---

## Twisting Vines

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:twisting_vines` feature type is used to place a patch of Twisting Vines. In vanilla, it is used in the Warped Forest biome.

### JSON format

<pre>
{
   "type": "minecraft:twisting_vines",
   "config": {
      "spread_width": 1,
      "spread_height": 1,
      "max_height": 1
   }
}
</pre>

* <span int>[I]</span> `spread_width`: The x and z-coordinate spread that the feature can generate in, as a radius. 
* <span int>[I]</span> `spread_height`: The y-coordinate spread that the feature can generate in, as a radius.
* <span int>[I]</span> `max_height`: The max height that a column of Twisting Vines can grow to. There is a small chance that the column of Twisting Vines will actually be taller than this value, however.