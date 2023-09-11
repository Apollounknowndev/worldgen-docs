---
layout: page
title: Freeze Top Layer
permalink: /docs/configured-features/feature-types/freeze-top-layer/
parent: Configured Features
grand_parent: Documentation
---

## Freeze Top Layer

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:freeze_top_layer` feature type is used to place snow and ice on the top layer of the world in areas where the biome temperature is low enough. In vanilla, all Overworld biomes place this feature, regardless of whether or not the biome will ever get snow. This prevents chunk border issues between biomes with snow and biomes without snow.

### JSON format

<pre>
{
   "type": "minecraft:freeze_top_layer",
   "config": {}
}
</pre>

This feature has no fields to configure.