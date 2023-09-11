---
layout: page
title: Glowstone Blob
permalink: /docs/configured-features/feature-types/glowstone-blob/
parent: Configured Features
grand_parent: Documentation
---

## Glowstone Blob

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:glowstone_blob` feature type is used to place a blob of glowstone. In vanilla, this is used in all Nether biomes.

{: .condition }
> This feature is only placed if the placement position is Air and the block above is Netherrack, Basalt, or Blackstone.

### JSON format

<pre>
{
   "type": "minecraft:glowstone_blob",
   "config": {}
}
</pre>

This feature has no fields to configure.