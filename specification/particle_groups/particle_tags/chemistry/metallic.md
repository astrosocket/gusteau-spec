(tag-chem-metallic)=
# Metallic

Tag: `Metallic`

Includes: [](#tag-chem-number)|[](#tag-chem-mass)|[](#tag-chem-abundance) |[](#tag-chem-mass-frac), [](#tag-chem-hydrogenic)

Particles whose chemistry includes metallic or molecular elements that are not already included in the `Hydrogen` tag.

Particle groups with this tag **must** include the subgroup `Metals`.
Chemical abundances are then datasets under the `Metals` subgroup defined using their [IUPAC symbol](https://iupac.org/what-we-do/periodic-table-of-elements/)([](doi:10.1515/pac-2019-0603)), possibly including ionization states, with the appropriate prefix.

Ionization states are specified via the lower-case letters `p` and `m` after the appropriate element. 
So He$^{++}$ would be `Hepp` and H$^{-}$ would be `Hm`.

Molecules are specified via alphabetical order of the component elements, with subscripts listed in line, e.g. $\text{C}_{10}H_8$ becoming `C10H8`.

## Denominator terms

Depending on the chemical abundance tag, the `Metallic` subgroup will have an additional **required** attribute:

| Name | Type | Description | Required For |
| --- | --- | --- | --- |
| MetalOnlyDenominator | boolean | Flag specifying whether the summation term in the denominator of the chemical abundance definition only includes metals (`True`) or also includes Hydrogen | Abundance, Mass-Frac |

and **required** dataset:

| Name | Description | Required For |
| --- | --- | --- |
| Metallic/TotalAbundance| Total abundance term. Includes Hydrogen species if `MetalOnlyDenominator` is `False`. Equivalent to $\sum_j n_j$.| Abundance |
| Metallic/TotalMass | Total mass term. Includes Hydrogen species if `MetalOnlyDenominator` is `False`. Equivalent to $\sum_j m_j n_j$ or $x_0$, above.| Mass-Frac |

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

| Name          | Description                       |
| ------------- | --------------------------------- |
| Metallic/N_He | Number density of Helium atoms    |
| Metallic/N_C  | Number density of Carbon atoms    |
| Metallic/N_N  | Number density of Nitrogen atoms  |
| Metallic/N_O  | Number density of Oxygen atoms    |
| Metallic/N_Ne | Number density of Neon atoms      |
| Metallic/N_Mg | Number density of Magnesium atoms |
| Metallic/N_Si | Number density of Silicon atoms   |
| Metallic/N_S  | Number density of Sulfur atoms    |
| Metallic/N_Ca | Number density of Calcium atoms   |
| Metallic/N_Fe | Number density of Iron atoms      |

Note that since the original array was the mass-fractions, these values would need to be transformed via $n_i = x_i x_0/m_i$.
:::
:::{tab-item} Mass Density
:sync: mass

| Name            | Description                     |
| --------------- | ------------------------------- |
| Metallic/Rho_He | Mass density of Helium atoms    |
| Metallic/Rho_C  | Mass density of Carbon atoms    |
| Metallic/Rho_N  | Mass density of Nitrogen atoms  |
| Metallic/Rho_O  | Mass density of Oxygen atoms    |
| Metallic/Rho_Ne | Mass density of Neon atoms      |
| Metallic/Rho_Mg | Mass density of Magnesium atoms |
| Metallic/Rho_Si | Mass density of Silicon atoms   |
| Metallic/Rho_S  | Mass density of Sulfur atoms    |
| Metallic/Rho_Ca | Mass density of Calcium atoms   |
| Metallic/Rho_Fe | Mass density of Iron atoms      |

Note that since the original array was the mass-fractions, these values would need to be transformed via $\rho_i=x_i x_0$.
:::
:::{tab-item} Abundance
:sync: abundance

| Name          | Description         |
| ------------- | ------------------- |
| Metallic/A_He | Helium abundance    |
| Metallic/A_C  | Carbon abundance    |
| Metallic/A_N  | Nitrogen abundance  |
| Metallic/A_O  | Oxygen abundance    |
| Metallic/A_Ne | Neon abundance      |
| Metallic/A_Mg | Magnesium abundance |
| Metallic/A_Si | Silicon abundance   |
| Metallic/A_S  | Sulfur abundance    |
| Metallic/A_Ca | Calcium abundance   |
| Metallic/A_Fe | Iron abundance      |
| Metallic/TotalAbundance | Total abundance term. Does not include Hydrogen. |

With the  `/.../Metallic.MetalOnlyDenominator` attribute set to `True`.

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

| Name          | Description             |
| ------------- | ----------------------- |
| Metallic/X_He | Helium mass-fraction    |
| Metallic/X_C  | Carbon mass-fraction    |
| Metallic/X_N  | Nitrogen mass-fraction  |
| Metallic/X_O  | Oxygen mass-fraction    |
| Metallic/X_Ne | Neon mass-fraction      |
| Metallic/X_Mg | Magnesium mass-fraction |
| Metallic/X_Si | Silicon mass-fraction   |
| Metallic/X_S  | Sulfur mass-fraction    |
| Metallic/X_Ca | Calcium mass-fraction   |
| Metallic/X_Fe | Iron mass-fraction      |
| Metallic/TotalMass | Total Mass term. Does not include Hydrogen |

With the  `/.../Metallic.MetalOnlyDenominator` attribute set to `True`.

`TotalMass` is $x_0$.

:::
::::