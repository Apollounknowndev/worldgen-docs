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


## JSON format

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
* `downfall`: 

Float
{: .label .label-green }
Controls the grass and foliage color if those colors are unset.
* `effects`: The effects in the biome.
    * `additions_sound`: (optional) The additional sound settings.
        * `sound`: The ID for the sound to be used.
        * `tick_change`: The chance per tick for the sound to start being played, as a value between 0 and 1.
    * `ambient_sound`: (optional) The ID for the ambient sound to be used.
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
* `features`: (can be empty) The list of placed features to use. Inside this list can be up to 11 lists of placed features. Without any features this will look like this:
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

* `has_precipitation`: Determines whether or not preciptation happens. If the biome temperature is low enough, the precipitation will be snow instead of rain.
* `spawn_costs`: (can be empty) The list of mobs that use the spawn cost mechanism. The spawn cost mechanism is effectively social distancing for mob spawning, where mobs cannot spawn too close to each other. Learn more about this mechanic [here](https://minecraft.fandom.com/wiki/Spawn#Spawn_costs).
    * `<entity id>`: The entity ID of the mob.
        * `energy_budget`: The maximum potential for a possible mob spawn.
        * `charge`: The mob's charge.
    
    Example of how this looks:
    
    ```json
    "spawn_costs": {
       "minecraft:enderman": {
          "energy_budget": 0.15,
          "charge": 0.7
       },
       "minecraft:ghast": {
          "energy_budget": 0.15,
          "charge": 0.7
       }
    }
    ```
* `spawners`: (can be empty) The mob spawn settings.
    * `<mob category>`: The mob category. Must be `monster`, `creature`, `ambient`, `axolotls`, `underground_water_creature`, `water_creature`, `water_ambient`, or `misc`. A list of elements.
        * `type`: The entity ID of the mob.
        * `weight`: The weight of the mob in comparison to other mobs in the category.
        * `minCount`: The minimum amount of mobs that can spawn as a pack.
        * `maxCount`: The maximum amount of mobs that can spawn as a pack.

    Example of how this looks:

    ```json
    "spawners": {
       "creature": [
          {
             "type": "minecraft:strider",
             "weight": 60,
             "minCount": 1,
             "maxCount": 2
          }
       ],
       "monster": [
          {
             "type": "minecraft:zombified_piglin",
             "weight": 1,
             "minCount": 2,
             "maxCount": 4
          }
       ]
    }
    ```

* `temperature`: Controls the grass and foliage color if those colors are unset. Also controls things like the altitude where snow starts, whether rain or so is the precipitation of the biome, and details of some generation features.
* `temperature_modifier`: (optional) The temperature modifier to use.
    * If set to `none`, no temperature modifier will be applied.
    * If set to `frozen`, the temperature will flucuate in the biome somewhat, occasionally reaching above 0.2 where it can rain. Only used in the Frozen Ocean biomes in vanilla.

## Examples

This is the absolute bare minimum a biome file needs to be a valid biome:
```json
{
   "temperature": 0.5,
   "downfall": 0.5,
   "has_precipitation": false,
   "effects": {
      "sky_color": 8103167,
      "fog_color": 12638463,
      "water_color": 4159204,
      "water_fog_color": 329011
   },
   "spawners": {},
   "spawn_costs": {},
   "carvers": {},
   "features": []
}
```

This biome would have no features like ores/trees, no old caves/ravines, no rain, and no mob spawns. The Void biome in vanilla is exactly the same to this, although it includes ambient cave sounds.

```json
{
   "temperature": 0.8,
   "downfall": 0.4,
   "has_precipitation": true,
   "effects": {
      "sky_color": 7907327,
      "fog_color": 12638463,
      "water_color": 4159204,
      "water_fog_color": 329011,
      "mood_sound": {
         "sound": "minecraft:ambient.cave",
         "tick_delay": 6000,
         "block_search_extent": 8,
         "offset": 2
      }
   },
   "spawners": {
      "creature": [
         {
            "type": "minecraft:sheep",
            "weight": 12,
            "minCount": 4,
            "maxCount": 4
         }
      ]
   },
   "spawn_costs": {},
   "carvers": {
      "air": [
         "minecraft:cave",
         "minecraft:cave_extra_underground",
         "minecraft:canyon"
      ]
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
      [],
      [],
      [],
      [],
      []
   ]
}
```

Now we're getting somewhere. This biome is similar to the vanilla Plains biome, but the only entity that spawns is the Sheep and Amethyst Geodes are the only feature that generates.
