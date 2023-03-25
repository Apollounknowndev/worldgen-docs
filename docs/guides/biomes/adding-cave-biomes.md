---
layout: page
title: Adding Cave Biomes
permalink: /guides/biomes/adding-cave-biomes/
parent: Biomes
grand_parent: Guides
nav_order: 1
---

# Adding Cave Biomes

Compared to adding biomes above ground, adding biomes underground is much simpler. In this tutorial we'll add a Spider Caves biome to the Overworld.

{: .note }
This guide does not show how to create the cave biome itself, but rather shows how to add it to Overworld generation.

Download [this datapack](/docs/guides/biomes/files/adding-cave-biomes/adding-cave-biomes-template.zip), which has all the files needed for this tutorial. Extract the contents of it and open it up in your editor of choice. For this example, Visual Studio Code will be used because it has the incredibly helpful [Datapack Helper Plus](https://marketplace.visualstudio.com/items?itemName=SPGoding.datapack-language-server) extension. You don't actually need a code editor though; you can do this with Notepad if you really want.

Once you open up the datapack in the editor, it should look something like this:

![All of the files in the attached datapack shown](/docs/guides/biomes/images/adding-cave-biomes/folder-structure.png)

Everything in the `example` folder is the code for the actual biome, such as the `spider_caves` biome and the hanging cobwebs feature. You should ignore the contents of that folder for now. This tutorial is focusing on actually adding the biome to generation, which needs to be done through the overworld's dimension file.

Open `data/minecraft/dimension/overworld.json`. This might take a moment to load, as it's a >4 MB file. The vast majority of the contents of this file consist of the biome layout. Each entry in the `biomes` list has two fields: a `biome` string (the ID for the biome to be placed), and a `parameters` object which contains all the parameters for the biome. We'll be adding a new entry to this list.

Scroll all the way down to the bottom and you should see this:

![The last two entries in the biome list](/docs/guides/biomes/images/adding-cave-biomes/last-biome-entries.png)

This image has two biome entries: one for the `minecraft:lush_caves` biome, and one for the `minecraft:deep_dark` biome. Duplicate the `minecraft:lush_caves` entry. It should look like this:

![A duplicate entry of the lush caves entry](/docs/guides/biomes/images/adding-cave-biomes/lush-caves-duplicate-entry.png)

Change `minecraft:lush_caves` in the second entry to `example:spider_caves`. Great! We're almost done. The last part is deciding the parameters where this biome will generate. The lush caves normally has these parameters:

![The Lush Caves parameters](/docs/guides/biomes/images/adding-cave-biomes/lush-caves-parameters.png)

This effectively tells the game to place the Lush Caves underground wherever there is a high `humidity` value. These parameters are typically within a range of `-1` to `1`: since `temperature`, `continentalness`, `erosion`, and `weirdness` contain all values in that range, that means those values will not affect its generation.

For this example, let's give the Spider Caves the opposite parameters; it will only generate where `humidity` is *low*. This is relatively simple to do. Change the humidity parameter from this:

```json
"humidity": [
   0.7,
   1
]
```

To this:

```json
"humidity": [
   -1,
   -0.7
]
```

Leave everything else the same. If you've done everything right, congratulations! You've added a cave biome to overworld generation. Open up Minecraft, create a new world with the datapack and run `/locate biome example:spider_caves`. You should be able to find the new Spider Caves biome!

![Found biome in /locate biome](/docs/guides/biomes/images/adding-cave-biomes/successful-biome-locate.png)
