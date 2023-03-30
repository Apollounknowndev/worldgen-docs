---
layout: page
title: No Bonemeal Flower
permalink: /docs/configured-features/feature-types/no-bonemeal-flower/
parent: Configured Features
grand_parent: Documentation
nav_order: 39
---

## No Bonemeal Flower

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:no_bonemeal_flower` feature type is used to place a patch of placed features. In vanilla, it is unused.

### JSON format

<pre>
{
   "type": "minecraft:no_bonemeal_flower",
   "config": {
      "tries": 96,
      "xz_spread": 6,
      "y_spread": 2,
      "feature": "foo:bar"
   }
}
</pre>

* ‌<bl>[I]</bl> `tried`: The number of tries for a placed feature to generate. Can be any positive integer, defaults to 127.
* ‌<bl>[I]</bl> `xz_spread`: The x and z-coordinate spread that the feature can generate in, as a radius. Defaults to 7.
* ‌<bl>[I]</bl> `y_spread`: The y-coordinate spread that the feature can generate in, as a radius. Defaults to 3.
* `feature`: The placed feature that will be placed.

### Additional Info

This feature is identical to the `minecraft:flower` and `minecraft:random_patch` feature in configuration. There appears to be no reasons for `minecraft:no_bonemeal_flower` to exist. Use `minecraft:random_patch` instead in case this feature is ever removed.