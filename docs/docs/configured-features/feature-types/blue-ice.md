---
layout: page
title: Blue Ice
permalink: /docs/configured-features/feature-types/blue-ice/
parent: Configured Features
grand_parent: Documentation
nav_order: 7
---

## Blue Ice

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:blue_ice` feature type is used to place a small iceberg of blue ice. In vanilla, it is used in the Frozen Ocean biome.

{: .extra-info }
The feature will fail to place if it attempts to be placed above sea level, the block or the block above it is not water, or none of the four cardinal directions relative to the starting block are packed ice.

### JSON format

<pre>
{
   "type": "minecraft:blue_ice",
   "config": {}
}
</pre>

This feature has no fields to configure.