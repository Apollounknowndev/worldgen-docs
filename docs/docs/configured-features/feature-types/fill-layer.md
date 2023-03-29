---
layout: page
title: Fill Layer
permalink: /docs/configured-features/feature-types/fill-layer/
parent: Configured Features
grand_parent: Documentation
nav_order: 20
---

## Fill Layer

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:fill_layer` feature type is used to place a layer of blocks. In vanilla, this feature type is used to place layers of blocks in the Superflat world type.

### JSON format

<pre>
{
   "type": "minecraft:fill_layer",
   "config": {
      "state": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:stone"
         }
      },
      "height": 64
   }
}
</pre>

* `state`: The block provider that will be used for the layer.
* ‌<bl>[I]</bl> `height`: The height that the layer of blocks will be placed at, as an offset from the bottom y-coordinate of the world.