---
layout: page
title: Geode
permalink: /docs/configured-features/feature-types/geode/
parent: Configured Features
grand_parent: Documentation
nav_order: 25
---

## Geode

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:geode` feature type is used to place a geode. In vanilla, these are used to generate Amethyst Geodes for the Overworld.

{: .condition }
> The `invalid_blocks_threshold` configuration affects the placement of this feature (see below).

### Generation explanation

The geode feature type is one of the most complex feature types in the game, so it requires an explanation of its own before each field is explained.

Geodes have a certain number of "distribution points" clustered around where the feature is originally placed. Each point roughly creates a sphere, and with multiple points clustered together you get a vaguely (but not completely) spherical feature. 

For each position within a range relative to the starting position (by default this is a 32x32x32 area centered at where the geode was placed), the distance from the position to the nearest generation point determines what geode layer is placed. Some noise gets added on top of this to make the geode's generation look more random.

### JSON format

<pre>
{
   "type": "minecraft:geode",
   "config": {
      "blocks": {
         "filling_provider": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:air"
            }
         },
         "inner_layer_provider": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:amethyst_block"
            }
         },
         "alternate_inner_layer_provider": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:budding_amethyst"
            }
         },
         "middle_layer_provider": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:calcite"
            }
         },
         "outer_layer_provider": {
            "type": "minecraft:simple_state_provider",
            "state": {
               "Name": "minecraft:smooth_basalt"
            }
         },
         "inner_placements": [
            {
               "Name": "minecraft:small_amethyst_bud",
               "Properties": {
                  "facing": "up",
                  "waterlogged": "false"
               }
            }
         ],
         "cannot_replace": "#minecraft:features_cannot_replace",
         "invalid_blocks": "#minecraft:geode_invalid_blocks"
      },
      "layers": {
         "filling": 1.7,
         "inner_layer": 2.2,
         "middle_layer": 3.2,
         "outer_layer": 4.2
      },
      "crack": {
         "generate_crack_chance": 0.95,
         "base_crack_size": 2,
         "crack_point_offset": 2
      },
      "noise_multiplier": 0.05,
      "use_potential_placements_chance": 0.35,
      "use_alternate_layer0_chance": 0.083,
      "placements_require_layer0_alternate": true,
      "outer_wall_distance": {
         "type": "minecraft:uniform",
         "value": {
            "min_inclusive": 4,
            "max_inclusive": 6
         }
      },
      "distribution_points": {
         "type": "minecraft:uniform",
         "value": {
            "min_inclusive": 3,
            "max_inclusive": 4
         }
      },
      "point_offset": {
         "type": "minecraft:uniform",
         "value": {
            "min_inclusive": 1,
            "max_inclusive": 2
         }
      },
      "min_gen_offset": -16,
      "max_gen_offset": 16,
      "invalid_blocks_threshold": 1
   }
}
</pre>

* `blocks`: The blocks to use for the geode.
   * `filling_provider`: The block provider that will be used for the center layer of the geode. In amethyst geodes, this is Air.
   * `inner_layer_provider`: The block provider that will be used for the inner layer of the geode. In amethyst geodes, this is Amethyst Blocks.
   * `alternate_inner_layer_provider`: The block provider that will be used instead of the `inner_layer_provider` depending on the chance provided by the `use_alternate_layer0_chance` field. In amethyst geodes, this is Budding Amethyst.
   * `middle_layer_provider`: The block provider that will be used for the middle layer of the geode. In amethyst geodes, this is Calcite.
   * `outer_layer_provider`: The block provider that will be used for the outermost layer of the geode. In amethyst geodes, this is Smooth Basalt.
   * <span int>[I]</span> `inner_placements`: A list of block providers that will be placed on the inner layer. In amethyst geodes, this is all of the Amethyst Bud sizes.
   * `cannot_replace`: A block tag for the blocks the geode cannot replace. *Unlike other block tags, this one cannot be inlined as a list of blocks. It MUST be a block tag reference.*
   * `invalid_blocks`: A block tag for blocks that are invalid for the geode to place in. If the number of distribution points in the geode that are in invalid blocks is greater than the `invalid_blocks_threshold` count. *Unlike other block tags, this one cannot be inlined as a list of blocks. It MUST be a block tag reference.*

{: .warning }
The `invalid_blocks` field is bugged, and is completely ignored by the game. The `#minecraft:geode_invalid_blocks` tag is always checked.

* `layers`: The radius of each layer. Each value in this is a double that can range from 0.01 to 5.0.
   * <span double>[D]</span> `filling`: (optional) The radius of the filling layer. Defaults to 1.7.
   * <span double>[D]</span> `inner_layer`: (optional) The radius of the inner layer. Defaults to 2.2.
   * <span double>[D]</span> `middle_layer`: (optional) The radius of the middle layer. Defaults to 3.2.
   * <span double>[D]</span> `outer_layer`: (optional) The radius of the outer layer. Defaults to 4.2.
* `crack`: The configuration for the generation of a "crack" in the geode.
   * <span double>[D]</span> `generate_crack_chance`: The chance that a crack generates on the geode, as a value between 0.0 and 1.0.
   * <span double>[D]</span> `base_crack_size`: The size of the crack, as a value between 0.0 and 5.0.
   * <span int>[I]</span> `crack_point_offset`: The offset of the point where the crack starts, as a value between 0 and 5. A higher `crack_point_offset` value leads to the crack starting closer to the center of the geode.
* <span double>[D]</span> `noise_multiplier`: (optional) The value that the noise sampler gets multiplied by, as a value between 0.0 and 1.0. Defaults to 0.05. A high multiplier may lead to swiss cheese-like generation and lighting issues, so **be careful**!
* <span double>[D]</span> `use_potential_placements_chance`: (optional) The chance for a block in the `inner_placements` list to be placed on an inner layer block, as a value between 0.0 and 1.0. Defaults to 0.35.
* <span double>[D]</span> `use_alternate_layer0_chance`: (optional) The chance for the block in the `alternate_inner_layer_provider` to be used instead of  the block in the `inner_layer_provider`, as a value between 0.0 and 1.0. Defaults to 0.0.
* <span bool>[B]</span> `placements_require_layer0_alternate`: (optional) Determines whether or not the the inner placement block must be placed on an alternate inner layer block. Defaults to true.
* <span int>[I]</span> `outer_wall_distance`: (optional) The distance each distribution point moves, as an integer provider between 1 and 20. Defaults to a uniform integer provider between 4 and 5.
* <span int>[I]</span> `distribution_points`: (optional) The number of distribution points, as an integer provider between 1 and 20. Defaults to a uniform integer provider between 3 and 4.
* <span int>[I]</span> `point_offset`: (optional) The size of the sphere that each distribution point creates, as an integer provider between 1 and 10. Defaults to a uniform integer provider between 1 and 2.
* <span int>[I]</span> `min_gen_offset`: (optional) The minimum distance between a position and the geode center that the geode will attempt to place blocks in. Defaults to -16.
* <span int>[I]</span> `max_gen_offset`: (optional) The maximum distance between a position and the geode center that the geode will attempt to place blocks in. Defaults to -16.
* <span int>[I]</span> `invalid_blocks_threshold`: The maximum amount of distribution points that are allowed to be in invalid blocks. If the number of distribution points that are in invalid blocks exceed this value, the geode fails to place.