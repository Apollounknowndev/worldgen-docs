---
layout: page
title: Monster Room
permalink: /docs/configured-features/feature-types/monster-room/
parent: Configured Features
grand_parent: Documentation
---

## Monster Room

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:monster_room` feature type is used to place a dungeon. In vanilla, it is placed in the Overworld.


{: .condition }
This feature will only place if there are 1-5 blocks of openings in the walls of where the monster room will be placed.

### JSON format

<pre>
{
   "type": "minecraft:monster_room",
   "config": {}
}
</pre>

This feature has no fields to configure.