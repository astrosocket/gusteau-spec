(tag-chem-metallic)=
# Metallic

Tag: `Metallic`

Includes: [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac), [](#tag-chem-hydrogen), [](#tag-chem-helium)

Tag-Description: Particles with metal chemistry

Subgroups: `Metals`

Subgroup-Description: Metallic chemistry quantities

Particles whose chemistry includes metallic or molecular elements that are not already included in the `Hydrogen`, `ExtendedHydrogen`, or `Helium` tags.

Particle groups with this tag **must** include the subgroup `Metals`.
Chemical abundances are then datasets under the `Metals` subgroup defined using their [IUPAC symbol](https://iupac.org/what-we-do/periodic-table-of-elements/)([](doi:10.1515/pac-2019-0603)), possibly including ionization states with the appropriate suffix.

Ionization states are specified via the lower-case letters `p` and `m` after the appropriate element with an underscore. 
So Ne$^{++}$ would be `Ne_pp`, LiH$^+$ would be `LiH_p` and F$^{-}$ would be `F_m`.

Molecules are specified with subscripts listed in line, e.g. $\text{C}_{10}H_8$ becoming `C10H8`.

## Denominator terms

Depending on the chemical abundance tag, the `Metals` subgroup will have an additional **required** attribute:

| Name                 | Type    | Description                                                                                                                                                        | Required For         |
| -------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| MetalOnlyDenominator | boolean | Flag specifying whether the summation term in the denominator of the chemical abundance definition only includes metals (`True`) or also includes other chemicals. | Abundance, Mass-Frac |

and *recommended* dataset:

| Name                    | Description                                                                                                                                                                           | Required For |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| Metals/TotalAbundance | Total abundance term. Includes non-metallic species if `MetalOnlyDenominator` is `False`. Equivalent to $\sum_j n_j$ in the [abundance definition](#eq:abundance-def).                | Abundance    |
| Metals/TotalMass      | Total mass term. Includes Hydrogen species if `MetalOnlyDenominator` is `False`. Equivalent to $\sum_j m_j n_j$  in the [mass-fraction definition](#eq:massfrac-def) or $x_0$, above. | Mass-Frac    |

## Example

Following the above rules, the elements in the classic eleven element metallicity array (e.g. in Gadget-2 or Gizmo), defined as 
```
n=0: "total" metal mass (everything not H, He)  <-- x_0
n=1: He  
n=2: C  
n=3: N  
n=4: O  
n=5: Ne  
n=6: Mg  
n=7: Si  
n=8: S  
n=9: Ca  
n=10: Fe 
```

would be represented as 

::::{tab-set}
:::{tab-item} Number Density
:sync: number

Groups: `NumberDensities/`

| Name      | Description                       |
| --------- | --------------------------------- |
| Helium/He | Number density of Helium atoms    |
| Metals/C  | Number density of Carbon atoms    |
| Metals/N  | Number density of Nitrogen atoms  |
| Metals/O  | Number density of Oxygen atoms    |
| Metals/Ne | Number density of Neon atoms      |
| Metals/Mg | Number density of Magnesium atoms |
| Metals/Si | Number density of Silicon atoms   |
| Metals/S  | Number density of Sulfur atoms    |
| Metals/Ca | Number density of Calcium atoms   |
| Metals/Fe | Number density of Iron atoms      |

Note that since the original array was the mass-fractions, these values would need to be transformed via $n_i = x_i x_0/m_i$.
:::
:::{tab-item} Mass Density
:sync: mass

Groups: `MassDensities/`

| Name      | Description                       |
| --------- | --------------------------------- |
| Helium/He | Mass density of Helium atoms    |
| Metals/C  | Mass density of Carbon atoms    |
| Metals/N  | Mass density of Nitrogen atoms  |
| Metals/O  | Mass density of Oxygen atoms    |
| Metals/Ne | Mass density of Neon atoms      |
| Metals/Mg | Mass density of Magnesium atoms |
| Metals/Si | Mass density of Silicon atoms   |
| Metals/S  | Mass density of Sulfur atoms    |
| Metals/Ca | Mass density of Calcium atoms   |
| Metals/Fe | Mass density of Iron atoms      |

Note that since the original array was the mass-fractions, these values would need to be transformed via $\rho_i=x_i x_0$.
:::
:::{tab-item} Abundance
:sync: abundance

Groups: `Abundances/`

| Name                  | Description                                      |
| --------------------- | ------------------------------------------------ |
| Helium/He             | Helium abundance                                 |
| Metals/C              | Carbon abundance                                 |
| Metals/N              | Nitrogen abundance                               |
| Metals/O              | Oxygen abundance                                 |
| Metals/Ne             | Neon abundance                                   |
| Metals/Mg             | Magnesium abundance                              |
| Metals/Si             | Silicon abundance                                |
| Metals/S              | Sulfur abundance                                 |
| Metals/Ca             | Calcium abundance                                |
| Metals/Fe             | Iron abundance                                   |
| Metals/TotalAbundance | Total abundance term. Does not include Hydrogen. |

With the  `/.../Metals.MetalOnlyDenominator` attribute set to `False`.

Note that since the original array was the mass-fractions, these values would need to be transformed in a 2-step process:
$$
\begin{aligned}
n_{i} & = \frac{x_{i} x_0}{m_i} \\
a_i & = \frac{n_i}{\sum_j n_j}
\end{aligned}
$$

`TotalAbundance` is given by $\sum_j n_j$.

:::
:::{tab-item} Mass Fraction
:sync: mass-frac

Groups: `MassFraction/`

| Name             | Description                                |
| ---------------- | ------------------------------------------ |
| Helium/He        | Helium mass-fraction                       |
| Metals/C         | Carbon mass-fraction                       |
| Metals/N         | Nitrogen mass-fraction                     |
| Metals/O         | Oxygen mass-fraction                       |
| Metals/Ne        | Neon mass-fraction                         |
| Metals/Mg        | Magnesium mass-fraction                    |
| Metals/Si        | Silicon mass-fraction                      |
| Metals/S         | Sulfur mass-fraction                       |
| Metals/Ca        | Calcium mass-fraction                      |
| Metals/Fe        | Iron mass-fraction                         |
| Metals/TotalMass | Total Mass term. Does not include Hydrogen |

With the  `/../MassFraction/Metals.MetalOnlyDenominator` attribute set to `False`.

`TotalMass` is $x_0$.

:::
::::
