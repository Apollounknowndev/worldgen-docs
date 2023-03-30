---
layout: page
title: Coral Claw
permalink: /docs/configured-features/feature-types/coral-claw/
parent: Configured Features
grand_parent: Documentation
nav_order: 10
---

## Coral Claw

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:coral_claw` feature type is used to place one type of coral. In vanilla, it is placed in the Warm Ocean biome.

{: .condition }
> This feature is only placed if the block at its starting position is Water or in the `minecraft:corals` block tag and the block above is Water.

### JSON format

<pre>
{
   "type": "minecraft:coral_claw",
   "config": {}
}
</pre>

This feature has no fields to configure.