---
layout: page
title: Introduction
permalink: /docs/worldgen/placed-features/introduction/
parent: Placed Features
grand_parent: Documentation
nav_order: 1
---

# Intro to Placed Features

<head>
    {% include field-type-colors.html %}
</head>

Placed feature files contain information about how a configured feature is placed in the world. 

### What is a feature?

A feature is a "decoration" that gets placed after the world's terrain shaping has been done. Small features like trees, rocks, plants, and ores are all features. Some small structures like dungeons, overworld fossils and desert wells are also features. Features cannot be located with `/locate`; this is why you can't use `/locate` to find dungeons.

Placed features are stored in the `/worldgen/placed_feature` folder. They are referenced either from the `features` list in biome files, or in some specific configured feature types such as the `vegetation_feature` field in the `minecraft:vegetation_patch` feature type.

## JSON format

A placed feature consists of two fields, as seen in this example:

<pre>
{
   "feature": "minecraft:oak",
   "placement": [
      {
         "type": "minecraft:count",
         "count": 4
      },
      {
         "type": "minecraft:in_square"
      },
      {
         "type": "minecraft:heightmap",
         "heightmap": "OCEAN_FLOOR"
      }
   ]
}
</pre>

The placed feature has two fields:

* <span str>[S]</span> `feature`: The ID of the configured feature to place. This references a file in the `/worldgen/configured_feature` folder.
* <span list>[L]</span> `placement`: A list of placement modifiers to change how the feature is placed. Each placement modifier is run in order, changing how many of a feature is placed, where in the chunk a feature is placed, etc. If the list is empty, the feature will place itself on the northwesternmost corner of each chunk at the bottom layer of the world.
