(tag-chem-extended)=
# Hydrogen (Extension)

Tag: `ExtendedHydrogen`

Includes: [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac), [](#tag-chem-hydrogen)

Tag-Description: Particles with extended hydrogen chemistry.

Additional hydrogen species can be included in the `Hydrogen` subgroup via this tag.
All species are optional but if present should use the below names.
They may **optionally** additionally be referenced by the full name via hard link:

::::{tab-set}
:::{tab-item} Number Density
:sync: number

Groups: `NumberDensities/Hydrogen`

| Name | Full Name          | Description                                            |
| ---- | ------------------ | ------------------------------------------------------ |
| Hm   | Hydride            | Number density of Hydride (H$^-$)                      |
| D    | Deuterium          | Number density of Deuterium                            |
| Dp   | Deuteron           | Number density of Deuterons (`DI`)                     |
| Dm   | Deuteride          | Number density of Deuteride (D$^-$)                    |
| H2p  |                    | Number density of Ionized Molecular Hydrogen (H$_2^+$) |
| HD   | DeuteratedHydrogen | Number density of Deuterated Hydrogen (`HD`)           |
| HDp  |                    | Number density of Ionized Deuterated Hydrogen (HD$^+$) |
| HDm  |                    | Number density of HD$^-$                               |
| H3p  |                    | Number density of H$_3^+$                              |
| H2Dp |                    | Number density of H$_2$D$^+$                           |

:::
:::{tab-item} Mass Density
:sync: mass

Groups: `MassDensities/Hydrogen`

| Name | Full Name          | Description                                          |
| ---- | ------------------ | ---------------------------------------------------- |
| Hm   | Hydride            | Mass density of Hydride (H$^-$)                      |
| D    | Deuterium          | Mass density of Deuterium                            |
| Dp   | Deuteron           | Mass density of Deuterons (`DI`)                     |
| Dm   | Deuteride          | Mass density of Deuteride (D$^-$)                    |
| H2p  |                    | Mass density of Ionized Molecular Hydrogen (H$_2^+$) |
| HD   | DeuteratedHydrogen | Mass density of Deuterated Hydrogen (`HD`)           |
| HDp  |                    | Mass density of Ionized Deuterated Hydrogen (HD$^+$) |
| HDm  |                    | Mass density of HD$^-$                               |
| H3p  |                    | Mass density of H$_3^+$                              |
| H2Dp |                    | Mass density of H$_2$D$^+$                           |

:::
:::{tab-item} Abundance
:sync: abundance

Groups: `Abundances/Hydrogen`

| Name | Full Name          | Description                                    |
| ---- | ------------------ | ---------------------------------------------- |
| Hm   | Hydride            | Hydride (H$^-$) abundance                      |
| D    | Deuterium          | Deuterium abundance                            |
| Dp   | Deuteron           | Deuterons (`DI`) abundance                     |
| Dm   | Deuteride          | Deuteride (D$^-$) abundance                    |
| H2p  |                    | Ionized Molecular Hydrogen (H$_2^+$) abundance |
| HD   | DeuteratedHydrogen | Deuterated Hydrogen (`HD`) abundance           |
| HDp  |                    | Ionized Deuterated Hydrogen (HD$^+$) abundance |
| HDm  |                    | HD$^-$ abundance                               |
| H3p  |                    | H$_3^+$ abundance                              |
| H2Dp |                    | H$_2$D$^+$ abundance                           |


:::
:::{tab-item} Mass Fraction
:sync: mass-frac

Groups: `MassFractions/Hydrogen`

| Name | Full Name          | Description                                        |
| ---- | ------------------ | -------------------------------------------------- |
| Hm   | Hydride            | Hydride (H$^-$) mass fraction                      |
| D    | Deuterium          | Deuterium mass fraction                            |
| Dp   | Deuteron           | Deuterons (`DI`) mass fraction                     |
| Dm   | Deuteride          | Deuteride (D$^-$) mass fraction                    |
| H2p  |                    | Ionized Molecular Hydrogen (H$_2^+$) mass fraction |
| HD   | DeuteratedHydrogen | Deuterated Hydrogen (`HD`) mass fraction           |
| HDp  |                    | Ionized Deuterated Hydrogen (HD$^+$) mass fraction |
| HDm  |                    | HD$^-$ mass fraction                               |
| H3p  |                    | H$_3^+$ mass fraction                              |
| H2Dp |                    | H$_2$D$^+$ mass fraction                           |
:::
::::