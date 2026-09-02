---
short_title: Mass Fraction
---
(tag-chem-mass-frac)=
# Mass-fraction-based Quantities

Tag: `MassFraction`

Includes:  [`Massive`](#tag-massive)

Tag-Description: Mass-fraction-based chemical abundances

Subgroups: `MassFractions`

Subgroup-Description: Mass fraction-based chemical abundances

Chemical abundances are defined using the mass fraction, i.e.
$$
\label{eq:massfrac-def}
x_i = \frac{m_i}{m_{\rm total}} \equiv \frac{\rho_i}{\sum_j \rho_j} \equiv \frac{m_i n_i}{\sum_j m_j n_j},
$$
where $m_i$, $\rho_i$ and $n_i$ are the mass, mass density, and number density of species $i$.

This is a dimensionless quantity!

(tag-mass-frac-denominator)=
## Denominator species

Because the choice of which species to include in the denominator is ambiguous, we require the list(s) to be specified in the attribute `/../MassFractions/X.Denominator_species` for species `X`.
(This applies to subspecies too: `/../MassFractions/X/i.Denominator_species`)

This field contains the list of species (using the same names as the relevant datasets) used in the denominator.

Example (uniform denominator):

```python
gusteau_hdf["/gas/MassFractions/Hydrogen"].attrs["Denominator_species"] == [
    "Hydrogen",
    "Helium",
    "Carbon",
    "Nitrogen",
    "Oxygen",
    "Neon",
    "Magnesium",
    "Silicon",
    "Iron"
]
```

Example (separate denominators):

```python
# separate hydrogen abundances
gusteau_hdf["/gas/MassFractions/Hydrogen/i"].attrs["Denominator_species"] == [
        "Hydrogen/i",
        "Hydrogen/ii",
        "Hydrogen/two",
        "Hydrogen/minus"
    ]
# Everything else
gusteau_hdf["/gas/MassFractions/Carbon"].attrs["Denominator_species"] == [
    "Helium",
    "Carbon",
    "Nitrogen",
    "Oxygen",
    "Neon",
    "Magnesium",
    "Silicon",
    "Iron"
]
```

(tag-mass-frac-totalmasses)=
## Total Masses

For clarity, we recommend including the denominator term(s) as additional datasets if they are not specified elsewhere as `TotalMasses` or `TotalXXXMasses`, especially if multiple denominators are used.
