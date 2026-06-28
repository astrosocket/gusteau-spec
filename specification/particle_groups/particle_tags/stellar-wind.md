---
short_title: Stellar Wind
---
(tag-stellarwind)=
# Stellar wind-related Quantities

Tag: `StellarWind`

Includes: [`Particles`](#tag-particles), ([`AGB`](#tag-agb)|[`SNIa`](#tag-snia)|[`SNII`](#tag-snii) on subgroup)

Tag-Description: Particles affected by various feedback events.

Subgroups: `StellarWind`

Subgroup-Description: This subgroup is the primary location to store stellar wind-related subgrid quantities.

Particles with this tag **must** include the subgroup `StellarWind` and specify at least one of [`AGB`](#tag-agb), [`SNIa`](#tag-snia), or [`SNII`](#tag-snii) on the `/../StellarWind.tags` attribute, indicating what sources of stellar wind are present.
The `AGB`/`SNIa`/`SNII` groups will then be subgroups of `StellarWind`.

While the quantities utilized in stellar wind-subgrid physics can vary significantly, especially between different sources, **example** datasets are described below. 
None of them are required, but should use the specified name (and naming patterns) if present.

:::{admonition}
:class: attention
If a quantity is shared by multiple wind types, it should be included at the `StellarWind` level.
Otherwise, quantities should be placed under their respective sub-subgroups.
:::

:::{admonition} Other stellar wind models
:class: dropdown
:class: hint
If the snapshot includes a wind source besides the above-mentioned models, include it using the same patterns:
 1. Add a subgroup to `StellarWind` with a descriptive name (e.g. `RedGiant`) and `Description` attribute ("Sourced from red giant stars")
 2. Add a tag with the same name (`RedGiant`) to the `StellarWind` subgroup.
 3. Add appropriate fields (`/../StellarWind/RedGiant/Masses`)
 4. Add it to the specification by submitting an [issue](https://github.com/astrosocket/gusteau-spec/issues/new/choose).
:::

## Example Datasets

| Name                     | Description                                                                  |
| ------------------------ | ---------------------------------------------------------------------------- |
| AGB/Masses               | Masses of gas that have been produced by AGB stars                           |
| SNIa/Metal_mass_fraction | Fractions of the particles' masses that are in metals produced by SNIa stars |


