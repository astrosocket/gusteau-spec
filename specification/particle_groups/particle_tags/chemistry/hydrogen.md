(tag-chem-hydrogenic)=
# Hydrogenic 

Tag: `Hydrogenic`

Includes: [](#tag-chem-number)|[](#tag-chem-mass)|[](#tag-chem-abundance) |[](#tag-chem-mass-frac)

Particles with hydrogen-dominant chemistry.
Neutral Hydrogen (`HI`) and related species abundances (H$^+$=`HII`, E$^-$, H$_2$) are specified via the appropriate prefix, the letter `H` or `E`, and the appropriate modifier. 
They may **optionally** additionally be referenced by the full name:

::::{tab-set}
:::{tab-item} Number Density
:sync: number

| Name | Full Name             | Description                                 |
| ---- | --------------------- | ------------------------------------------- |
| N_H  | HydrogenNumberDensity | Number density of Neutral Hydrogen (`HI`)   |
| N_Hp | ProtonNumberDensity[^proton]   | Number density of Ionized Hydrogen (`HII`)  |
| N_E  | ElectronNumberDensity | Number density of Electrons                 |
| N_H2 | H2NumberDensity       | Number density of Molecular Hydrogen (`H2`) |

:::
:::{tab-item} Mass Density
:sync: mass

| Name   | Full Name       | Description                               |
| ------ | --------------- | ----------------------------------------- |
| Rho_H  | HydrogenDensity | Mass density of Neutral Hydrogen (`HI`)   |
| Rho_Hp | ProtonDensity[^proton]   | Mass density of Ionized Hydrogen (`HII`)  |
| Rho_E  | ElectronDensity | Mass density of Electrons                 |
| Rho_H2 | H2Density       | Mass density of Molecular Hydrogen (`H2`) |

:::
:::{tab-item} Abundance
:sync: abundance

| Name | Full Name         | Description                         |
| ---- | ----------------- | ----------------------------------- |
| A_H  | HydrogenAbundance | Neutral Hydrogen (`HI`) abundance   |
| A_Hp | ProtonAbundance[^proton]   | Ionized Hydrogen (`HII`) abundance  |
| A_E  | ElectronAbundance | Electron abundance                  |
| A_H2 | H2Abundance       | Molecular Hydrogen (`H2`) abundance |


:::
:::{tab-item} Mass Fraction
:sync: mass-frac

| Name | Full Name            | Description                             |
| ---- | -------------------- | --------------------------------------- |
| X_H  | HydrogenMassFraction | Neutral Hydrogen (`HI`) mass-fraction   |
| X_Hp | ProtonMassFraction[^proton]   | Ionized Hydrogen (`HII`) mass-fraction  |
| X_E  | ElectronMassFraction | Electron mass-fraction                  |
| X_H2 | H2MassFraction       | Molecular Hydrogen (`H2`) mass-fraction |
:::
::::

[^proton]: We chose proton rather than something like `HI` or `HydrogenI` for clarity.