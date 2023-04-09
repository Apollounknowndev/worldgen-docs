---
layout: page
title: Introduction
permalink: /docs/worldgen/configured-features/introduction/
parent: Configured Features
grand_parent: Documentation
nav_order: 1
---

# Intro to Configured Features

<head>
    {% include field-type-colors.html %}
</head>

Configured feature files contain configuration information about a feature. 

### What is a feature?

A feature is a "decoration" that gets placed after the world's terrain shaping has been done. Small features like trees, rocks, plants, and ores are all features. Some small structures like dungeons, fossils and desert wells are also features. Features cannot be located with `/locate`; this is why you can't use `/locate` to find dungeons.

Configured features simply define the *configuration* of that feature. Placed features determines how that feature is *placed* in the world. For example, a placed feature may tell the game to place 10 trees per chunk in a forest biome, and the configured feature for that tree tells the game that the tree should generate 4-6 blocks tall and with Oak Logs as the trunk.

Configured features are stored in the `/worldgen/configured_feature` folder.

There are currently 61 configured features types, each with their own configuration. Because of this large amount, each configured feature type has its own page.

## JSON format

Let's take a look at an example configured feature configuration:

<pre>
{
   "type": "minecraft:no_op",
   "config": {}
}
</pre>

There are two fields:

* ‌<pu>[S]</pu> `type`: The ID of the configured feature type. This references a hardcoded configured feature type like `minecraft:tree`, `minecraft:ore`, etc.
* `config`: The configuration of the feature. The properties inside this object depend on the configured feature type being used. In this example, since we're using the `minecraft:no_op` configured feature type, there are no other fields to configure.

The level of customization available in a configured feature can vary significantly depending on the feature type. Some configured feature types like trees and geodes have more than a dozen parameters that can be adjusted and experimented with. However, other features like dungeons and ice spikes do not have any parameters to configure. If you're unsure about what configuration options are available for a particular feature type, you can check the page for the specific configured feature type to learn more.
