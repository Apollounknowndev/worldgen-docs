---
layout: page
title: Blue Ice
permalink: /docs/configured-features/feature-types/blue-ice/
parent: Configured Features
grand_parent: Documentation
nav_order: 7
---

## Blue Ice

The `minecraft:blue_ice` feature type is used to place a small iceberg of blue ice. In vanilla, it is used in the Frozen Ocean biome.

### JSON format

<pre>
{
   "type": "minecraft:blue_ice",
   "config": {}
}
</pre>

This feature has no fields to configure.

### Additional Info

* The feature will fail to place if it attempts to be placed above sea level.
* The feature requires the block and the block above it to be water, and one of the four cardinal directions relative to the starting block must be packed ice.