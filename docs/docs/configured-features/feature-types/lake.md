---
layout: page
title: Lake
permalink: /docs/configured-features/feature-types/lake/
parent: Configured Features
grand_parent: Documentation
nav_order: 33
---

## Lake

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:lake` feature type is used to place a small pool of a fluid. In vanilla, this is used for lava lakes in the Overworld.

### Jsom format

<pre>
{
   "type": "minecraft:lake",
   "config": {
      "fluid": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:lava",
            "Properties": {
               "level": "0"
            }
         }
      },
      "barrier": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:stone"
         }
      }
   }
}
</pre>

* `fluid`: The block state provider that will be used for the fluid of the lake.
* `barrier`: The block state provider that will be used for the barrier of the lake.

### Additional Info

* The feature is marked as Deprecated in the game's code. This doesn't mean necesarily that it's getting removed, but that it should be avoided.