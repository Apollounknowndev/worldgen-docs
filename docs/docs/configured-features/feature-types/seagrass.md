---
layout: page
title: Seagrass
permalink: /docs/configured-features/feature-types/seagrass/
parent: Configured Features
grand_parent: Documentation
nav_order: 51
---

## Seagrass

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:seagrass` feature type is used to place a single seagrass. In vanilla, this is used in the Ocean and River biomes.

{: .position }
> The placement position of this feature is moved to the height of the `OCEAN_FLOOR` heightmap.
>
> The change in position of where the seagrass is placed on the x and z coordinates relative to the starting point functions identically to an `xz_spread` of 7 with the `minecraft:random_patch` feature type.

### Json format

<pre>
{
   "type": "minecraft:seagrass",
   "config": {
      "probability": 0.6
   }
}
</pre>

* ‌<ye>[F]</ye> `probability`: The chance for tall seagrass to generate instead of normal seagrass, as a float between 0.0 and 1.0.