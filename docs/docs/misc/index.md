---
layout: page
title: Heightmaps
permalink: /docs/misc/heightmaps/
parent: Miscellaneous
grand_parent: Documentation
---

# Heightmaps
Heightmaps store the height of the terrain at a given block during world generation. This can be useful in cases where you want features to be on the top of terrain (i.e. trees and rocks). In vanilla, there's six different heightmaps.

## `WORLD_SURFACE`
The `WORLD_SURFACE` heightmap returns the highest block that is not air.

## `WORLD_SURFACE_WG`
Identical to `WORLD_SURFACE`, but is only used during worldgen. It gets scrapped after the chunk finishes generation.

## `OCEAN_FLOOR`
The `OCEAN_FLOOR` heightmap returns the highest block that blocks movement. This is similar to `WORLD_SURFACE`, but it ignores blocks like plants, water, snow layers, cobwebs, etc.

## `OCEAN_FLOOR_WG`
Identical to `OCEAN_FLOOR`, but is only used during worldgen. It gets scrapped after the chunk finishes generation.

## `MOTION_BLOCKING`
The `MOTION_BLOCKING` heightmap returns the highest block that blocks movement *and* isn't a liquid. Similar to `OCEAN_FLOOR`, but the heightmap won't target water blocks.

## `MOTION_BLOCKING_NO_LEAVES`
Identical to `MOTION_BLOCKING`, but leaves are ignored.