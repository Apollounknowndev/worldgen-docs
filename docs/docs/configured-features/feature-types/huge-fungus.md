---
layout: page
title: Huge Fungus
permalink: /docs/configured-features/feature-types/huge-fungus/
parent: Configured Features
grand_parent: Documentation
nav_order: 28
---

## Huge Fungus

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:huge_fungus` feature type is used to place a huge fungus. In vanilla, this is used for huge Crimson and Warped fungi.

{: .condition }
> The placement of this feature depends on the `valid_base_block` and `planted` configurations (see below).

### Json format

<pre>
{
   "type": "minecraft:huge_fungus",
   "config": {
      "hat_state": {
         "Name": "minecraft:nether_wart_block"
      },
      "decor_state": {
         "Name": "minecraft:shroomlight"
      },
      "stem_state": {
         "Name": "minecraft:crimson_stem",
         "Properties": {
            "axis": "y"
         }
      },
      "valid_base_block": {
         "Name": "minecraft:crimson_nylium"
      },
      "planted": true
   }
}
</pre>

* `hat_state`: The block state that will be used for the cap of the fungus.
* `decor_state`: The block state that will be used for decoration in the cap.
* `stem_state`: The block state that will be used for the stem of the fungus.
* `stem_state`: The block state that the fungus must be planted on.
* ‌<or>[B]</or> `planted`: (optional) If enabled, the fungus can generate above the world generation height limit (not the dimension height limit) and can replace plants upon generation. Defaults to false.