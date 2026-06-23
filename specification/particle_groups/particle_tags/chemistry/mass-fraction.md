---
short_title: Mass-frac
---
(tag-chem-mass-frac)=
# Mass-fraction-based Quantities

Tag: `Mass-frac`

Includes:  [`Massive`](#tag-massive)

Chemical abundances are defined using the mass fraction, i.e.
$$
x_i = \frac{m_i}{m_{\rm total}} \equiv \frac{\rho_i}{\sum_j \rho_j} \equiv \frac{m_i n_i}{\sum_j m_j n_j},
$$
where $m_i$, $\rho_i$ and $n_i$ are the mass, mass density, and number density of species $i$.

This is a dimensionless quantity!

All abundances given via mass fraction should be denoted as `X_species_name`, so a hydrogen mass fraction would be given as `X_hydrogen`.