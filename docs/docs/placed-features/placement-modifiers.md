---
layout: page
title: Placement Modifiers
permalink: /docs/worldgen/placed-features/placement-modifiers/
parent: Placed Features
grand_parent: Documentation
---

# Placement Modifiers

<head>
    {% include field-type-colors.html %}
</head>

When the game is told to place a feature, it needs more information than just "place this feature". How frequently should it generate? At what elevations should it generate at? Should it only generate if floating in air? Placement modifiers are how this information is given to the game. Let's take a look at an example placed feature to see this in action:

<pre>
{
   "feature": "minecraft:oak",
   "placement": [
<span mark-1>       {
         "type": "minecraft:count",
         "count": 4
      },</span>
<span mark-2>      {
         "type": "minecraft:random_offset",
         "xz_spread": {
            "type": "minecraft:uniform",
            "value": {
               "min_inclusive": 0,
               "max_inclusive": 15
            }
         },
         "y_spread": 0
      },</span>
<span mark-3>      {
         "type": "minecraft:heightmap",
         "heightmap": "OCEAN_FLOOR"
      },</span>
<span mark-4>      {
         "type": "minecraft:block_predicate_filter",
         "predicate": {
            "type": "minecraft:matching_blocks",
            "offset": [
               0,
               -1,
               0
            ],
            "blocks": "minecraft:grass_block"
         }
      }</span>
   ]
}
</pre>

When the games goes to place this feature, the following information is given (in this specific order):

<span mark-1>-</span> The feature should be placed 4 times per chunk Each "feature placement" runs the next steps independently of one another.

<span mark-2>-</span> The placement should be moved to a random x/z position in the chunk.

<span mark-3>-</span> The placement should be moved vertically to the `OCEAN_FLOOR` heightmap.

<span mark-4>-</span> The placement should be removed if the block below it is not `minecraft:grass_block`.

Each placement modifier in the `placement` list has a `type` field to tell the game which placement modifier type to use. Further fields (if any) are determined based on the placement modifier type.

The 15 current placement modifiers types can be fit into 3 broad categories, although some types could fit into multiple categories. These categories are count, condition, and position. Below is a list of all placement modifiers in their respective categories.

