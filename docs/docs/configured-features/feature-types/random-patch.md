---
layout: page
title: Random Patch
permalink: /docs/configured-features/feature-types/random-patch/
parent: Configured Features
grand_parent: Documentation
nav_order: 44
---

## Random Patch

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:random_patch` feature type is used to place a patch of placed features. In vanilla, it is used to place patches of lily pads, sugar cane and other block patches.

### Json format

<pre>
{
   "type": "minecraft:flower",
   "config": {
      "tries": 96,
      "xz_spread": 6,
      "y_spread": 2,
      "feature": "foo:bar"
   }
}
</pre>

* ‌<bl>[I]</bl> `tries`: The number of tries for a placed feature to generate. Can be any positive integer, defaults to 127.
* ‌<bl>[I]</bl> `xz_spread`: The x and z-coordinate spread that the feature can generate in, as a radius. Defaults to 7.
* ‌<bl>[I]</bl> `y_spread`: The y-coordinate spread that the feature can generate in, as a radius. Defaults to 3.
* `feature`: The placed feature that will be placed.

### Additional Info

This feature is identical to the `minecraft:flower` and `minecraft:no_bonemeal_flower` feature in configuration.