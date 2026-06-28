(tag-chem-hydrogen)=
# Hydrogen

Tag: `Hydrogen`

Includes: [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac)

Tag-Description: Particles with hydrogen-dominant chemistry.

Subgroups: `Hydrogen`

Subgroup-Description: Hydrogen chemical quantities

Neutral Hydrogen (`HI`) and related species quanties (H$^+$=`HII`, E$^-$, H$_2$) are specified via the appropriate subgroups, the letter `H` or `E`, and the appropriate modifier. 
They may **optionally** additionally be referenced by the full name via hard link:

::::{tab-set}
:::{tab-item} Number Density
:sync: number

Groups: `NumberDensities/Hydrogen`

| Name | Full Name       | Description                                 |
| ---- | --------------- | ------------------------------------------- |
| H    | Hydrogen        | Number density of Neutral Hydrogen (`HI`)   |
| Hp   | Proton[^proton] | Number density of Protons (`HII`)           |
| E    | Electron        | Number density of Electrons                 |
| H2   |                 | Number density of Molecular Hydrogen (`H2`) |

:::
:::{tab-item} Mass Density
:sync: mass

Groups: `MassDensities/Hydrogen`

| Name | Full Name       | Description                               |
| ---- | --------------- | ----------------------------------------- |
| H    | Hydrogen        | Mass density of Neutral Hydrogen (`HI`)   |
| Hp   | Proton[^proton] | Mass density of Protons (`HII`)           |
| E    | Electron        | Mass density of Electrons                 |
| H2   |                 | Mass density of Molecular Hydrogen (`H2`) |

:::
:::{tab-item} Abundance
:sync: abundance

Groups: `Abundances/Hydrogen`

| Name | Full Name       | Description                         |
| ---- | --------------- | ----------------------------------- |
| H    | Hydrogen        | Neutral Hydrogen (`HI`) abundance   |
| Hp   | Proton[^proton] | Proton (`HII`) abundance            |
| E    | Electron        | Electron abundance                  |
| H2   |                 | Molecular Hydrogen (`H2`) abundance |


:::
:::{tab-item} Mass Fraction
:sync: mass-frac

Groups: `MassFractions/Hydrogen`

| Name | Full Name       | Description                             |
| ---- | --------------- | --------------------------------------- |
| H    | Hydrogen        | Neutral Hydrogen (`HI`) mass-fraction   |
| Hp   | Proton[^proton] | Proton (`HII`) mass-fraction            |
| E    | Electron        | Electron mass-fraction                  |
| H2   |                 | Molecular Hydrogen (`H2`) mass-fraction |
:::
::::

[^proton]: We chose proton rather than something like `HI` or `HydrogenI` for extra clarity.
