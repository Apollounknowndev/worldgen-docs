---
layout: page
title: Building Placed Features
permalink: /guides/features/building-placed-features/
parent: Features
grand_parent: Guides
---

# Building Placed Features

<head>
    {% include field-type-colors.html %}
</head>

{: .warning }
This page is not complete yet.

A major part of world generation is placing all of the small features like trees, rocks and grass. Placing these features correctly is important, as otherwise you may have features fail to generate at all or features that generate in strange positions. The guide will go through the process of building a placed feature for a few different features.

It is recommended you look at [this](docs/placed-features/placement-modifiers) documentation page to understand the concept of placement modifiers and the different types of placement modifiers whilst following this guide.

### Placing a tree

Let's place some oak trees on the surface, at about the same density as trees in the Forest biome.

Download [this](/assets/files/guides/building-placed-features/tree-feature-template.zip) datapack and unzip it. It contains all of the files needed for the tutorial. When you create a world with the datapack, it should generate only the Forest biome with no trees.

![A vanilla forest biome with no trees](/assets/images/guides/building-placed-features/no-trees.png)
-----

With the opened pack, navigate to `data/example/worldgen/placed_feature/trees.json` (we will be ignoring the other files in this tutorial). When you open it, you should see this:

<pre>
{
  "feature": "minecraft:oak",
  "placement": []
}
</pre>

The game doesn't know what height to put the tree at or how many trees per chunk should generate, so it will try to generate a tree once per chunk at the bottom of the world. Since trees cant generate with blocks next to them, the tree placement will always fail. Let's fix that!

Let's start by getting our trees to the surface. There is a `heightmap` placement modifier that moves the feature to a given heightmap, so let's add it to the `placement` list. The specifics of heightmaps aren't important here, so just use `WORLD_SURFACE`. The placed feature should now look like this:

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    }
  ]
}
</pre>

Create a new world with the updated pack aaaaand...

![Forest biome with trees in a grid](/assets/images/guides/building-placed-features/grid-trees.png)
-----

...that's not *quite* what we wanted. The features are all spawning in a grid, which doesn't look natural at all, and they're spawning on blocks they shouldn't like sand and water. Let's ignore the water issue for now and focus on the grid spawning issue. This can be fixed by adding an `in_square` placement modifier, a placement modifier that moves the feature around in the chunk. The placed feature should now look like this:

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    },
    {
      "type": "minecraft:in_square"
    }
  ]
}
</pre>

Open a world with the datapack, and this will be the result.

![Forest biome with no tree grid, but some floating trees](/assets/images/guides/building-placed-features/floating-trees.png)
-----

Wait, how did that happen? Didn't we move the trees to the `WORLD_SURFACE` heightmap? Well, this is due to the placement modifier order.

One of the most important aspects about placed features to know is that placement modifiers are ran in order, one after another. In the example above, we moved the tree to the `WORLD_SURFACE` heightmap at the corner of the chunk and then moved the feature to a random x/z position in the chunk. 

To fix this, the feature should be put on the heightmap *after* its x/z position have already been determined. It's as simple as changing the order of the placement modifiers. The fixed placed feature should now look like this:

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:in_square"
    },
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    }
  ]
}
</pre>

Open the world with the datapack, and you'll see that trees no longer float in the air!

![Sparse forest biome with trees in water](/assets/images/guides/building-placed-features/sparse-trees.png)
-----

Next, let's increase the number of trees. There is a `count` placement modifier that increases the number of feature placements per chunk. Let's add this modifier with a `count` of 10. Here is what the placed feature should look like now:

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:in_square"
    },
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    },
    {
      "type": "minecraft:count",
      "count": 10
    }
  ]
}
</pre>

Wait, remember the placement modifier order that was mentioned earlier? Think about how this will effect this placed feature. Right now, the steps happen in this order:
- Move a tree randomly in the x/z position in the chunk
- Elevate the tree to the `WORLD_SURFACE` heightmap
- Increase the number of trees per chunk to 10

Every tree is generated in the same position, because we never tell them to be placed independently of one another. If the `count` placement modifier is first, each tree placement will run the next placement modifiers separately from one another, meaning there will be 10 attempts per chunk to place a tree, all at random positions in the chunk. The placed feature should look like this: 

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:count",
      "count": 10
    },
    {
      "type": "minecraft:in_square"
    },
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    }
  ]
}
</pre>

In game, it now looks like this:

![Forest biome, with trees stacking on one another](/assets/images/guides/building-placed-features/stacking-trees.png)
-----

Why are trees are stacking on top of other trees now? This is due to the fact that features get placed one at the time; this means a tree can move to the `WORLD_SURFACE` heightmap after another tree has generated at that position, moving the new tree above the previous one.

The `block_predicate_filter` placement modifier prevents a feature from generating if a [block predicate](/docs/misc/block-predicates/) condition is not met. There's a block predicate called `would_survive` for testing if a certain block could last at a certain position. If an oak sapling can't survive in a position, a tree shouldn't generate there. Therefore, a `would_survive` block predicate should be used checking if an `oak_sapling` can survive at the position.

While we're fixing tree stacking, let's also fix trees in water.

The `surface_water_depth_filter` placement modifier prevents a feature from generating if the depth of water at the x/z position is above a certain maximum depth. If `max_water_depth` is set to 0, it means the feature can never generate if it would be in a body of water like a river or lake.


With these two placement modifiers, the placed feature now looks like this:

<pre>
{
  "feature": "minecraft:oak",
  "placement": [
    {
      "type": "minecraft:count",
      "count": 10
    },
    {
      "type": "minecraft:in_square"
    },
    {
      "type": "minecraft:heightmap",
      "heightmap": "WORLD_SURFACE"
    },
    {
      "type": "minecraft:surface_water_depth_filter",
      "max_water_depth": 0
    },
    {
      "type": "minecraft:block_predicate_filter",
      "predicate": {
        "type": "minecraft:would_survive",
        "state": {
          "Name": "minecraft:oak_sapling",
          "Properties": {
            "stage": "0"
          }
        }
      }
    }
  ]
}
</pre>

One more time, let's open the game with the datapack. If you've done everything correctly, this should be the result:

![A forest biome with no generation issues](/assets/images/guides/building-placed-features/final-trees.png)