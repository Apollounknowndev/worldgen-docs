---
layout: page
title: Configured Features
permalink: /docs/worldgen/configured-features/
parent: Worldgen
grand_parent: Documentation
---

<style>
re {color:#FF6F6F;font-weight:bold}
or {color:#FEC856;font-weight:bold}
ye {color:#FBFF55;font-weight:bold}
gr {color:#00E61D;font-weight:bold}
bl {color:#5573FF;font-weight:bold}
pu {color:#CE52FE;font-weight:bold}
</style>

# Configured Features

Configured feature files contain configuration information about a feature. 

### What is a feature?

A feature is a "decoration" that gets placed after the world's terrain shaping has been done. Small features like trees, rocks, plants, and ores are all features. Some small structures like dungeons, fossils and desert wells are also features. Features cannot be located with `/locate`; this is why you can't use `/locate` to find dungeons.

Keep in mind that configured features don't actually decide anything about where the feature is placed; placed features handle that. Placed features decide where configured features are placed.

They are stored in the `/worldgen/configured_feature` folder.

As of 1.19, there are 61 configured features types, each with their own configuration. Because of this large amount, each configured feature type has its own page.

## JSON format

Let's take a look at an example configured feature configuration:
```json
{
   "type": "minecraft:no_op",
   "config": {}
}
```

There are two fields:

* ‌<pu>[S]</pu> `type`: The ID of the configured feature type. This references a hardcoded configured feature type like `minecraft:tree`, `minecraft:ore`, etc.
* `config`: The configuration of the feature. The properties inside this object depend on the configured feature type being used. In this example, since we're using the `minecraft:no_op` configured feature type, there are no other fields to configure.

The amount of things you can configure in a configured feature significantly differs based on the feature; some feature types like trees and geodes have well over a dozen values for you to tweak and play around with. Other feature types like dungeons and ice spikes have no values for you to configure. If you want to know what there is to configure for a configured feature type, check the page for it.