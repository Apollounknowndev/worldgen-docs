---
layout: page
title: Replace Single Block
permalink: /docs/configured-features/feature-types/replace-single-block/
parent: Configured Features
grand_parent: Documentation
nav_order: 46
---

## Replace Single Block

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:replace_single_block` feature type is used to replace a single block in the world with another block. In vanilla, this is currently unused. It was formerly used to place Emerald Ore back before 1.18 when they only generated in veins of one.

### Json format

<pre>
{
  "type": "minecraft:replace_single_block",
  "config": {
    "targets": [
      {
        "target": {
          "predicate_type": "minecraft:block_match",
          "block": "minecraft:stone"
        },
        "state": {
          "Name": "minecraft:emerald_ore"
        }
      }
    ]
  }
}
</pre>

* ‌<re>[L]</re> `targets`: A list of targets for the feature.
    * `target`: The target predicate.
        * `predicate_type`: The rule test that needs to pass for the block in `state` to be placed.
        * `state`: The block state that gets placed if the aforementioned predicate passes.