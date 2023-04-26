---
layout: page
title: Sculk Patch
permalink: /docs/configured-features/feature-types/sculk-patch/
parent: Configured Features
grand_parent: Documentation
nav_order: 49
---

## Sculk Patch

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:sculk_patch` feature type is used to generate a patch of sculk. In vanilla, it is used in the Deep Dark biome.

### Generation explanation

The game takes the values from the configured feature config and simulates sculk spreading with it. This is why sculk from world and sculk from Sculk Catalysts look so similar.

### JSON format

<pre>
{
   "type": "minecraft:sculk_patch",
   "config": {
      "charge_count": 10,
      "amount_per_charge": 32,
      "spread_attempts": 64,
      "growth_rounds": 0,
      "spread_rounds": 1,
      "extra_rare_growths": 2,
      "catalyst_chance": 0.5
   }
}
</pre>

* <span int>[I]</span> `charge_count`: The number of charges in this sculk patch, as a value between 1 and 32.
* <span int>[I]</span> `amount_per_charge`: The initial value of each chargem as a value between 1 and 500.
* <span int>[I]</span> `spread_attempts`: The amount of attempts for the sculk to spread for each spread round, as a value between 1 and 64.
* <span int>[I]</span> `growth_rounds`: The number of growth rounds, as a value between 0 and 8.
* <span int>[I]</span> `spread_rounds`: The number of spread rounds, as a value between 0 and 8.
* <span int>[I]</span> `extra_rare_growths`: The maximum number of attempts for a Sculk Shrieker to be generated, as an integer provider.
* <span float>[F]</span> `catalyst_chance`: The chance for a Sculk Catalyst to generate, as a value between 0.0 and 1.0.