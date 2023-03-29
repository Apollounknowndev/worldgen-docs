---
layout: page
title: Netherrack Replace Blobs
permalink: /docs/configured-features/feature-types/netherrack-replace-blobs/
parent: Configured Features
grand_parent: Documentation
nav_order: 38
---

## Netherrack Replace Blobs

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:netherrack_replace_blobs` feature type is used to replace all blocks within a certain radius with another block. The feature will move the starting position down until a valid position can be found.

### Json format

<pre>
{
   "type": "minecraft:netherrack_replace_blobs",
   "config": {
      "state": {
         "Name": "minecraft:diorite"
      },
      "target": {
         "Name": "minecraft:stone"
      },
      "radius": 12
   }
}
</pre>

* `state`: The block state that the feature places.
* `target`: The target block state to be replaced by the feature.
* ‌<bl>[I]</bl> `radius`: The radius of the block replacement, as an integer provider between 0 and 12.