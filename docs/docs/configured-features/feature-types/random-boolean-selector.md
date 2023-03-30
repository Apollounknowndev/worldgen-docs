---
layout: page
title: Random Boolean Selector
permalink: /docs/configured-features/feature-types/random-boolean-selector/
parent: Configured Features
grand_parent: Documentation
nav_order: 43
---

## Random Boolean Selector

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:random_boolean_selector` feature type is used to choose to place between two different placed features. The chance of each feature generating is equal. In vanilla, this feature is used in the placement of clay pools in Lush Caves and mushroom placement in Mushroom Fields.

### JSON format

<pre>
{
   "type": "minecraft:random_boolean_selector",
   "config": {
      "feature_false": {
         "feature": "minecraft:huge_brown_mushroom",
         "placement": []
      },
      "feature_true": {
         "feature": "minecraft:huge_red_mushroom",
         "placement": []
      }
   }
}
</pre>

* `feature_false`: The first of the two placed feature reference to select from.
* `feature_true`: The second of the two placed feature reference to select from.