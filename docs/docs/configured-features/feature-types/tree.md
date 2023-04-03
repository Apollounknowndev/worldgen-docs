---
layout: page
title: Tree
permalink: /docs/configured-features/feature-types/tree/
parent: Configured Features
grand_parent: Documentation
nav_order: 55
---

## Tree

<head>
    {% include field-type-colors.html %}
</head>

{: .note }
The game's code needs to be checked to get the complete information to finish this page.

The `minecraft:tree` feature type is used to place a tree. In vanilla, the feature is used to generate all Overworld trees.

### Generation explanation

Tree reference trunk placers and foliage providers. Trunk placers determine the shape of the tree trunk, and near the top of them foliage placer(s) are attached. They can also optionally have a root placer for the trunk to be placed on, and decorators to apply to the tree after the trunk and foliage have been generated.

### JSON format

<pre>
{
  "type": "minecraft:tree",
  "config": {
    "ignore_vines": true,
    "force_dirt": false,
    "minimum_size": {
      "type": "minecraft:two_layers_feature_size",
      "limit": 1,
      "lower_size": 0,
      "upper_size": 1
    },
    "dirt_provider": {
      "type": "minecraft:simple_state_provider",
      "state": {
        "Name": "minecraft:dirt"
      }
    },
    "trunk_provider": {
      "type": "minecraft:simple_state_provider",
      "state": {
        "Name": "minecraft:oak_log",
        "Properties": {
          "axis": "y"
        }
      }
    },
    "foliage_provider": {
      "type": "minecraft:simple_state_provider",
      "state": {
        "Name": "minecraft:oak_leaves",
        "Properties": {
          "distance": "7",
          "persistent": "false",
          "waterlogged": "false"
        }
      }
    },
    "trunk_placer": {
      "type": "minecraft:straight_trunk_placer",
      "base_height": 4,
      "height_rand_a": 2,
      "height_rand_b": 0
    },
    "foliage_placer": {
      "type": "minecraft:blob_foliage_placer",
      "radius": 2,
      "offset": 0,
      "height": 3
    },
    "decorators": [
      {
        "type": "minecraft:beehive",
        "probability": 0.01
      }
    ]
  }
}
</pre>

* ‌<or>[B]</or> `ignore_vines`: (optional) Whether or not the tree will place regardless of if vines would block it. Defaults to false.
* ‌<or>[B]</or> `force_dirt`: (optional) Whether or not the block state in `dirt_provider` will be forcefully placed under the tree trunk. Defaults to false.
* `minimum_size`: The minimum feature size. This is used to prevent the tree from being placed within a certain distance of other trees or from generating on steep terrain.
  * ‌<pu>[S]</pu> `type`: The feature size type. Can either be `minecraft:two_layers_feature_size` or `minecraft:three_layers_feature_size`.
    * ‌<bl>[I]</bl> `min_clipped_height`: (optional) The minimum height where the tree will generate even if there's blocks that would normally prevent it from being placed. Value between 0 and 80, defaults to null.
    * If set to `minecraft:two_layers_feature_size`, the further fields are as follows:
      * ‌<bl>[I]</bl> `limit`: (optional) The threshold value above which `upper_size` is used. At and below this threshold, `lower_size` is used instead. A `limit` of 2 means the bottom two layers of the tree trunk use the `lower_size` while all other layers of the tree trunk use the `upper_size`. Value between 0 and 81, defaults to 1.
      * ‌<bl>[I]</bl> `lower_size`: (optional) The radius to check when at and below the `limit`. A `lower_size` of 2 means that the game will check every block in a 5x5 area centered on the tree trunk to make sure it is either air, water, a plant, or in the `#minecraft:logs` tag. If any of these checks fail, the tree will not place. Value between 0 and 16, defaults to 0.
      * ‌<bl>[I]</bl> `upper_size`: (optional) The radius to check when above the `limit`. See `lower_size` for details on how this value is used. Value between 0 and 16, defaults to 1.
    * If set to `minecraft:three_layers_feature_size`, the further fields are as follows:
      * ‌<bl>[I]</bl> `limit`: (optional) The threshold value below which `lower_size` is used. Value between 0 and 81, defaults to 1.
      * ‌<bl>[I]</bl> `upper_limit`: (optional) The threshold value above which which `upper_size` is used. An `upper_limit` of 2 means the top two layers of the tree trunk use the `upper_size` while the layers of the tree trunk down to where `lower_limit` is use the `middle_size`. Value between 0 and 81, defaults to 1.
      * ‌<bl>[I]</bl> `lower_size`: (optional) The radius to check when below the `limit`. A `lower_size` of 2 means that the game will check every block in a 5x5 area centered on the tree trunk to make sure it is either air, water, a plant, or in the `#minecraft:logs` tag. If any of these checks fail, the tree will not place. Value between 0 and 16, defaults to 0.
      * ‌<bl>[I]</bl> `middle_size`: (optional) The radius to check when at or above the `limit` but below the `upper_limit`. See `lower_size` for details on how this value is used. Value between 0 and 16, defaults to 1.
      * ‌<bl>[I]</bl> `upper_size`: (optional) The radius to check when at or above the `upper_limit`. See `lower_size` for details on how this value is used. Value between 0 and 16, defaults to 1.
