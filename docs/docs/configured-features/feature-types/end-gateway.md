---
layout: page
title: End Gateway
permalink: /docs/configured-features/feature-types/end-gateway/
parent: Configured Features
grand_parent: Documentation
---

## End Gateway

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:end_gateway` feature type is used to place an end gateway that warps entities into and out of the Outer End. In vanilla, they are placed in the End Highlands biome.

### JSON format

<pre>
{
   "type": "minecraft:end_gateway",
   "config": {
      "exact": true,
      "exit": [
         100,
         50,
         0
      ]
   }
}
</pre>

* <span bool>[B]</span> `exact`: Determines whether or not the end gatewy will teleport entities to the exact exit location.
* `exit`: (optional) The coordinates that the end gateway will teleport entities to. An `exit` of [100,50,0] will teleport the player to the obsidian platform that you enter the End on.