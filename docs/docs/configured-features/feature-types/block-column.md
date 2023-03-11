---
layout: page
title: Block Column
permalink: /docs/configured-features/feature-types/block-column/
parent: Configured Features
grand_parent: Documentation
nav_order: 5
---

## Block Column

<style>
re {color:#FF6F6F;font-weight:bold}
or {color:#FEC856;font-weight:bold}
bl {color:#5573FF;font-weight:bold}
pu {color:#CE52FE;font-weight:bold}
</style>

The `minecraft:block_column` feature type is used to place a column of blocks in any direction. The blocks used in the columns are placed in "layers". This can be used to have a lantern hanging from a column of chains, for example. In vanilla, this feature type is used for the glow berry vines in Lush Caves.

### JSON format

```json
{
   "type": "minecraft:block_column",
   "config": {
      "direction": "down",
      "allowed_placement": {
         "type": "minecraft:true"
      },
      "prioritize_tip": false,
      "layers": [
         {
            "height": 4,
            "provider": {
               "type": "minecraft:simple_state_provider",
               "state": {
                  "Name": "minecraft:stone"
               }
            }
         }
      ]
   }
}
```

* ‌<pu>[S]</pu> `direction`: The direction the block column will place blocks. Either `up`, `down`, `north`, `east`, `south`, or `west`.
* `allowed_placement`: The [block predicate](/docs/misc/block-predicates/) that must be passed for the block column to continue placing blocks. It is run each time a block is attempted to be placed.
* ‌<or>[B]</or> `prioritize_tip`: Determines how the game will cut off blocks if the full block column cannot be generated. If set to `true`, blocks will start being cut off from the base so that the tip of the column will still generate.
* ‌<re>[L]</re> `layers`: (can be empty) The list of blocks to be used in the column. The block column starts with the first entries in the list and works down through all the entries in the list.
   * ‌<bl>[I]</bl> `height`: The number of blocks to be placed for the layer.
   * `provider`: The block provider that will be used for the layer.

### Additional Info

You may notice in some cases that the block column will stop one block before it reaches the point where the block predicate would fail. For example, here's what happens when a block column places downwards and the block predicate checks for air:

![(Image of the block column stopping a block before hitting the ground)](/docs/docs/configured-features/feature-types/images/block-column/1.png)

This happens because the game moves the block predicate check one block in the specified `direction` before testing the first block. For downwards facing block columns, this means the block predicate filter is always ran one block below where it should be run. This can be fixed by adding an offset to the block predicate filter like this:

```json
{
   "type": "minecraft:matching_blocks",
   "offset": [
      0,
      1,
      0
   ],
   "blocks": "minecraft:air"
}
```

Adding that offset fixes the issue.

![(Image of the block column touching the ground)](/docs/docs/configured-features/feature-types/images/block-column/2.png)

The offset should be opposite of the `direction` for any given direction. If your block column goes up, the offset should be one block down. If your block column goes west, the offset should be one block east. This is the same across all directions.