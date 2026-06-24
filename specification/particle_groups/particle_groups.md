(particle-groups)=
# Particle Groups

## Description

Datasets for different particle types are stored in groups with descriptive names, e.g. BaryonicGas, LowResDarkMatter, BulgeStars, SMBHs.
The required fields for a type of particle are defined hierarchically and are intended to be composable, specified by tags.
For example, all particle groups must contain the fields in the `Particle` type (e.g. `Coordinates`, `Velocities`), while the `BulgeStars` group, tagged with `SPH`, `SubgridParticles`, and `Metallic`, would be required to include the union of additional fields in those categories.  
Note that `Metallic`, for example, also brings in the `Hydrogenic`, `Massive`, and `Mass-frac` tags[^chem].

[^chem]: The `Mass-frac` tag is "optional". See [](#tag-chemistry) for more information.

Multiple field names can refer to the same underlying dataset through the use of hard or soft links, e.g. `Density` could be a hard link to `SPH_Smoothed_Density`. 

Also, these categories and fields are the minimum required, and are not restrictive.
Effectively, by tagging a particle group with a certain particle type, you are *guaranteeing* the presence of the corresponding datasets _with the specified definitions_.

However, you can certainly include additional fields without the appropriate flag (assuming it exists).

:::{admonition}
:class: error
Including a field from a tag with a *different* definition than what is specified (e.g. storing the electron _mass fraction_ as `ElectronAbundance`, see [](#tag-chemistry)) is a **violation** of the specification[^unclear].
:::

All particle groups must fulfill [`Particles`](#tag-particles) at a minimum.

[^unclear]: If you believe a particular field definition is incorrect/unclear, you're more than welcome to raise an [issue](https://github.com/astrosocket/gusteau-spec/issues/new/choose)!

::::{admonition} Is it _really_ a particle?
:class: tip
:class: dropdown
Short answer? Yes!

Long Answer: In our framework, a _particle group_ is a group of datasets matching the [`Particles`](#tag-particles) tag and a _particle_ is the object described by the corresponding rows across the datasets. 
However, the [`Particles`](#tag-particles) group is very simple, and only contains an ID dataset, a positional dataset, and a velocity dataset.
So as long as your collection of objects is **identifiable**, has a defined **set of [$D$](#header-dimension) coordinates** and **$D$ velocities**, it's a particle for these purposes.  
That means objects like Voronoi cells or Gizmo's finite volume elements (aka `gas`) are considered particles in this framework. 

:::{admonition} 🤓 "Well technically..."
:class: hint
:icon: false
:class: dropdown
Actually your object just needs to be positionable in $D+D+1$ space, arbitrarily defining one set of $D$ values as `Coordinates`, the other as `Velocities` and the final as the `ID`.
But that's basically what a particle is anyway.
:::
::::

(particle-groups-attributes)=
### Attributes

(particle-groups-attributes-req)=
#### Required Attributes

| Name           | Type     | Description                                                                                                                                                                                                    |
| -------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aliases        | string[] | List of aliases (links) to this Group. E.g. ["gas", "PartType0"]                                                                                                                                               |
| Tags           | string[] | List of particle type tags filled by this Group. An empty list is assumed to only match [`Particle`](#tag-particles).  Tags are case-insensitive: "Massive" is the same as "massive" is the same as "mAsSiVe". |
| NumberOfFields | int      | Number of Datasets contained in this group                                                                                                                                                                     |


(particle-groups-attributes-opt)=
#### Optional Attributes

| Name              | Type | Description                                                                                     |
| ----------------- | ---- | ----------------------------------------------------------------------------------------------- |
| NumberOfParticles | long | Number of particles (elements/length of first dimension) of each dataset. Must be equal to $N$. |

(particle-groups-datasets)=
### Datasets

Datasets can be one of two types:
1. 1D arrays of length $N$
2. 2D matrices of shape $N$x$M$, where the quantity $M$ is an arbitrary positive integer.

Note that matrices are intended to represent vector/tensor quantities with a well-defined (generally related to $D$) size that does not vary between different _types_ of simulations,  _versions_ of simulation code, _sub-grid physics_, or similar.  
If such is a possibility (chemical abundances, for example), consider using [Subgroups](#particle-groups-subgroups) of 1D arrays instead.
In light of this, datasets types are assumed to be `number[`$N$`]`, unless explicitly stated otherwise.

Since all datasets represent $N$ quantities of something, names should be plural by default, i.e. `InternalEnergies` instead of `InternalEnergy`.
This does not apply if the main term of the name is the symbolic name (e.g. the Greek symbol).
For example, `Mdot_Bondi` should not need be converted to `Mdot_Bondis`, though  `BondiAccretionRates` may be clearer.

 Every dataset must have the following attributes, which describe the dataset, including units and transformation:

| Name                        | Type   | Description                                                                             | Link                                |
| --------------------------- | ------ | --------------------------------------------------------------------------------------- | ----------------------------------- |
| Units                       | string | Dataset units                                                                           | [](#pg-units)                       |
| ConversionFactorCGS         | double | Conversion factor to CGS units, not including cosmological corrections                  | [](#pg-conversionfactorcgs)         |
| ConversionFactor_PhysCGS    | double | Conversion factor to CGS units, including cosmological corrections                      | [](#pg-conversionfactor_physcgs)    |
| Description                 | string | Description of the dataset                                                              | [](#pg-description)                 |
| Expression_for_physical_CGS | string | The condensed expression for converting the dataset units into physical CGS units       | [](#pg-expression_for_physical_cgs) |
| LossyCompression            | string | Filter used for lossy compression. If no filter is applied, use the empty string, `""`. | [](#pg-lossycompression)            |
| U_I_exponent                | float  | Power of the [current unit](#unit-table)                                                |                                     |
| U_L_exponent                | float  | Power of the [length unit](#unit-table)                                                 |                                     |
| U_M_exponent                | float  | Power of the [mass unit](#unit-table)                                                   |                                     |
| U_T_exponent                | float  | Power of the [temperature unit](#unit-table)                                            |                                     |
| U_t_exponent                | float  | Power of the [time unit](#unit-table)                                                   |                                     |
| a_scale_exponent            | float  | Power of the [scale-factor](#cosmo-scale-factor)                                        |                                     |
| h_scale_exponent            | float  | Power of the [reduced Hubble constant ($h$)](#cosmo-littleh)                            |                                     |

(pg-units)=
#### Units

Dataset units, e.g. `"cm"` or `"furlongs/fortnight/M_moon"`.

(pg-conversionfactorcgs)=
#### ConversionFactorCGS

Numerical factor to convert from the [dataset units](#pg-units) to cosmological CGS (like `cm/h`).
Final numerical result of the quantity $U_I^{\text{U\_I\_Exponent}} \times U_L^{\text{U\_L\_Exponent}} \times U_M^{\text{U\_M\_Exponent}} \times U_T^{\text{U\_T\_Exponent}}\times U_t^{\text{U\_t\_Exponent}}$ where $U_{x}$ are from [`/Units`](#unit-table).

(pg-conversionfactor_physcgs)=
#### ConversionFactor_PhysCGS

Numerical factor to convert from the [dataset units](#pg-units) to physical CGS (like `cm`).
Final numerical result of the quantity $a^{\text{a\_scale\_exponent}} \times h^{\text{h\_scale\_exponent}} \times U_I^{\text{U\_I\_Exponent}} \times U_L^{\text{U\_L\_Exponent}} \times U_M^{\text{U\_M\_Exponent}} \times U_T^{\text{U\_T\_Exponent}}\times U_t^{\text{U\_t\_Exponent}}$ where $U_{x}$ are from [`/Units`](#unit-table).


(pg-description)=
#### Description

Plain description of the quantities in this dataset. For datasets listed in one of the [](#particle-groups-tags), should match or expand the description in the tag.

(pg-expression_for_physical_cgs)=
#### Expression_for_physical_CGS

String expression version of [](#pg-conversionfactor_physcgs).
Only unit and cosmological factors with non-zero exponents should be included.
For example, comoving density might be `"a^-3 U_M U_L^-3 [g cm^-3]"`.

(pg-lossycompression)=
#### LossyCompression

Name of a lossy compression filter that was applied to this dataset.
Leave empty if no filter was applied.

(particle-groups-subgroups)=                           
### Subgroups 

Subgroups form a collection of related datasets inside a Particle Group. Generally, they are used to organize datasets that may have the same units, or represent similar quantities. Prominent examples include chemical abundances or black hole merger statistics.

Subgroups have no required attributes or datasets.


(tag-particles)=
## The `Particles` Tag

The base particle type. Has an id, position, velocity, and nothing else.

| Name | 2nd Dimension | Description |
| ----------- | ------------- | -------------------------------------------------- |
| ParticleIDs | | Particle ID number |
| Coordinates | $D$ | The $D$-D coordinates of the particle |
| Velocities | $D$ | The $D$-D peculiar velocity vector of the particle |

(particle-groups-tags)=
## Other Particle tags

The current list of known particle tags is

:::{toc}
:context: children
:::

