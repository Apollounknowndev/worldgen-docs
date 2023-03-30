---
layout: page
title: Ice Spike
permalink: /docs/configured-features/feature-types/ice-spike/
parent: Configured Features
grand_parent: Documentation
nav_order: 30
---

## Ice Spike

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:ice_spike` feature type is used to place a large ice spike. In vanilla, this is used in the Ice Spikes biome.

{: .position }
> The placement position is moved downwards until it reaches a non-air block.

{: .condition }
> This feature is only placed if the block at the (moved) placement position is Snow.

### JSON format

<pre>
{
   "type": "minecraft:ice_spike",
   "config": {}
}
</pre>

This feature has no fields to configure.