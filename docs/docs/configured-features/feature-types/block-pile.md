---
layout: page
title: Block Pile
permalink: /docs/configured-features/feature-types/block-pile/
parent: Configured Features
grand_parent: Documentation
---

## Block Pile

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:block_pile` feature type is used to place a pile of blocks. In vanilla, this feature type is used to place piles of Hay in Villages.

{: .condition }
> This feature is not placed if the placement position is within the bottom 5 blocks of the world. 
>
> Additionally, each block in the pile is only placed if the block below it has a sturdy upper face or is a Dirt Path. In the latter case the block is only placed with a probability of 50%. 

### JSON format

<pre>
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
</pre>

* `state_provider`: The block provider that will be used for the block pile.