---
layout: page
title: Simple Block
permalink: /docs/configured-features/feature-types/simple-block/
parent: Configured Features
grand_parent: Documentation
nav_order: 52
---

## Simple Block

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:simple_block` feature type is used to place a single block. In vanilla, this is used to place Spore Blossoms in Lush Caves.

### Json format

<pre>
{
   "type": "minecraft:simple_block",
   "config": {
      "to_place": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:stone"
         }
      }
   }
}
</pre>

* `to_place`: The block state provider to use.