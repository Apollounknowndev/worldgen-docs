# Dimension Types
Dimension type files control the properties of a dimension. These properties include things like whether beds work or not, whether sky light should be calculated, etc.

Unlike other worldgen files, they are **not** stored in the `/worldgen` folder. They are stored in their own `/dimension_type` folder.

Let's take a look at an example dimension type file, this one being for the Overworld:

```
{
  "ambient_light": 0.0,
  "bed_works": true,
  "coordinate_scale": 1.0,
  "effects": "minecraft:overworld",
  "has_ceiling": false,
  "has_raids": true,
  "has_skylight": true,
  "height": 384,
  "infiniburn": "#minecraft:infiniburn_overworld",
  "logical_height": 384,
  "min_y": -64,
  "monster_spawn_block_light_limit": 0,
  "monster_spawn_light_level": {
    "type": "minecraft:uniform",
    "value": {
      "max_inclusive": 7,
      "min_inclusive": 0
    }
  },
  "natural": true,
  "piglin_safe": false,
  "respawn_anchor_works": false,
  "ultrawarm": false
}
```

Let's break this down line by line:

* `ambient_light`: Controls the amount of ambient light in the dimension. The minimum is 0 (no ambient light) and the maximum is 1 (super bright everywhere).
* `bed_works`: Determines whether or not beds work. If set to `false`, they will blow up if a player attempts to set their spawn with them.
* `coordinate_scale`: The value in which coordinates are multiplied/divided when entering/leaving the dimension. This is set to `8` for the nether.
* `effects`: Determines the dimension-wide effects. 
	* If set to `minecraft:overworld`, the sky will have clouds, stars, the sun and the moon.
	* If set to `minecraft:nether`, the fog will be thicker than normal.
	* If set to `minecraft:the_end`, the dimension will have the end sky, completely ignoring the biome sky and fog colors.
* `has_ceiling`: *(Research into code needed)*
* `has_raids`: Determines whether or not pillager raids can happen.
* `has_skylight`: Determines whether or not sky light is calculated.
* `height`: The upper build limit of the dimension, starting from the `min_y`. *Must be a multiple of 16!*
* `infiniburn`: A block tag. Fire on the blocks in this block tag will never burn out.
* `logical_height`: The maximum height that chorus fruit will teleport entities and nether portals can be generated. *Must be a multiple of 16, and cannot be greater than `height`!*
* `min_y`: The lower build limit of the dimension. *Must be a multiple of 16!*
* `monster_spawn_block_light_limit`: The maximum block light level where mobs can spawn. *Must be an integer between 0 and 15 (inclusive)!*
* `monster_spawn_light_level`: The range of light levels where mobs can spawn, taking into account sky light. *Must be an integer provider between 0 and 15 (inclusive)!*
* `natural`: If set to true:
    * Compasses point towards the world spawn.
    * Nether Portals spawn Zombified Piglins.
* `piglin_safe`: Determines whether or not Piglins and Hoglins will automatically be converted into their Zombified variants.
* `respawn_anchor_works`: Determines whether or not respawn anchors work. If set to `false`, they will blow up if a player attempts to set their spawn with them.
* `ultrawarm`: If set to true:
    * Water evaporates when placed.
    * Sponges are automatically dried.
    * Lava flows faster and can cover a larger. area
