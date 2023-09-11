---
layout: page
title: Forest Rock
permalink: /docs/configured-features/feature-types/forest-rock/
parent: Configured Features
grand_parent: Documentation
---

## Forest Rock

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:forest_rock` feature type is used to place a rock of a certain block. In vanilla, this is used to place mossy cobblestone rocks in the Old Growth Taiga biomes.

{: .position }
> The placment position is moved downwards until it is directly above a block that is in the `minecraft:dirt` or `minecraft:base_stone_overworld` block tags. If it reaches the lower build limit, the placement fails.

### JSON format

<pre>
{
   "type": "minecraft:forest_rock",
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

* `state`: The block provider that will be used for the rock.