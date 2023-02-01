---
layout: page
title: Biomes
permalink: /docs/worldgen/biomes/
parent: Worldgen
grand_parent: Documentation
---

# Biomes

Biome files contain information about a biome such as the sky/water colors, mob spawning, and features used in generation.

They are stored in the `/worldgen/biome` folder.


Let's take a look at an example biome configuration:
```json
{
    "carvers": {},
    "downfall": 0.4,
    "effects": {
        "fog_color": 12638463,
        "mood_sound": {
            "block_search_extent": 8,
            "offset": 2,
            "sound": "minecraft:ambient.cave",
            "tick_delay": 6000
        },
        "sky_color": 7907327,
        "water_color": 4159204,
        "water_fog_color": 329011
    },
    "features": [
        [],
        [],
        [
            "minecraft:amethyst_geode"
        ],
        [],
        [],
        [],
        [
            "minecraft:ore_diamond",
            "minecraft:ore_diamond_large",
            "minecraft:ore_diamond_buried"
        ],
        [],
        [],
        [
            "minecraft:glow_lichen",
            "minecraft:trees_plains",
            "minecraft:flower_plains",
            "minecraft:patch_grass_plain"
        ],
        [
            "minecraft:freeze_top_layer"
        ]
    ],
    "has_precipitation": true,
    "spawn_costs": {},
    "spawners": {
        "ambient": [
            {
                "type": "minecraft:bat",
                "maxCount": 8,
                "minCount": 8,
                "weight": 10
            }
        ],
        "axolotls": [],
        "creature": [],
        "misc": [],
        "monster": [
            {
                "type": "minecraft:zombie",
                "maxCount": 4,
                "minCount": 4,
                "weight": 95
            },
            {
                "type": "minecraft:skeleton",
                "maxCount": 4,
                "minCount": 4,
                "weight": 100
            }
        ],
        "underground_water_creature": [
            {
                "type": "minecraft:glow_squid",
                "maxCount": 6,
                "minCount": 4,
                "weight": 10
            }
        ],
        "water_ambient": [],
        "water_creature": []
    },
    "temperature": 0.8
}
```

There's a lot to configure in biomes. The settings are as follows:

* `carvers`: The configured carvers the biome should use.
    * `air`: (optional) A list of carvers that carve through terrain in the `air` cave generation step. 
    * `liquid`: (optional) A list of carvers that carve through terrain in the `liquid` cave generation step. Unused in vanilla as of 1.18.
* `creature_spawn_probability`: (optional) Controls how frequently creatures spawn, as a value between 0 and 1.
* `downfall`: Controls the grass and foliage color if those colors are unset.
* `effects`: The effects in the biome.
    * `additions_sound`: (optional) The additional sound settings.
        * `sound`: The ID for the sound to be used.
        * `tick_change`: The chance per tick for the sound to start being played, as a value between 0 and 1.
    * `ambient_sound`: (optional) The ID for the amount sound to be used.
    * `fog_color`: The biome's fog color, as a decimal value.
    * `foliage_color`: (optional) The biome's foliage color, as a decimal value. The downfall and temperature values will determine the foliage color if none is provided.
    * `grass_color`: (optional) The biome's grass color, as a decimal value. The downfall and temperature values will determine the grass color if none is provided.
    * `grass_color_modifier`: (optional) The grass color modifier to use.
        * If set to `none`, no color modifier will be applied. This is the default.
        * If set to `dark_forest`, the grass will have the dark forest color.
        * If set to `swamp`, the grass will alternate between the two swamp colors.
    * `mood_sound`: (optional) The mood sound settings.
        * `sound`: The ID for the sound to be used.
        * `tick_delay`: The minimum delay between mood sounds.
        * `block_search_extent`: The range of areas where the mood sound will be played. Centered on the player, the cubic range where a mood sound can be played is calulated as `2 * block_search_extent`.
        * `offset`: The minimum distance from the player that the mood sound can play from.
    * `music`: (optional) The music settings.
        * `sound`: The ID for the music to be played.
        * `min_delay`: The minimum delay being two pieces of music being started, in ticks.
        * `max_delay`: The maximum delay between two pieces of music being started, in ticks.
        * `replace_current_music`: Whether or not music that is already playing should be replaced with new music.
    * `particle`: (optional) The biome particle settings.
        * `probability`: How often the particle should spawn, as a value between 0 and 1. 
        * `options`: The particle options. 
            * `type`: The particle type. For more information on particle fields, see the [wiki article](https://minecraft.fandom.com/wiki/Commands/particle) on particles for more information. 
    * `sky_color`: The biome's sky color, as a decimal value.
    * `water_color`: The biome's water color, as a decimal value.
    * `water_fog_color`: The biome's water fog color, as a decimal value.
* `features`: The list of placed features to use. Inside this list can be up to 11 lists of placed features. Without any features this will look like this:

```json
"features": [
    [],
    [],
    [],
    [],
    [],
    [],
    [],
    [],
    [],
    [],
    []
]
```

Each list corresponds to a generation step. At least in vanilla, certain steps are used to place certain features. The steps are as follows:
    * `RAW_GENERATION`: Only used for the small end islands in the End dimension in vanilla.
    * `LAKES`: Used for placement of lava lakes.
    * `LOCAL_MODIFICATIONS`: Used for placement of Amethyst Geodes and Icebergs.
    * `UNDERGROUND_STRUCTURES`: Used for Monster Rooms (dungeons) and Fossils. **Underground structures such as Mineshafts and Ancient Cities generate during this generation step.**
    * `SURFACE_STRUCTURES`: Used for desert wells and blue ice patches. **Surface structures such as Villages and Shipwrecks generate during this generation step.**
    * `STRONGHOLDS`: Unused. **Strongholds generate during this generation step.**
    * `UNDERGROUND_ORES`: Used for Overworld blobs of alternate stone and ores, and the disks of sand, gravel and clay in rivers.
    * `UNDERGROUND_DECORATION`: Used for Nether blocks of alternate stone and ores, and infested stone.
    * `FLUID_SPRINGS`: Used for the single blocks of lava and water.
    * `VEGETAL_DECORATION`: Used for vegetation like trees, grass, mushrooms, etc.
    * `TOP_LAYER_MODIFICATION`: Used for placing snow and ice in cold areas.

### 🚧 Under construction 🚧