---
layout: page
title: Fixing Common Errors
permalink: /guides/misc/fixing-common-errors/
parent: Misc
grand_parent: Guides
nav_order: 1
---

# Fixing Common Errors

<head>
    {% include field-type-colors.html %}
</head>

There are many different types of errors that can appear in worldgen packs. This guide will show the most common of these and how to fix them.

### How to view errors

When testing worldgen packs, you will almost certainly need more information than the "Data pack validation failed!" message. The game logs will give you specific information on what is causing issues. 

If you're using the vanilla launcher, go to Settings and activate "Open output log when Minecraft: Java Edition starts". 

If you're not using the vanilla launcher, your game instance should have a screen where you can see the logs.

## Errors

### Unbound values in registry

<pre>
java.lang.IllegalStateException: Unbound values in registry (...)
</pre>

This error occurs when you reference a registry entry that doesn't exist. What does this mean, exactly? We'll use an example. Let's say you have this placed feature:

<pre>
{
  "feature": "minecraft:aok",
  "placement": []
}
</pre>

You will get this error:

<pre>
java.lang.IllegalStateException: Unbound values in registry ResourceKey
[minecraft:root / minecraft:worldgen/configured_feature]: [minecraft:aok]
</pre>

This error tells you that one of your files is trying to reference the `minecraft:aok` configured feature, even though it does not exist. 

In this case, you would need to either change the feature being referenced (probably to `minecraft:oak`) or add a `minecraft:aok` configured feature.

-----

### No key (...) in MapLike

<pre>
java.lang.RuntimeException: No key (...) in MapLike[...]
</pre>

This error occurs when you are missing a required field. For example, take a look at this configured feature:

<pre>
{
  "type": "minecraft:ore",
  "config": {
    "discard_chance_on_air_exposure": 0,
    "targets": [
      {
        "target": {
          "predicate_type": "minecraft:block_match",
          "block": "minecraft:stone"
        },
        "state": {
          "Name": "minecraft:diamond_ore"
        }
      }
    ]
  }
}
</pre>

The game has no clue what the ore's `size` is because the field is missing. Therefore, this error will occur:

<pre>
java.lang.RuntimeException: No key size in MapLike
[{"discard_chance_on_air_exposure":0,"targets":[{"target":{"predicate_type"
:"minecraft:block_match","block":"minecraft:stone"},"state":
{"Name":"minecraft:diamond_ore"}}]}]
</pre>

It's a rather long error due to the game spitting out the entire contents of the file, but it tells you what field you are missing at the very start.

To fix this issue, you'll need to add the key that is missing from the file. In this example, you'd add a `size` value.

**Additional Info**

There is a special case of this error. It will look like this:

<pre>
java.lang.RuntimeException: No key preset in MapLike[...]
</pre>

The [...] will contain the entire dimension file that is causing the error. This can occur for a few different reasons:

- A biome referenced in the dimension file does not exist.
- A biome referenced in the dimension file is invalid.
<pre>
"biomes": [
  {
    "biome": "example:plainss", <--- example:plainss either doesn't exist, or the biome has an error in it
    "parameters": {
      "temperature": 0,
      "humidity": [
        0,
        0
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

- Two values in a parameter range are not in ascending order.
<pre>
"biomes": [
  {
    "biome": "minecraft:plains",
    "parameters": {
      "temperature": 0,
      "humidity": [
        -0.2,
        -0.5 <--- -0.5 is less than -0.2, so it should come first
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

-----

### Feature order cycle

<pre>
java.lang.IllegalStateException: Feature order cycle found, involved biomes: [...]
</pre>

This error occurs when two or more biomes in the same dimension reference the same placed features in the same step, but in different orders to one another.

The game enforces a dimension-wide order to feature placement*. This prevents feature order randomly changing based on the order biomes in a chunk are generated in. For example, let's say Biome A places rocks before trees (in the same step), and Biome B places trees before rocks. If these biomes are in the same chunk, which gets placed first? The answer is that it would differ depending on how the chunk is loaded, making worldgen less deterministic.

*(\* it's actually more complex than that, but for most cases it is functionally dimension-wide.)*

The error should say which biomes are causing the error. For example, this error tells you that the conflicting biomes are `example:forest` and `example:plains`:

<pre>
Feature order cycle found, involved sources: [
Reference{ResourceKey[minecraft:worldgen/biome / example:forest]=net.minecraft.class_1959@36694f06}, 
Reference{ResourceKey[minecraft:worldgen/biome / example:plains]=net.minecraft.class_1959@333681ba}]
</pre>

For this example, let's say these are the feature lists for the biomes:

`example:plains`:
<pre>
"features": [
  [
    "example:trees_forest",
    "example:generic_grass",
    "example:generic_flowers"
  ]
]
</pre>

`example:forest`:
<pre>
"features": [
  [
    "example:trees_plains",
    "example:generic_flowers",
    "example:generic_grass"
  ]
]
</pre>

The `example:generic_flowers` and `example:gemeric_grass` features are in a different order between the two biomes. One biome file should switch around the order of the two features so it is consistent with the other biome file.

**Additional Info**

Due to [MC-252369](https://bugs.mojang.com/browse/MC-252369), there can be some cases where feature order cycles are detected even when none exist. The current best way to fix it is adding a placement modifier to one of the placed features so the game treats it as a separate feature.

-----

### Tried to biome check an unregistered feature

<pre>
java.lang.IllegalStateException: Tried to biome check an unregistered feature, 
or a feature that should not restrict the biome
</pre>

This occurs when a placed feature that has a `biome` placement modifier is referenced by a configured feature.

Let's say you have a placed feature that places a glowstone block in the world. You want it to generate randomly in the chunk, but only in the `minecraft:nether_wastes` biome. You would have a placed feature that looks something like this:

<pre>
{
  "feature": "example:glowstone_block",
  "placement": [
    {
      "type": "minecraft:count",
      "count": 1
    },
    {
      "type": "minecraft:in_square"
    },
    {
      "type": "minecraft:height_range",
      "height": {
        "type": "minecraft:uniform",
        "min_inclusive": {
          "above_bottom": 0
        },
        "max_inclusive": {
          "below_top": 0
        }
      }
    },
    {
      "type": "minecraft:biome"
    }
  ]
}
</pre>

Let's say that the `minecraft:nether_wastes` biome references this feature. It placed one feature attempt per chunk, randomly within the x/y/z bounds of the chunk. Finally, it does a biome check. Since the placed feature was referenced by the `minecraft:nether_wastes` biome, it will check that the current position is in the `minecraft:nether_wastes` biome. If it isn't, the placement is scrapped.

Some configured features can reference placed features, however, so what if one of those references the glowstone block placed feature? Well, it would do the same think (one placement, random position in x/y/z) until it reaches the `minecraft:biome` placement modifier. What biome is it checking for? At this point the game does not keep track of the biome that referenced the initial feature, so it has no biome to check for. This causes the game to freeze up and crash.

The solution is to remove all references to the `minecraft:biome` placement modifier in placed features that are referenced from configured features.