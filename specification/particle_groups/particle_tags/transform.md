---
short_title: Transform
---
(tag-transform)=
# Transformed Particles

Tag: `Transform`

Includes: [`Particles`](#tag-particles)

Tag-Description: Particles that transition between particle types.

Subgroups: `CarriedOver`

Subgroup-Description: Quantities carried over from previous particle type

Examples include gas collapsing into star or other sink particle, stars moving along the stellar evolution track, compact object formation.

For the purpose here, it does not matter how or why the particle transformed.

## Datasets:

| Name                  | Description                                                                              |
| --------------------- | ---------------------------------------------------------------------------------------- |
| TransformTimes        | Time of the most recent particle type transformation.                                    |
| TransformScaleFactors | Scale-factor of the most recent particle type transformation.                            |
| PreviousParticleTypes | Previous particle type as an index into [`/Header.ParticleNames`](#header-particlenames) |

## Subgroup - `CarriedOver`

The `CarriedOver` subgroup should contain any of the fields that were retained from the previous particle type(s) that are no longer actively updated, organized by type.

As an example, gas particles that have undergone splitting may have a `SplitCounts` field.
If that particle transforms into a star and retains the field, further updates to that field are nonsensical; however it may be retained for various purposes, like identifying the originating gas particle.
It would be a good candidate for moving to the `CarriedOver/gas` subgroup.

Note that entire subgroups can be retained in this manner and we recommend retaining any group hierarchy, just under the `CarriedOver/${ParticleType}/` subgroup instead of the top-level group. 

Likewise, relevant tags can be moved to the `CarriedOver/${ParticleType}` group instead of remaining at the top-level.
