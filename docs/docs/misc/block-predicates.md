---
layout: page
title: Block Predicates
permalink: /docs/misc/block-predicates/
parent: Miscellaneous
grand_parent: Documentation
---

# Block Predicates

Block predicates are used to check the properties of blocks relative to the current position. They're used in some configured feature types and placement modifiers.

The configuration for a block predicate is as follows:

* `type`: The block predicate type to check.
    * If set to `minecraft:all_of`:
        * `predicates`: A list of block predicates. All predicates in the list must pass for this predicate to pass.
    * If set to `minecraft:any_of`:
        * `predicates`: A list of block predicates. At least one predicate in the list must pass for this predicate to pass.
    * If set to `minecraft:has_sturdy_face`:
        * `direction`: A direction. Can be `up`, `down`, `north`, `south`, `east`, or `west`. The block being checked must have a sturdy face in the given direction for the predicate to pass.
        * `offset`: (optional) A list of 3 integers that define the offset from the original position where the predicate gets checked. An `offset` of [0,1,0] means the block above the original position will be checked. Defaults to \[0,0,0\].
    * If set to `minecraft:inside_world_bounds`:
        * `offset`: See `minecraft:has_sturdy_face` for explanation.
        The predicate checks for if the block at the given position is within the height limit.
    * If set to `minecraft:matching_block_tag`:
        * `offset`: See `minecraft:has_sturdy_face` for explanation.
        * `tag`: The block tag that the block at the given position must match. 
    * If set to `minecraft:matching_blocks`:
        * `offset`: See `minecraft:has_sturdy_face` for explanation.
        * `blocks`: The block ID, list of block IDs or block tag that the block at the given position must match. 
    * If set to `minecraft:matching_fluids`:
        * `offset`: See `minecraft:has_sturdy_face` for explanation.
        * `fluids`: Identical to the `blocks` field in `minecraft:matching_blocks`, but fluids instead of blocks.
    * If set to `minecraft:not`:
        * `predicates`: A block predicate. The provided block predicate must fail for this predicate to pass.
    * If set to `minecraft:replaceable`, there are no further fields. This predicate passes if the block at the given position is air, liquid or a plant. 
    * If set to `minecraft:solid`, there are no further fields. This predicate passes if the block at the given position is solid. 
    * If set to `minecraft:true`, there are no further fields. This predicate always passes.
    * If set to `minecraft:would_survive`:
        * `offset`: See `minecraft:has_sturdy_face` for explanation.
        * `state`: The block state to check. The predicate passes if the block provided at the offset position would survive. Used in vanilla to prevent trees stacking on top of each other.