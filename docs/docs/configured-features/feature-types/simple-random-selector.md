---
layout: page
title: Simple Random Selector
permalink: /docs/configured-features/feature-types/simple-random-selector/
parent: Configured Features
grand_parent: Documentation
nav_order: 53
---

## Simple Random Selector

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:simple_random_selector` feature type is used to choose to place between a number of different placed features. The chance of each feature generating is equal. In vanilla, this feature is used in a few places, one of which being the selection of which coral type to place in the Warm Ocean biome.

### JSON format

<pre>
{
   "type": "minecraft:simple_random_selector",
   "config": {
      "features": [
         "foo:bar/feature_a",
         "foo:bar/feature_b",
         "foo:bar/feature_c"
      ]
   }
}
</pre>

* <span list>[L]</span> `features`: The list of placed features to select from. Each placed feature in the list has an equal chance of generating.