---
short_title: Abundance
---
(tag-chem-abundance)=
# Abundance-based Quantities

Tag: `Abundance`

Includes:  [`Particle`](#tag-particles)

Tag-Description: Normalized number fraction-based chemical abundances

Subgroups: `Abundances`

Subgroup-Description: Normalized number fraction-based chemical abundances

Chemical abundances are defined using the normalized number fraction, i.e.
$$
\label{eq:abundance-def}
\hat{n}_i = \frac{n_i}{\sum_j n_j},
$$
where $n_i$ is the number density of species $i$.

This is a dimensionless quantity!

(tag-abundance-denominator)=
## Denominator species

Because the choice of which species to include in the denominator is ambiguous, we require the list(s) to be specified in the attribute `/../Abundances/X.Denominator_species` for species `X`.
(This applies to subspecies too: `/../Abundances/X/i.Denominator_species`)

This field contains the list of species (using the same names as the relevant datasets) used in the denominator.

Example (uniform denominator):

```python
gusteau_hdf["/gas/Abundances/Hydrogen"].attrs["Denominator_species"] == [
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
gusteau_hdf["/gas/Abundances/Hydrogen/i"].attrs["Denominator_species"] == [
        "Hydrogen/i",
        "Hydrogen/ii",
        "Hydrogen/two",
        "Hydrogen/minus"
    ]
# Everything else
gusteau_hdf["/gas/Abundances/Carbon"].attrs["Denominator_species"] == [
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

(tag-abundances-totalabundances)=
## Total Abundances

For clarity, we recommend including the denominator term(s) as additional datasets if they are not specified elsewhere as `TotalAbundances` or `TotalXXXAbundances`, especially if multiple denominators are used.
