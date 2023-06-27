---
layout: page
title: Updating Worldgen Packs
permalink: /guides/misc/pack-updating/
parent: Misc
grand_parent: Guides
nav_order: 2
---

# Updating Worldgen Packs

<head>
    {% include field-type-colors.html %}
</head>

The changes between versions since 1.18 have been for the most part minimal. This guide will cover updates from 1.18 all the way to 1.20.

{: .note }
Several changes listed here include the removal of fields in certain files. **These can still be in the files**, but they will do nothing.

[misode.github.io](https://misode.github.io/upgrader/) has a datapack upgrader if you do not wish to update your datapacks manually.

## 1.18 -> 1.18.2

- Several fields now require tags to have `#` prepended before them. This includes the following:
  - The `infiniburn` field in dimension types
  - The `cannot_replace` and `invalid_blocks` fields in the `minecraft:geode` configured feature type
  - The `replaceable` field in the `minecraft:vegetation_patch` and `minecraft:waterlogged_vegetation_patch` configured feature types
  - The `root_replaceable` field in the `minecraft:root_system` configured feature type
  - The `value` field in the `minecraft:protected_blocks` structure processor type

1.18.1
<pre>
{
  ...
  "effects": "minecraft:overworld",
  "infiniburn": "minecraft:infiniburn_overworld",
  ...
}
</pre>

1.18.2
<pre>
{
  ...
  "effects": "minecraft:overworld",
  "infiniburn": "#minecraft:infiniburn_overworld",
  ...
}
</pre>

- With the introduction of data-driven cave generation, aquifers and ore veins, several large changes were made to `noise_settings` files.
  - The `noise_caves_enabled`, `noodle_caves_enabled`, and `structures` fields have been removed.
  - There's a new field named `noise_router`. It contains 11 inner fields, which all accept density functions (a new thing in this version!):
    - `barrier` (used for aquifers)
    - `fluid_level_floodedness` (used for aquifers)
    - `fluid_level_spread` (used for aquifers)
    - `lava` (used for aquifers)
    - `temperature` (used for biome noise parameters)
    - `vegetation` (used for biome noise parameters)
    - `continents` (used for biome noise parameters)
    - `erosion` (used for biome noise parameters)
    - `depth` (used for biome noise parameters and aquifers)
    - `initial_density_without_jaggedness` (used for aquifers and surface rules)
    - `final_density` (the actual final terrain shaping)
    - `vein_toggle` (used for ore veins)
    - `vein_ridged` (used for ore veins)
    - `vein_gap` (used for ore veins)
    It is highly recommended that you look at how the vanilla Overworld, Nether and End dimensions handled this change.

1.18.1
<pre>
{
  "sea_level": 63,
  "disable_mob_generation": false,
  "noise_caves_enabled": true,
  "noodle_caves_enabled": true,
  ...
  "structures": {
    ...
  },
  "surface_rule": ...
}
</pre>

1.18.2
<pre>
{
  "sea_level": 63,
  "disable_mob_generation": false,
  ...
  "noise_router": {
    "barrier": ...,
    "fluid_level_floodedness": ...,
    "fluid_level_spread": ...,
    "lava": ...,
    "temperature": ...,
    "vegetation": ...,
    "continents": ...,
    "erosion": ...,
    "depth": ...,
    "ridges": ...,
    "initial_density_without_jaggedness": ...,
    "final_density": ...,
    "vein_toggle": ...,
    "vein_ridged": ...,
    "vein_gap": ... 
  },
  "surface_rule": ...
}
</pre>

- Structure support has returned after being missing from 1.18 and 1.18.1! While this leads to a bunch of changes with how structures generation works, the upgrading tutorial will only cover the breaking changes that have been caused from this.
  Configured structure features now have three new fields:
  - `biomes`, which is a biome tag. Determines the biomes the structure can spawn in.
  - `adapt_noise`, which is a boolean. Determines whether or not terrain is adapted around the structure. Defaults to false.
  - `spawn_overrides`, which is formatted similarly to the `spawners` field in biomes. It determines the mob spawn overrides in the structure.

1.18.1
<pre>
{
  "type": "minecraft:monument",
  "config": {}
}
</pre>

1.18.2
<pre>
{
  "type": "minecraft:monument",
  "biomes": "#minecraft:has_structure/ocean_monument",
  "adapt_noise": false,
  "spawn_overrides": {
    "axolotls": {
      "bounding_box": "full",
      "spawns": []
    },
    "monster": {
      "bounding_box": "full",
      "spawns": [
        {
          "type": "minecraft:guardian",
          "weight": 1,
          "minCount": 2,
          "maxCount": 4
        }
      ]
    },
    "underground_water_creature": {
      "bounding_box": "full",
      "spawns": []
    }
  },
  "config": {}
}
</pre>

-----

## 1.18.2 -> 1.19

- The `type` field in dimension files can no longer accept an inlined dimension type, it must be a reference to a separate dimension type file.
- The `seed` field in the `minecraft:noise` generator type and `minecraft:the_end` biome source type has been removed.
- The `category` field in biomes has been removed, all functionality has been moved to biome tags.
- The `min_value` and `max_value` fields in the `minecraft:spline` density function type been removed. Use the `minecraft:clamp` density function to get the same effect.
- Configured structure features have been moved from `worldgen/configured_structure_feature` to `worldgen/structure`.
- The following fields have been removed from noise settings files due to being fully delegated to density functions:
  - `terrain_shaper`
  - `sampling`
  - `top_slide`
  - `bottom_slide`
  
  On top of this, the `minecraft:slide` and `minecraft:terrain_shaper_spline` density functions have been removed. The former has been replaced by a combination of the `minecraft:add`, `minecraft:mul` and `minecraft:y_clamped_gradient` density functions (view the vanilla worldgen fields to see how the Overworld, Nether and End do it), and the latter has been replaced by the `minecraft:spline` density function.

1.18.2
<pre>
{
  ...
  "default_fluid": {
    "Name": "minecraft:water",
    "Properties": {
      "level": "0"
    }
  },
  "noise": {
    "min_y": -64,
    "height": 384,
    "size_horizontal": 1,
    "size_vertical": 2,
    "sampling": {
      "xz_scale": 0.9999999814507745,
      "y_scale": 0.9999999814507745,
      "xz_factor": 80,
      "y_factor": 160
    },
    "bottom_slide": {
      "target": 0.1171875,
      "size": 3,
      "offset": 0
    },
    "top_slide": {
      "target": -0.078125,
      "size": 2,
      "offset": 8
    },
    "terrain_shaper": {
      "offset": 0,
      "factor": 0,
      "jaggedness": 0
    }
  },
  "noise_router": ...
}
</pre>

1.19
<pre>
{
  ...
  "default_fluid": {
    "Name": "minecraft:water",
    "Properties": {
      "level": "0"
    }
  },
  "noise": {
    "min_y": -64,
    "height": 384,
    "size_horizontal": 1,
    "size_vertical": 2
  },
  "noise_router": ...
}
</pre>

- The `concentric_rings` structure placement type has a new field `preferred_biomes`, which is a biome tag. It determines the biomes that structures in the structure set prefer.

- Changed structure generation in several large ways.
  - All fields in the `config` field have been moved to the root field.
  - Added new field `step`, which is a generation step. It can be either `raw_generation`, `lakes`, `local_modifications`, `underground_structures`, `surface_structures`, `strongholds`, `underground_ores`, `underground_decoration`, `fluid_springs`, `vegetal_decoration`, or `top_layer_modification`.
  - Removed boolean field `adapt_noise`, and replaced it with `terrain_adaption`. It can be either `none`, `beard_thin`, `beard_box`, or `bury`. Defaults to `none`.
  - All other changes are specific to certain structure types.
    - `minecraft:mineshaft`:
      - The `type` field has been renamed to `mineshaft_type`.
      - The `probability` field has been removed, as structure sets now handle its functionality.
    - `minecraft:ruined_portal`:
      
      The `portal_type` field has been removed, with the `setups` field taking its place. The `setups` field is a list of different ruined portal setup configurations. This list cannot be empty.
        - `weight`: The weight of this ruined portal setup compared to others in the list, as an integer.
        - `placement`: The portal placement type. Can be either `on_land_surface`, `partly_buried`, `on_ocean_floor`, `in_mountain`, `underground`, or `in_nether`.
        - `air_pocket_probability`: The probability that the ruined portal will generate with a pocket of air around it, as a float between 0.0 and 1.0.
        - `mossiness`: How mossy the ruined portal is, as a float between 0.0 and 1.0.
        - `overgrown`: Whether or not the ruined portal generates with jungle leaves around, as a boolean.
        - `vines`: Whether or not the ruined portal generates with vines on it, as a boolean.
        - `can_be_cold`: Whether or not the ruined portal can replace magma and lava with netherrack, as a boolean.
        - `replace_with_blackstone`: Whether or not stone bricks should be replaced with their blackstone equivalent, as a boolean.
    - `minecraft:bastion`, `minecraft:pillager_outpost` and `minecraft:village`:
      
      The three jigsaw-based structure types have been merged into one structure type: `minecraft:jigsaw`. It has all the existing fields from each structure type, with five new ones:
        - `start_height`: The height the structure generates at, as a height provider.
        - `project_start_to_heightmap`: The optional heightmap to project the structure onto. 
          - If `project_start_to_heightmap` is absent, the `start_height` height is where the structure starts. If `project_start_to_heightmap` exists, the `start_height` *relative* to the given heightmap is where the structure starts.
        - `max_distance_from_center`: The maximum distance from the structure start that the structure can extend out to, as an integer between 1 and 128. If you don't know what value to set it to, set it to 80 as that was the previous hardcoded value.
        - `use_expansion_hack`: A boolean. Only used for vanilla villages and pillager outposts, should be disabled for anything else.
        - `start_jigsaw_name`: An optional jigsaw name. The jigsaw name here is where the structure actually attaches to.

1.18.2
<pre>
{
  "type": "minecraft:village",
  "biomes": "#minecraft:has_structure/village_plains",
  "adapt_noise": true,
  "spawn_overrides": {},
  "config": {
    "start_pool": "minecraft:village/plains/town_centers",
    "size": 6
  }
}
</pre>

1.19
<pre>
{
  "type": "minecraft:jigsaw",
  "biomes": "#minecraft:has_structure/village_plains",
  "step": "surface_structures",
  "spawn_overrides": {},
  "terrain_adaptation": "beard_thin",
  "start_pool": "minecraft:village/plains/town_centers",
  "size": 6,
  "start_height": {
    "absolute": 2
  },
  "project_start_to_heightmap": "WORLD_SURFACE_WG",
  "max_distance_from_center": 80,
  "use_expansion_hack": true
}
</pre>

- Changed the configuration for the `minecraft:disk` configured feature type.
  - Removed the `state` block state field, with it being replaced with `state_provider`. The new field has two fields:
    - `rules`: The list of rules to check. If all fail, the `fallback` state is used. Not optional, but can be empty.
      - `if_true`: The [block predicate](/docs/misc/block-predicates/) that must be passed for the `then` block state to be used.
      - `then`: The block state that should be used if the block predicate from `if_true` passes.
    - `fallback`: The block state provider used if all `rules` fail.
  - Removed the `targets` block state list field, with a `target` block predicate field taking its place.
  - There is no longer a hardcoded check for the origin position to be `minecraft:water`, as the `block_predicate_filter` placement modifier in placed features has this functionality.
- The `minecraft:ice_patch` configured feature type has been removed as all functionality was merged into the `minecraft:disk` configured feature type.

1.18.2
<pre>
{
  "type": "minecraft:ice_patch",
  "config": {
    "state": {
      "Name": "minecraft:packed_ice"
    },
    "radius": 2,
    "half_height": 1,
    "targets": [
      {
        "Name": "minecraft:grass_block",
        "Properties": {
          "snowy": "false"
        }
      },
      {
        "Name": "minecraft:snow_block"
      }
    ]
  }
}
</pre>

1.19
<pre>
{
  "type": "minecraft:disk",
  "config": {
    "state_provider": {
      "fallback": {
        "type": "minecraft:simple_state_provider",
        "state": {
          "Name": "minecraft:packed_ice"
        }
      },
      "rules": []
    },
    "target": {
      "type": "minecraft:matching_blocks",
      "blocks": [
        "minecraft:grass_block",
        "minecraft:snow_block"
      ]
    },
    "radius": 2,
    "half_height": 1
  }
}
</pre>

- Renamed the `minecraft:glow_lichen` configured feature type to `minecraft:multiface_growth` as single sculk veins now use it. No change to configuration made.

1.18.2
<pre>
{
  "type": "minecraft:glow_lichen",
  "config": {
    ...
  }
}
</pre>

1.19
<pre>
{
  "type": "minecraft:multiface_growth",
  "config": {
    ...
  }
}
</pre>

- Added two new fields to dimension types: 
  - `monster_spawn_block_light_limit`, which is an integer. Controls the maximum block light level that mobs can spawn at.
  - `monster_spawn_light_level`, which is an integer provider. Controls the light levels where mobs can spawn.

1.18.2
<pre>
{
  ...
  "min_y": -64,
  "height": 384,
}
</pre>

1.19
<pre>
{
  ...
  "min_y": -64,
  "height": 384,
  "monster_spawn_light_level": {
    "type": "minecraft:uniform",
    "value": {
      "min_inclusive": 0,
      "max_inclusive": 7
    }
  },
  "monster_spawn_block_light_limit": 0
}
</pre>

- Added field `replaceable` to configured carvers, which is a block tag for the blocks carvers can replace.

1.18.2
<pre>
{
  ...
  "lava_level": {
    "above_bottom": 8
  },
  "horizontal_radius_multiplier": 1,
  ...
}
</pre>

1.19
<pre>
{
  ...
  "lava_level": {
    "above_bottom": 8
  },
  "replaceable": "#minecraft:overworld_carver_replaceables",
  "horizontal_radius_multiplier": 1,
  ...
}
</pre>

- Added field `probability` to the `minecraft:leave_vine` tree decorator type, which is a float between 0.0 and 1.0. Previously this was a hardcoded value of 0.25.

1.18.2
<pre>
{
  "type": "minecraft:leave_vine",
  "probability": 0.25
}
</pre>

1.19
<pre>
{
  "type": "minecraft:leave_vine",
  "probability": 0.25
}
</pre>

- Added five new integer fields to the `minecraft:old_blended_noise` density function type: `xz_scale`, `y_scale`, `xz_factor`, `y_factor`, and `smear_scale_multiplier`. All of these values were split off from the noise settings file.

1.18.2
<pre>
{
  "type": "minecraft:old_blended_noise"
}
</pre>

1.19
<pre>
{
  "type": "minecraft:old_blended_noise",
  "xz_scale": 0.25,
  "y_scale": 0.125,
  "xz_factor": 80,
  "y_factor": 160,
  "smear_scale_multiplier": 8
}
</pre>

-----

## 1.19 -> 1.19.3

- The `name` field in template pools has been removed.

1.19
<pre>
{
  "name": "minecraft:empty",
  "fallback": "minecraft:empty",
  "elements": []
}
</pre>

1.19.3
<pre>
{
  "fallback": "minecraft:empty",
  "elements": []
}
</pre>

-----

## 1.19.3 -> 1.19.4

- Biomes no longer have a `precipitation` field that accepts either `rain`, `snow`, or `none`. They now have a `has_precipitation` field which is a boolean. Whether or not snow generates in the biome now depend on the biome's `temperature`.

1.19.3
<pre>
{
  ...
  "downfall": 0.4,
  "precipitation": "rain",
  "effects": {
    ...
  }
}
</pre>

1.19.4
<pre>
{
  ...
  "downfall": 0.4,
  "has_precipitation": true,
  "effects": {
    ...
  }
}
</pre>

-----

## 1.19.4 -> 1.20

- The `rule` structure processor no longer has an `output_nbt` field that accepts a string. It instead has a `block_entity_modifier` field that accepts a block entity modifier (guide on that coming at some point).

1.19.4
<pre>
{
  ...
  "output_state": {
    "Name": "minecraft:chest"
  },
  "output_nbt": "{\"LootTableSeed\":123}"
}
</pre>

1.20
<pre>
{
  ...
  "output_state": {
    "Name": "minecraft:chest"
  },
  "block_entity_modifier": {
    "type": "minecraft:append_static",
    "data": {\"LootTableSeed\":123}
  }
}
</pre>

- The `minecraft:huge_fungus` feature has a new field: `replaceable_blocks`, which is a block predicate for blocks that can be replaced by the fungus.

1.19.4
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
    "planted": false
  }
}
</pre>

1.20
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
    "replaceable_blocks": {
      "type": "minecraft:matching_blocks",
      "blocks": [
        ...
      ]
    },
    "planted": false
  }
}
</pre>