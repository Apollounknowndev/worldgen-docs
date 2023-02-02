---
layout: page
title: Vertical Anchors
permalink: /docs/misc/vertical-anchors/
parent: Miscellaneous
grand_parent: Documentation
---

# Vertical Anchors

Vertical anchors are used to provide the elevation for some configured feature types and placement modifiers. There's three vertical anchors: one absolute, and two relative. All of these take integer providers.

## `absolute` 

An absolute height, as used in commands or coordinates.

## `above_bottom`

The height relative to the minimum build height of the dimension. An `above_bottom` value of 10 in a dimension with a minimum build height of -64 would be -54 in coordinates.

## `below_top`

The height relative to the maximum build height of the dimension. A `below_top` value of 10 in a dimension with a maximum build height of 320 would be 310 in coordinates.