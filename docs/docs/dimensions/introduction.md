---
layout: default
title: Introduction
permalink: /docs/dimensions/introduction/
parent: Dimensions
grand_parent: Documentation
nav_order: 1
---
<head>
    {% include version-select.html %}
    {% include field-type-colors.html %}
</head>

# Intro to Dimensions

In order for Minecraft to register a dimension, it needs to know three things about it:
* The biomes the dimension uses
* The properties of the dimension (build limit, whether or not there's skylight, etc.)
* The terrain shaping and blocks used in the terrain for the dimension

Dimension files supply the game with all of this information.

Unlike other worldgen files, they are **not** stored in the `/worldgen` folder. They are stored in their own `/dimension` folder.

Let's take a look at an example dimension file. This one is identical to the Overworld, except the only biome is the Plains:

<pre>
{
   "type": "minecraft:overworld",
   "generator": {
      "type": "minecraft:noise",<ver-h data-version="<=1.18.2">      "seed": 0,</ver-h><ver-s data-version=">=1.19"></ver-s>      "settings": "minecraft:overworld",
      "biome_source": {
         "type": "minecraft:multi_noise",
         "biomes": [
            {
               "biome": "minecraft:plains",
               "parameters": {
                  "temperature": [
                     -1,
                     1
                  ],
                  "humidity": [
                     -1,
                     1
                  ],
                  "continentalness": [
                     -1,
                     1
                  ],
                  "erosion": [
                     -1,
                     1
                  ],
                  "weirdness": [
                     -1,
                     1
                  ],
                  "depth": 0,
                  "offset": 0
               }
            }
         ]
      }
   }
}
</pre>

The settings are as follows:

* `type`: The dimension type file this dimension uses. Learn how dimension type files work [here](/docs/dimensions/dimension-types/).
* `generator`: Controls the terrain generation and biome source for the dimension.
	* `type`: The generator type.
		* If set to `minecraft:debug`, there are no further fields. This is only used for the `debug` world type, and doesn't have any practical use.
		* If set to `minecraft:flat`, the further fields are as follows:
			* `settings`: Controls all the superflat settings.
				* `biome`: The biome ID the dimension uses. Defaults to `minecraft:plains`.
				* `features`: Determines whether features like ores, trees, and other vegetation generates. Defaults to false.
				* `lakes`: Determines whether or not lava lakes generate. Defaults to false.
				* `layers`: A list of block layers the dimension should use. The layers get placed in order from the top of the list to the bottom of the list.
					* `block`: The block ID the layer uses.
					* `height`: The number of blocks thick the layer is.
				* `structure_overrides`: A list of structures that the dimension generates. *(May or may not be required, more research needed.)*
		* If set to `minecraft:noise`, the further fields are as follows:
            * <ver-h data-version="<=1.18.2"><code>seed</code>: The seed for the dimension to use. This overrides the world seed and is a required field.</ver-h>
			* `settings`: The noise settings file this dimension uses.
			* `biome_source`: The biome source this dimension uses.
				* `type`: The biome source type.
					* If set to `minecraft:the_end`, there are no further fields. This is used for the End dimension's biome layout, and cannot be configured at all.
					* If set to `minecraft:fixed`, the further fields are as follows:
						* `biome`: The biome used for the entire dimension. Useful if you just want a single biome in your dimension.
					* If set to `minecraft:checkerboard`, the further fields are as follows:
						* `scale`: Must be an integer between 0 and 62 (inclusive), defaults to 2. Controls the size of biomes on the checkerboard. This value is expontential (i.e. a `scale` of 3 leads to 9x9 chunk areas of a biome)
						* `biomes`: A list of biomes that is used in the checkerboard.
					* If set to `minecraft:multi_noise`, the settings are as follows:
						* `preset`: The preset for the biome layout. Can be either `minecraft:overworld` or `minecraft:nether`. **Mutually exclusive with the `biomes` field!**
						* `biomes`: A list of biomes with their respective parameters. Biome parameters are a complex subject and will soon have their own page. **Mutually exclusive with the `preset` field!**