* `dirt_provider`: The block state provider to use for dirt under the tree trunk.
* `trunk_provider`: The block state provider to use for the tree trunk.
* `foliage_provider`: The block state provider to use for the foliage of the tree.
* `root_placer`: (optional) The root placer for the tree.
  * ‌<pu>[S]</pu> `type`: The root placer type to use. The current only option is `minecraft:mangrove_root_placer`.
    * `root_provider`: The block state provider to use for the roots.
    * ‌<bl>[I]</bl> `trunk_offset_y`: The offset of the trunk from the starting position, as an integer provider.
    * `above_root_placement`: (optional) The block placement above the roots.
      * `above_root_provider`: The block state provider to use for the block above the root.
      * ‌<ye>[F]</ye> `above_root_placement_chance`: The chance for the `above_root_provider` to be placed on each root block, as a value between 0.1 and 1.0.
    * If the root placer type is `minecraft:mangrove_root_placer`, the further fields are as follows:
      * `mangrove_root_placement`: The placement of the mangrove roots.
        * ‌<bl>[I]</bl> `max_root_width`: The maximum width of the roots (not accounting for skewing), as a value between 1 and 12.
        * ‌<bl>[I]</bl> `max_root_length`: The maximum length of the roots (not accounting for skewing), as a value between 1 and 64.
        * ‌<ye>[F]</ye> `random_skew`: The chance that the root will extend out an extra block, as a value between 0.0 and 1.0.
        * `can_growth_through`: A block tag for the blocks that the roots in `root_provider` can grow through.
        * `muddy_roots_in`: A block tag for the blocks that the muddy roots in `muddy_root_provider` can grow through.
        * `muddy_roots_provider`: The block state provider to use for the muddy roots.
* `trunk_placer`: The trunk placer for the tree.
  * ‌<pu>[S]</pu> `type`: The trunk placer type to use. Can be `minecraft:bending_trunk_placer`, `minecraft:cherry_trunk_placer`, `minecraft:dark_oak_trunk_placer`, `minecraft:fancy_trunk_placer`, `minecraft:forking_trunk_placer`, `minecraft:giant_trunk_placer`, `minecraft:mega_jungle_trunk_placer`, `minecraft:straight_trunk_placer`, or `minecraft:upwards_branching_trunk_placer`.
  * ‌<bl>[I]</bl> `base_height`: The base height of the tree, as an integer between 0 and 32.
  * ‌<bl>[I]</bl> `height_rand_a`: A random amount of height to add to the tree height, as an integer between 0 and 32. Anywhere between 0 and `height_rand_a` blocks of height will be added to the `base_height` to get the final tree height.
  * ‌<bl>[I]</bl> `height_rand_b`: A random amount of height to add to the tree height, as an integer between 0 and 24. Functions identically to `height_rand_b`.
  * If the trunk placer type is `minecraft:dark_oak_trunk_placer`, `minecraft:fancy_trunk_placer`, `minecraft:forking_trunk_placer`, `minecraft:giant_trunk_placer`, `minecraft:mega_jungle_trunk_placer`, `minecraft:straight_trunk_placer`, there are no further fields.
  * If the trunk placer type is `minecraft:bending_trunk_placer`, the further fields are as follows:
    * ‌<bl>[I]</bl> `bend_length`: The length of the tree bend. This is not exact, so you may rarely see a tree extend horizontally a block over the maximum of `bend_length`. Integer provider between 1 and 64.
    * ‌<bl>[I]</bl> `min_height_for_leaves`: The minimum height of the trunk where leaves will generate, as a positive value.
  * If the trunk placer type is `minecraft:cherry_trunk_placer`, the further fields are as follows:
    * ‌<bl>[I]</bl> `branch_count`: The number of branches on the tree, as an integer provider between 1 and 3.
    * ‌<bl>[I]</bl> `branch_end_offset_from_top`: An integer provider between -16 and 16.
    * ‌<bl>[I]</bl> `branch_horizontal_length`: An integer provider between 2 and 16.
    * ‌<bl>[I]</bl> `branch_start_offset_from_top`: An integer provider between 2 and 16.

{: .note }
> `branch_start_offset_from_top` is forced to be a uniform integer provider, and is formatted slightly differently from other integer values. The format looks like this:
> <pre>
  "branch_start_offset_from_top": {
    "max_inclusive": -3,
    "min_inclusive": -4
  },
