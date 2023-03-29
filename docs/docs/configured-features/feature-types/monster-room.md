---
layout: page
title: Monster Room
permalink: /docs/configured-features/feature-types/monster-room/
parent: Configured Features
grand_parent: Documentation
nav_order: 35
---

## Monster Room

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:monster_room` feature type is used to place a dungeon. In vanilla, it is placed in the Overworld.

### JSON format

<pre>
{
   "type": "minecraft:monster_room",
   "config": {}
}
</pre>

This feature has no fields to configure.

### Additional info

* When attempting to place a monster room, the game will check for opening in the walls. If 1-5 blocks of openings are found, the monster room will place. Otherwise, the generation will fail.