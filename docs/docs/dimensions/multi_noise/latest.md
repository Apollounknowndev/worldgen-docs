---
layout: default
title: Multi-Noise Biome Source
permalink: /docs/dimensions/multi-noise/latest/
parent: Dimensions
grand_parent: Documentation
nav_order: 3
---

# Multi-Noise Biome Source

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
Here, the Plains biome will generate if `humidity` is between -1 and 0 and the Forst biome will generate if `humidity` is between 0 and 1. Since all other parameters are set to 0, they do not matter.

The `humidity` value normally fluctuates between -1 and 1, but what if it goes outside the range? If no biomes in the biome source match the parameters, the game will choose the closest parameters. For example, if `humidity` was -1.1, the Plains biome would be chosen as it has parameters closer to the -1.1 humidity than the Forest biome.

Here's a more complex example. This time we'll use 2 inputs and 9 biomes in a grid. Since a list of 9 biomes would be very long, we'll visualize it in a grid instead.

![](/docs/docs/dimensions/multi_noise/images/2d/grid.png)

For this example, the inputs will be the following: 
* `humidity` value of 0.3
* `temperature` value of 0.6 

![](/docs/docs/dimensions/multi_noise/images/2d/grid_with_point.png)

* Since the `humidity` value is 0.3, the input fits into the middle column of this biome grid. 
* Since the `temperature` value is 0.6, the input fits into the bottom row of this biome grid. 

This means that when the `humidity` input is 0.3 and the `temperature` input is 0.6, the gray biome will generate.

For vanilla's Nether dimension, two dimensions of noise is enough; with only five biomes, you don't need to use all six parameters. However, the vanilla Overworld, with it's 50+ biomes, *does* need to use all six parameters. What it does to place all these biomes is take a grid like the one shown above and takes it to the extreme by making it six dimensional (technically only 5/6 parameters use a grid, but that will be explained later). This is for practical purposes impossible to visualize all at once, so we'll use three different "layers" of grids to visualize it.

For the following example, [Snowcapped](https://snowcapped.jacobsjo.eu/) will be used to show the biome grids. Snowcapped is an incredibly useful tool for making large and complex biome layouts.

As an example, take a look at this river:

![A river on a coast passing through a Taiga, with a plateau in the background](/docs/docs/dimensions/multi_noise/images/6d/river.png)

Using the F3 screen, the noise parameters can be seen for each block with precision to three decimal places. At the center of the entrance of the river on the river floor, the parameters are as follows:

* `continentalness`: -0.065
* `erosion`: -0.031
* `temperature`: -0.283
* `humidity`: 0.155
* `weirdness`: -0.018
* `depth`: -0.013

We know what the output is already going to be: It's going to be the River biome. But what if you didn't have the image? You can use the biome grids to figure out what biome will generate at a certain block given its noise parameters, which is what we will be doing.

![A grid of more grids, with `weirdness` as the x axis and `depth` as the y axis](/docs/docs/dimensions/multi_noise/images/6d/1.png)

The "first layer" grid can be used to visualize weirdness and depth values. Instead of each cell on the grid correlating to a biome, it correlates to another grid.
With a `weirdness` of -0.018 and a `depth` of -0.013, the middle top cell is the one used.

![Same as the above image, but with the middle top cell in a red box](/docs/docs/dimensions/multi_noise/images/6d/1_with_box.png)

Let's look at the cell that was used.

![A grid of more grids, with `erosion` as the x axis and `continentalness` as the y axis](/docs/docs/dimensions/multi_noise/images/6d/2.png)

The "second layer" grid can be used to visualize erosion and continentalness values. Each cell correlates to another grid.
With an `erosion` of -0.031 and a `continentalness` of -0.006, the cell below the exact middle cell is the one used.

![Same as the above image, but with the cell below the exact middle cell in a red box](/docs/docs/dimensions/multi_noise/images/6d/2_with_box.png)

Let's look at the cell that was used.

![A grid of biomes, with `humidity` as the x axis and `temperature` as the y axis](/docs/docs/dimensions/multi_noise/images/6d/3.png)

The "third layer" grid can be used to visualize humidity and temperature values. Each cell correlates to a biome.
With a `temperature` value of -0.283 and `humidity` value of 0.155, the cell above the right of the exact middle is the one used. This cell correlates to the River biome.

![A grid of biomes, with `humidity` as the x axis and `temperature` as the y axis](/docs/docs/dimensions/multi_noise/images/6d/3_with_box.png)

What did this all mean? This means that with these example parameters as an input:

* `continentalness`: -0.065
* `erosion`: -0.031
* `temperature`: -0.283
* `humidity`: 0.155
* `weirdness`: -0.018
* `depth`: -0.013

The game will output the River biome.


### 🚧 **Under construction** 🚧
