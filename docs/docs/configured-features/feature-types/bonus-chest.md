---
layout: page
title: Bonus Chest
permalink: /docs/configured-features/feature-types/bonus-chest/
parent: Configured Features
grand_parent: Documentation
---

## Bonus Chest

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:bonus_chest` feature type is used to place the game's often forgotten bonus chest.

{: .position }
> The chest is placed at a random position within the chunk at the height of the `MOTION_BLOCKING_NO_LEAVES` heightmap if this position is Air or a block with no collision.
> If there is no block in the chunk that fulfills these conditions the placement fails.

### JSON format

<pre>
{
   "type": "minecraft:bonus_chest",
   "config": {}
}
</pre>

This feature has no fields to configure.