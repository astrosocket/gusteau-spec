(tag-chemistry)=
# Chemistry

Includes:  [`Massive`](#tag-massive)[^mass-frac], [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac)

Particles with an internal state that represents some form of "chemistry".
For consistancy, tags in the chemistry group **must pick at least one** of [`Abundance`](#tag-chem-abundance), [`MassDensity`](#tag-chem-mass) [`MassFraction`](#tag-chem-mass-frac), or [`NumberDensity`](#tag-chem-number) to represent chemical quantities for inclusion.

Thus an example tag set could be `["Abundance", "Hydrogen", "Metallic"]` to represent [abundance-based](#tag-chem-abundance), [metallic](#tag-chem-metallic) hydrogen chemistry.

The chemical quantities will then be listed under the corresponding subgroups, listed here for convenience:

* `Abundances`
* `MassFraction`
* `NumberDensity`
* `MassDensity`

Continuing the above example would define the following fields:
```
/.../Abundances/Hydrogen/H
/.../Abundances/Hydrogen/E
/.../Abundances/Hydrogen/Hp
/.../Abundances/Hydrogen/H2
/.../Abundances/Metals/XXX1
/.../Abundances/Metals/XXX2
/.../Abundances/Metals/...
/.../Abundances/Metals/TotalAbundances
/.../Abundances/Metals.MetalOnlyDenominator
```
where `XXX1` and `XXX2` are example tracked "metals".

Note, however, that since more than one of `Abundance`/etc. can be selected, chemical quantities can be split across subgroups without repeating analogous fields.
For example,
```
/.../Abundances/Hydrogen/H
/.../Abundances/Hydrogen/E
/.../MassFractions/Hydrogen/Hp
/.../MassFractions/Hydrogen/H2
```
is a valid implementation of `Abundance`, `MassFraction`, `Hydrogen`.

## Chemistry specific tags:

The following are chemistry specific tags:

:::{toc}
:context: children
:::

[^mass-frac]: Only included if [`MassFraction`](#tag-chem-mass-frac) or [`MassDensity`](#tag-chem-mass) is included.
