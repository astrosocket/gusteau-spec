(tag-chem-helium)=
# Helium

Tag: `Helium`

Includes: [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac)

Tag-Description: Particles with helium chemistry.

Subgroups: `Helium`

Subgroup-Description: Helium chemistry quantities

Neutral Helium (`HeI`) and related species quanties (He$^+$=`HeII`, He$^{++}$=`HeIII`) are specified via the appropriate subgroups, the letters `He`, and the appropriate modifier. 
They may **optionally** additionally be referenced by the full name via hard link:

Only the Neutral Helium dataset is **required**.

::::{tab-set}
:::{tab-item} Number Density
:sync: number

Groups: `NumberDensities/Helium`

| Name | Full Name | Description                                       |
| ---- | --------- | ------------------------------------------------- |
| He   | Helium    | Number density of Neutral Helium (`HeI`)          |
| Hep  |           | Number density of Ionized Helium (`HeII`)         |
| Hepp |           | Number density of Doubly Ionized Helium (`HeIII`) |

:::
:::{tab-item} Mass Density
:sync: mass

Groups: `MassDensities/Helium`

| Name | Full Name | Description                                     |
| ---- | --------- | ----------------------------------------------- |
| He   | Helium    | Mass density of Neutral Helium (`HeI`)         |
| Hep  |           | Mass density of Ionized Helium (`HeII`)         |
| Hepp |           | Mass density of Doubly Ionized Helium (`HeIII`) |

:::
:::{tab-item} Abundance
:sync: abundance

Groups: `Abundances/Helium`

| Name | Full Name | Description                               |
| ---- | --------- | ----------------------------------------- |
| He   | Helium    | Neutral Helium (`HeI`) abundance         |
| Hep  |           | Ionized Helium (`HeII`) abundance         |
| Hepp |           | Doubly Ionized Helium (`HeIII`) abundance |


:::
:::{tab-item} Mass Fraction
:sync: mass-frac

Groups: `MassFractions/Helium`

| Name | Full Name | Description                                   |
| ---- | --------- | --------------------------------------------- |
| He   | Helium    | Neutral Helium (`HeI`) mass fraction         |
| Hep  |           | Ionized Helium (`HeII`) mass fraction         |
| Hepp |           | Doubly Ionized Helium (`HeIII`) mass fraction |
:::
::::