> </pre>

  * If the trunk placer type is `minecraft:upwards_branching_trunk_placer`, the further fields are as follows:
    * ‌<ye>[F]</ye> `place_branch_per_log_probability`: The chance per log on the main tree trunk that a branch in a random direction will be generated, as a value between 0 and 1.
    * ‌<bl>[I]</bl> `extra_branch_steps`: Positive integer provider.
    * ‌<bl>[I]</bl> `extra_branch_length`: Non-negative integer provider.
    * `can_growth_through`: A block tag for the blocks that the branch can grow through.
* `foliage_placer`: The foliage placer for the tree.
  * ‌<pu>[S]</pu> `type`: The foliage placer type to use. Can be `minecraft:acacia_foliage_placer`, `minecraft:blob_foliage_placer`, `minecraft:bush_foliage_placer`, `minecraft:cherry_foliage_placer`,`minecraft:dark_oak_foliage_placer`, `minecraft:fancy_foliage_placer`, `minecraft:jungle_foliage_placer`, `minecraft:mega_pine_foliage_placer`, `minecraft:pine_foliage_placer`,   `minecraft:random_spread_foliage_placer`, or `minecraft:spruce_foliage_placer`.
  * ‌<bl>[I]</bl> `radius`: The radius of the foliage placer, as an integer provider between 0 and 16.
  * ‌<bl>[I]</bl> `offset`: The offset of the foliage placer from its starting position, as an integer provider between 0 and 16.
  * If the foliage placer type is `minecraft:acacia_foliage_placer` or `minecraft:dark_oak_foliage_placer`, there are no further fields.
  * If the foliage placer type is `minecraft:blob_foliage_placer`, `minecraft:bush_foliage_placer`, `minecraft:fancy_foliage_placer`, `minecraft:jungle_foliage_placer`, or `minecraft:pine_foliage_placer`, the further fields are as follows:
    * ‌<bl>[I]</bl> `height`: The height of the foliage placer, as an integer between 0 and 16.
  * If the foliage placer type is `minecraft:cherry_foliage_placer`,  the further fields are as follows:
    * ‌<ye>[F]</ye> `wide_bottom_layer_hole_chance`: Float between 0.0 and 1.0.
    * ‌<ye>[F]</ye> `corner_hole_chance`: Float between 0.0 and 1.0.
    * ‌<ye>[F]</ye> `hanging_leaves_chance`: Float between 0.0 and 1.0.
    * ‌<ye>[F]</ye> `hanging_leaves_extension_chance`: Float between 0.0 and 1.0.
  * If the foliage placer type is `minecraft:mega_pine_foliage_placer`,  the further fields are as follows:
    * ‌<bl>[I]</bl> `height`: The height of the foliage placer, as an integer provider between 0 and 24.
  * If the foliage placer type is `minecraft:random_spread_foliage_placer`,  the further fields are as follows:
    * ‌<bl>[I]</bl> `height`: The height of the foliage placer, as an integer provider between 1 and 512.
    * ‌<bl>[I]</bl> `leaf_placement_attempts`: The number of attempts to place a leaf block, as an integer between 0 and 256.
  * If the foliage placer type is `minecraft:spruce_foliage_placer`,  the further fields are as follows:
    * ‌<bl>[I]</bl> `trunk_height`: An integer provider between 0 and 24.
* ‌<re>[L]</re> `decorators`: A list of decorators to apply to the tree.
  * ‌<pu>[S]</pu> `type`: The tree decorator type. Can be `minecraft:alter_ground`, `minecraft:attached_to_leaves`, `minecraft:beehive`, `minecraft:cocoa`, `minecraft:leave_vine`, or `minecraft:trunk_vine`.
  * If the tree decorator type is `minecraft:trunk_vine`, there are no further fields.
  * If the tree decorator type is `minecraft:beehive`, `minecraft:cocoa`, or `minecraft:leave_vine`, the further fields are as follows:
    * ‌<ye>[F]</ye> `probability`: The change of the tree decorator occurring, as a float between 0.0 and 1.0.
  * If the tree decorator type is `minecraft:alter_ground`, the further fields are as follows:
    * `provider`: The block state provider to replace the blocks around the tree with.
  * If the tree decorator type is `minecraft:attached_to_leaves`, the further fields are as follows:
    * ‌<ye>[F]</ye> `probability`: The probability of the block in `block_provider` to be attempted to be placed on a leaf block, as a float between 0.0 and 1.0.
    * ‌<bl>[I]</bl> `exclusion_radius_xz`: Integer between 0 and 16.
    * ‌<bl>[I]</bl> `exclusion_radius_y`: Integer between 0 and 16.
    * ‌<bl>[I]</bl> `required_empty_blocks`: The required amount of empty blocks in a direction in `directions` for the block in `block_provider` to be placed. Integer between 0 and 16.
    * `block_provider`: The block provider to use in this tree decorator.
    * ‌<re>[L]</re> `directions`: A list of decorations that this decorator will attempt to generate blocks in relative to each leaf block.