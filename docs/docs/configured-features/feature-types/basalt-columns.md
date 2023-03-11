---
layout: page
title: Basalt Columns
permalink: /docs/configured-features/feature-types/basalt-columns/
parent: Configured Features
grand_parent: Documentation
nav_order: 3
---

## Basalt Columns

<style>
bl {color:#5573FF;font-weight:bold}
</style>

The `minecraft:basalt_columns` feature type is used to place clusters of basalt columns. In vanilla, this feature type is used to generate a lot of the basalt in the Basalt Delta biome.

### JSON format

```json
{
   "type": "minecraft:basalt_columns",
   "config": {
      "reach": 1,
      "height": 2
   }
}
```

* ‌<bl>[I]</bl> `reach`: The radius of a cluster of basalt, as an integer provider between 0 and 3 (inclusive).
* ‌<bl>[I]</bl> `height`: The maximum height of a cluster of basalt, as an integer provider between 1 and 10 (inclusive).

Please note that multiple clusters of basalt can generate as one feature, so just because the `reach` value is 3 or below, it doesn't mean that the maximum radius for a basalt columns feature is 3.