---
layout: page
title: Huge Brown Mushroom
permalink: /docs/configured-features/feature-types/huge-brown-mushroom/
parent: Configured Features
grand_parent: Documentation
nav_order: 27
---

## Huge Brown Mushroom

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:huge_brown_mushroom` feature type is used to place a mushroom with the brown mushroom cap. In vanilla, this is used for the large Brown Mushrooms in the Dark Forest and Mushroom Fields biomes.

{: .condition }
> This feature is only placed if the block below the placement position is in the `minecraft:dirt` or `minecraft:mushroom_grow_block` block tag. Additionally there needs to be sufficient space to place the feature filled with Air or blocks in the `minecraft:leaves` block tag.

### JSON format

<pre>
{
   "type": "minecraft:huge_brown_mushroom",
   "config": {
      "cap_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:brown_concrete"
         }
      },
      "stem_provider": {
         "type": "minecraft:simple_state_provider",
         "state": {
            "Name": "minecraft:white_concrete"
         }
      },
      "foliage_radius": 3
   }
}
</pre>

* `cap_provider`: The block provider that will be used for the cap of the mushroom.
* `stem_provider`: The block provider that will be used for the stem of the mushroom.
* <span int>[I]</span> `foliage_radius`: The radius of the mushroom cap. Defaults to 2.