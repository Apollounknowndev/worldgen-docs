---
layout: page
title: Flower
permalink: /docs/configured-features/feature-types/flower/
parent: Configured Features
grand_parent: Documentation
---

## Flower

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:flower` feature type is used to place a patch of placed features. In vanilla, it is used to place patches of flowers.

### JSON format

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

* <span int>[I]</span> `tries`: The number of tries for a placed feature to generate. Can be any positive integer, defaults to 127.
* <span int>[I]</span> `xz_spread`: The x and z-coordinate spread that the feature can generate in, as a radius. Defaults to 7.
* <span int>[I]</span> `y_spread`: The y-coordinate spread that the feature can generate in, as a radius. Defaults to 3.
* `feature`: The placed feature that will be placed.

### Additional Info

This feature is identical to the `minecraft:no_bonemeal_flower` and `minecraft:random_patch` feature in configuration. However, the `minecraft:flower` feature has one unique property; when grass is bonemealed, the game will find the first `minecraft:flower` feature in the biome where the grass was bonemealed and place that feature.