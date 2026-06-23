---
short_title: Subfind
---
(tag-subfind)=
# Particles with SubFind information

Tag: `Subfind`

Includes: [](#tag-massive)

Particles with SubFind information attached.

Particles with this tag **must** include the subgroup `Subfind` with the following datasets. 
Datasets may **optionally** be linked with datasets at the main group level that are prefixed with `Subfind` (i.e. `SubfindDMDensity` links to `Subfind/DMDensity`.

## Attributes

The `Subfind` subgroup must have the following attributes:

| Name              | Type                 | Description                                                                                                                                           |
| ----------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| NumNearest        | number               | The threshold of nearest particles used                                                                                                               |
| DarkMatterSpecies | number[] or string[] | List of particle types considered as DarkMatter in the same format as [`/Header.ParticleNames`](#header-ParticleNames) or as indices into that array. |

## Datasets

In the following, "Dark Matter" refers to the particle types listed in the `DarkMatterSpecies` attribute.

| Name                        | Description                                                                                                                                    |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Subfind/DMDensities         | Local total mass density, estimated using the standard cubic-spline SPH kernel over all "Dark Matter" particles with a radius of `SubfindHsml` |
| Subfind/Densities           | Local total mass density, estimated using the standard cubic-spline SPH kernel over all particles within a radius of `SubfindHsml`             |
| Subfind/Hsml                | The radius of the sphere centered on this particle enclosing the `NumNearest` "Dark Matter" particles.                                         |
| Subfind/VelocityDispersions | The $D$D velocity dispersion of all "Dark Matter" particles within a radius of `SubfindHsml`                                                   |
