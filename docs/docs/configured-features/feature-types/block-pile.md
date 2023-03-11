---
layout: page
title: Block Pile
permalink: /docs/configured-features/feature-types/block-pile/
parent: Configured Features
grand_parent: Documentation
nav_order: 6
---

## Block Pile

The `minecraft:block_pile` feature type is used to place a pile of blocks. In vanilla, this feature type is used to place piles of Hay in Villages.

### JSON format

```json
{
   "type": "minecraft:block_pile",
   "config": {
      "state_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:stone"
         }
      }
   }
}
```

* `state_provider`: The block provider that will be used for the block pile.