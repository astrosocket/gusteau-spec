---
short_title: Transform
---
(tag-transform)=
# Transformed Particles

Tag: `Transform`

Includes: [`Particles`](#tag-particles)

Tag-Description: Particles that transition between particle types.

Subgroups: `FromParent_X`

Subgroup-Description: Quantities carried over from previous particle type

Examples include gas collapsing into star or other sink particle, stars moving along the stellar evolution track, compact object formation.

For the purpose here, it does not matter how or why the particle transformed.

:::{admonition} Subgroup names
:class: note
The `X` in `FromParent_X` should match exactly one of the names in [](#header-particle_names) and represents the species of the originating particle.

If this particle type can be formed from multiple different species, multiple subgroups should be included, eg. `FromParent_gas`, `FromParent_stars` would allow both direct-collapse black holes and ordinary stellar black holes.
:::

## Datasets:

| Name                  | Description                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------ |
| TransformTimes        | Time of the most recent particle type transformation.                                      |
| TransformScaleFactors | Scale-factor of the most recent particle type transformation.                              |
| PreviousParticleTypes | Previous particle type as an index into [`/Header.Particle_names`](#header-particle_names) |

At least one of `TransformTimes` and `TransformScaleFactors` is **required**. If having both options is unfeasible, `TransformTimes` is the preferred option[^time_preference].  `PreviousParticleTypes` is **required**.

[^time_preference]: `TransformTimes` is preferred because it is the variable that is more likely to be available. `TransformScaleFactors` only makes sense in cosmological simulations

(transform-fromparent_x)=
## Subgroup - `FromParent_X`

The `FromParent` subgroup should contain any of the fields that were retained from the previous particle type(s) that are no longer actively updated, organized by type.

As an example, gas particles that have undergone splitting may have a `SplitCounts` field.
If that particle transforms into a star and retains the field, further updates to that field are nonsensical; however it may be retained for various purposes, like identifying the originating gas particle.
It would be a good candidate for moving to the `FromParent_gas` subgroup.

Note that entire subgroups can be retained in this manner and we recommend retaining any group hierarchy, just under the `FromParent_${ParticleType}/` subgroup instead of the top-level group. 

Likewise, relevant tags can be moved to the `FromParent_${ParticleType}` group instead of remaining at the top-level.