- Count
   - [Count](#count-1)
   - [Noise Based Count](#noise_based_count)
   - [Noise Threshold Count](#noise_threshold_count)
- Condition
   - [Biome](#biome)
   - [Block Predicate Filter](#block_predicate_filter)
   - [Environment Scan](#environment_scan)
   - [Rarity Filter](#rarity_filter)
   - [Surface Relative Threshold Filter](#surface_relative_threshold_filter)
   - [Surface Water Depth Filter](#surface_water_depth_filter)
- Position
   - [Carving Mask](#carving_mask)
   - [Count On Every Layer](#count_on_every_layer)
   - [Height Range](#height_range)
   - [Heightmap](#heightmap)
   - [In Square](#in_square)
   - [Random Offset](#random_offset)

## Count

These placement modifiers alter the number of times a feature is placed per chunk.

### `count`

This placement modifier simply makes copies of the current feature placement(s).

- <span int>[I]</span> `count`: The number of feature placements at the current placement position, as an integer provider. Cannot be lower than 0 or higher than 256.

### `noise_based_count`

This placement modifier makes copies of the current feature placements(s), with the number of copies depending on a noise sampled at the current placement position. The noise sampled is hardcoded into the placement modifier type and there is no way to configure it.

- <span int>[I]</span> `noise_to_count_ratio`: The ratio of the number of copies to the noise sampled.
- <span double>[D]</span> `noise_factor`: The scale of the noise sampled. Unlike other instances of noise scaling in data-driven worldgen, increasing this value decreases the scale (meaning how quickly the noise varies decreases). 
- <span double>[D]</span> `noise_offset`: Offsets the noise output before the `noise_to_count_ratio` is factored in. Defaults to 0.0.

The below images show where features are placed at a birds-eye view, with a red square indicating a feature placement.

This image is where the `noise_factor` is 20.

![A visualization of feature placements, with about a dozen small areas with a few feature placements](/assets/images/docs/placement-modifiers/nbc-factor-20.png)

This image is where the `noise_factor` is 40.

![A visualization of feature placements, with three small areas with a few feature placements and three large areas with many](/assets/images/docs/placement-modifiers/nbc-factor-40.png)

The image where the `noise_factor` is higher has slower-moving noise, and thus has fewer, larger condensed areas of features.

### `noise_threshold_count`

This placement modifier makes copies of the current feature placements(s), with the number of copies depending on whether or not a noise sampled at the current placement position is above a threshold.

- <span double>[D]</span> `noise_level`: The threshold that determines whether the `above_noise` count or the `below_noise` count is used.
- <span int>[I]</span> `below_noise`: The count that is used if the noise output is less than the `noise_level` theshold.
- <span int>[I]</span> `below_noise`: The count that is used if the noise output is greater than or equal to the `noise_level` theshold.


## Condition
These placement modifiers only allow feature placements to pass if a condition is met. If the condition is not met, the feature placement is scrapped.

### `biome`

This condition passes if the feature placement is in the same biome that the placed feature was referenced from. This prevents features leaking into other biomes, i.e. Birch trees "leaking" into a Dark Forest biome that was in the same chunk.

**If a configured feature references a placed feature that has a `biome` placement modifier, the game will crash!** See [here](/guides/misc/fixing-common-errors/#tried-to-biome-check-an-unregistered-feature) for more information.

This placement modifier has no fields to configure.

### `block_predicate_filter`

This condition passes if a block predicate is met.

- `predicate`: The block predicate to check. See [here](/docs/misc/block-predicates/) for all the details on how block predicates work.

### `environment_scan`

The feature placement scans either up or down a certain number of blocks from the current position to find a positioon where a block predicate is met. If no position is found, the condition fails.

- <span str>[S]</span> `direction_of_search`: The direction to search. Must be either `up` or `down`.
- <span int>[I]</span> `max_steps`: The maximum number of blocks that will be scanned, as an integer between 1 and 32.
- `target_condition`: The block predicate being searched for. See [here](/docs/misc/block-predicates/) for all the details on how block predicates work.
- `allowed_search_condition`: (optional) The block predicate that each block checked must pass for the search to continue.

### `rarity_filter`

The condition passes if a random probability is met.

- <span int>[I]</span> `chance`: The chance for the feature placement to pass, as an integer. The odds for the feature placement to pass is 1/`chance`.

### `surface_relative_threshold_filter`

The condition passes if the current position is in a given range relative to a heightmap.

- <span str>[S]</span> `heightmap`: The heightmap to be checking against. See [here](/docs/misc/heightmaps/) for information on the different heightmap types.
- <span int>[I]</span> `min_inclusive`: The minimum vertical value relative to the heightmap where the condition passes. If left blank, there is no minimum.
- <span int>[I]</span> `max_inclusive`: The maximum vertical value relative to the heightmap where the condition passes. If left blank, there is no maximum.

### `surface_water_depth_filter`

The condition passes if the difference of the `WORLD_SURFACE` and `OCEAN_FLOOR` heightmaps at the given position is less than or equal to the given threshold. Note that the condition returns the same result for any elevation; the feature doesn't need to be in water for the condition to fail.

- <span int>[I]</span> `max_water_depth`: The maximum difference of the aforementioned heightmaps where the feature is still placed.


## Position
These placement modifiers alter how feature placement(s) are positioned in the world.

### `carving_mask`

The placement modifier removes all current feature placements and returns new placements positioned at every single block in the chunk carved out by a carver cave. This placement modifier is mostly useless in vanilla, as noise caves and structures won't be checked.

- <span str>[S]</span> `step`: The carving step to use. Either `liquid` or `air`.

### `count_on_every_layer`

The placement modifier is a combination of the `count`, `in_square`, and a custom `heightmap` all in one. It's primary use is in dimensions with a roof, like the Nether. 

- `count`: The number of feature placements per vertical elevation. Cannot be lower than 0 or higher than 256.

### `height_range`

The placement modifier moves the elevation of the feature placement based on a height provider.

- <span int>[I]</span> `height`: The height provider for where the feature placement is placed.

### `heightmap`

The placement modifier moves the elevation of the feature placement to the given heightmap.

- <span str>[S]</span> `heightmap`: The heightmap to move the feature placement to. See [here](/docs/misc/heightmaps/) for information on the different heightmap types.

### `in_square`

The placement modifier adds a random value between 0 and 15 (inclusive) to the current position. If no other horiztonal positioning placement modifiers have been used, this randomizes the placement to be at any x/z position in the starting chunk.

This placement modifier has no fields to configure.

### `random_offset`

The placement modifier offsets the current feature placement on each axis.

- <span int>[I]</span> `xz_spread`: The offset on the x-axis and z-axis, as an integer provider between -16 and 16. Even though both horizontal axes use the same integer provider, they can output different values for each axis.
- <span int>[I]</span> `y_spread`: The offset of the y-axis, as an integer provider between -16 and 16.