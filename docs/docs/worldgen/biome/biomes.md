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
* `downfall`: Controls the grass and foliage color if those colors are unset.
* `effects`: The effects in the biome.
    * `additions_sound`: (optional) The additional sound settings.
        * `sound`: The ID for the sound to be used.
        * `tick_change`: The chance per tick for the sound to start being played, as a value between 0 and 1.
    * `ambient_sound`: (optional) The ID for the amount sound to be used.
    * `fog_color`: The fog color in the biome, as a decimal value.
    * `foliage_color`: (optional) The foliage color in the biome, as a decimal value. The downfall and temperature values will determine the foliage color if none is provided.
    * `grass_color`: (optional) The grass color in the biome, as a decimal value. The downfall and temperature values will determine the grass color if none is provided.
    * `grass_color_modifier`: (optional) The grass color modifier to use.
        * If set to `none`, no color modifier will be applied. This is the default.
        * If set to `dark_forest`, 

### 🚧 Under construction 🚧