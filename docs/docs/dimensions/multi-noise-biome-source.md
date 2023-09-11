---
layout: default
title: Multi-Noise Biome Source
permalink: /docs/dimensions/multi-noise/
parent: Dimensions
grand_parent: Documentation
nav_order: 3
---

# Multi-Noise Biome Source

<head>
    {% include field-type-colors.html %}
</head>


{: .warning }
This page is not complete yet.


The multi-noise system is used to place biomes at certain places of the world. The biome being placed is based on six inputs:

* `continentalness`
* `erosion`
* `temperature`
* `humidity`
* `weirdness`
* `depth`

The first five inputs are based on perlin noise, and the sixth one is based on the depth relative to the surface.

While these names in vanilla make some logical sense to how they place biomes (i.e. desert biomes generate where `temperature` is high and ocean biomes generate where `continentalness` is low), the names are arbitray; Nothing is stopping you from having a snowy biome that only generates when the input `temperature` is very high, for example.

Each block in the world has the inputs stored. When the game goes to place biomes, the block will give the game its input values and the game will output the biome to be placed at that block.

A dimension file has a list of biomes and their ideal inputs (known in the files as their "parameters"), which are a list of parameters and min/max values which are preferred. This is rather complex to explain, so we'll start with one input (one "dimension" of noise) and work our way up to the full six inputs (six "dimensions" of noise). here's an example with just two biomes, the Plains and the Forest:

<pre>
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
</pre>
Here, the Plains biome will generate if `humidity` is between -1 and 0 and the Forest biome will generate if `humidity` is between 0 and 1. Since all other parameters are set to 0, they do not matter.

The `humidity` value normally fluctuates between -1 and 1, but what if it goes outside the range? If no biomes in the biome source match the parameters, the game will choose the closest parameters. For example, if `humidity` was -1.1, the Plains biome would be chosen as it has parameters closer to the -1.1 humidity than the Forest biome.

Here's a more complex example. This time we'll use 2 inputs and 9 biomes in a grid. Since a list of 9 biomes would be very long, we'll visualize it in a grid instead.

![](/assets/images/docs/multi-noise-biome-source/2d_grid.png)

For this example, the inputs will be the following: 
* `humidity` value of 0.3
* `temperature` value of 0.6 

![](/assets/images/docs/multi-noise-biome-source/2d_grid_with_point.png)

* Since the `humidity` value is 0.3, the input fits into the middle column of this biome grid. 
* Since the `temperature` value is 0.6, the input fits into the bottom row of this biome grid. 

This means that when the `humidity` input is 0.3 and the `temperature` input is 0.6, the gray biome will generate.

### 🚧 **Under construction** 🚧
