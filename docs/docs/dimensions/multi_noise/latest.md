---
layout: default
title: Multi-Noise Biome Source
permalink: /docs/dimensions/multi-noise/latest/
parent: Dimensions
grand_parent: Documentation
nav_order: 2
---

# Multi-Noise Biome Source

The multi-noise system is used to place biomes at certain places of the world. The biome being placed is based on six inputs:

* `continentalness`
* `erosion`
* `temperature`
* `humidity`
* `weirdness`
* `depth`

The first five inputs are based on perlin noise, and the sixth one is based on the depth below the surface.

A dimension file has a list of biomes and their ideal inputs (known in the files as their "parameters"), which are a list of parameters and min/max values which are preferred. This is rather complex to explain, so here's an example with just two biomes, the Plains and the Forest:

```json
[
   {
      "biome": "minecraft:plains",
      "parameters": {
         "temperature": 0,
         "humidity": [
            -1,
            0
         ],
         "continentalness": 0,
         "erosion": 0,
         "weirdness": 0,
         "depth": 0,
         "offset": 0
      }
   },
   {
      "biome": "minecraft:forest",
      "parameters": {
         "temperature": 0,
         "humidity": [
            0,
            1
         ],
         "continentalness": 0,
         "erosion": 0,
         "weirdness": 0,
         "depth": 0,
         "offset": 0
      }
   }
]
```
Here, the Plains biome will generate if `humidity` is between -1 and 0 and the Forst biome will generate if `humidity` is between 0 and 1.

The `humidity` value normally fluctuates between -1 and 1, but what if it goes outside the range? If no biomes in the biome source match the parameters, the game will choose the closest parameters. For example, if `humidity` was -1.1, the Plains biome would be chosen as it has parameters closer to the -1.1 humidity than the Forest biome.

### 🚧 **Under construction** 🚧
