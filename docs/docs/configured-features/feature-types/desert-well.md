---
layout: page
title: Desert Well
permalink: /docs/configured-features/feature-types/desert-well/
parent: Configured Features
grand_parent: Documentation
nav_order: 14
---

## Desert Well

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:desert_well` feature type is used to place desert wells. In vanilla, it is placed in the Desert biome.

{: .position }
> The placement position is moved downwards until it reaches a non-air block.

{: .condition }
> This feature is only placed if the block at the (moved) placement position is Sand (not Red Sand).

### JSON format

<pre>
{
   "type": "minecraft:desert_well",
   "config": {}
}
</pre>

This feature has no fields to configure.