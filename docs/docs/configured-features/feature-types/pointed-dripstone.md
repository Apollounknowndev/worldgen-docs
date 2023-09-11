---
layout: page
title: Pointed Dripstone
permalink: /docs/configured-features/feature-types/pointed-dripstone/
parent: Configured Features
grand_parent: Documentation
---

## Pointed Dripstone

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:pointed_dripstone` feature type is used to place a small patch of dripstone blocks with a Pointed Dripstone on top. In vanilla, this is used in the Dripstone Caves biome.

### JSON format

<pre>
{
   "type": "minecraft:pointed_dripstone",
   "config": {
      "chance_of_taller_dripstone": 0.2,
      "chance_of_directional_spread": 0.7,
      "chance_of_spread_radius2": 0.5,
      "chance_of_spread_radius3": 0.5
   }
}
</pre>

* <span float>[F]</span> `chance_of_taller_dripstone`: (optional) The chance of the pointed dripstone being two blocks tall instead of one. Defaults to 0.2
* <span float>[F]</span> `chance_of_directional_spread`: (optional) The chance of dripstone blocks spreading horizontally. Defaults to 0.7.
* <span float>[F]</span> `chance_of_spread_radius2`: (optional) The chance that the horizontal spread will be two blocks if the dripstone has already spread one block. Defaults to 0.5.
* <span float>[F]</span> `chance_of_spread_radius3`: (optional) The chance that the horizontal spread will be three blocks if the dripstone has already spread two blocks. Defaults to 0.5.