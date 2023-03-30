---
layout: page
title: Random Selector
permalink: /docs/configured-features/feature-types/random-selector/
parent: Configured Features
grand_parent: Documentation
nav_order: 45
---

## Random Selector

<head>
    {% include field-type-colors.html %}
</head>

The `minecraft:random_selector` feature type is used to randomly select betwen a list of placed features. In vanilla, it is used in many places where the feature to get placed at a certain position should be randomized. This includes things like types of trees to place in a Forest biome.

### Json format

<pre>
{
   "type": "minecraft:random_selector",
   "config": {
      "features": [
         {
            "chance": 0.5,
            "feature": "foo:feature_a"
         },
         {
            "chance": 0.2,
            "feature": "foo:feature_b"
         }
      ],
      "default": "foo:bar/feature_c"
   }
}
</pre>

* ‌<re>[L]</re> `features`: The list of features to use.
    * ‌<ye>[F]</ye> `chance`: The chance for this feature to be placed, as a float between 0.0 and 1.0.
    * `feature`: The placed feature to be used if this entry is selected.
* `default`: The default placed feature to use if none of the features in `features` are selected.

### Additional Info
The way `random_selector` works is that it goes down the list of features and the first entry where a random float between 0.0 and 1.0 is less than the provided `chance` is selected to be placed. So in the example as seen in the JSON format section:
* `foo:feature_a` has a 50% chance of being placed.
* `foo:feature_b` has a 20% chance of being placed if `foo:feature_a` isn't placed (which is a 50% chance), so the actual chance of this feature being placed is 10%.
* `foo:feature_c` is placed if both `foo:feature_a` and `foo:feature_c` fail (a 40% chance), so the chance of this feature being placed is 40%.