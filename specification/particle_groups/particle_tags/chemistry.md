(tag-chemistry)=
# Chemistry

Includes:  [`Massive`](#tag-massive)[^mass-frac], [`NumberDensity`](#tag-chem-number)|[`MassDensity`](#tag-chem-mass)|[`Abundance`](#tag-chem-abundance)|[`MassFraction`](#tag-chem-mass-frac)

Particles with an internal state that represents some form of "chemistry".
For consistancy, tags in the chemistry group **must pick at least one** of [`Abundance`](#tag-chem-abundance), [`MassDensity`](#tag-chem-mass) [`MassFraction`](#tag-chem-mass-frac), or [`NumberDensity`](#tag-chem-number) to represent chemical quantities for inclusion.

Thus an example tag set could be `["Abundance", "Hydrogen", "Metallic"]` to represent [abundance-based](#tag-chem-abundance), metallic & hydrogen chemistry.

The chemical quantities will then be listed under the corresponding subgroups, listed here for convenience:

* `Abundances`
* `MassFraction`
* `NumberDensity`
* `MassDensity`

Continuing the above example could define the following fields:

```
/.../Abundances/Hydrogen/i
/.../Abundances/Electrons
/.../Abundances/Hydrogen/ii
/.../Abundances/Hydrogen/molecular
/.../Abundances/Carbon
/.../Abundances/Metals
/.../Abundances/Aluminium
/.../Abundances/Sulfur
```
:::{admonition} 
:class: tip
`Carbon`, `Aluminium`, and `Sulfur` are examples and not required.
:::

Note, however, that since more than one of `Abundance`/etc. can be selected, chemical quantities can be split across subgroups without repeating analogous fields.
For example,

```
/.../Abundances/Hydrogen/i
/.../Abundances/Electrons
/.../MassFractions/Hydrogen/ii
/.../MassFractions/Hydrogen/molecular
```

is a valid implementation of `Abundance`, `MassFraction`, `Hydrogen`.

(tag-chemistry-elements)=
## Elements

For simple chemical simulation, elemental quantities should be included as single datasets using the IUPAC name below the appropriate `Abundance`/etc. group, for example[^iupac]:

```
/.../MassFractions/Carbon
/.../NumberDensities/Iron
```

[^iupac]: For Americans, that means aluminium, not aluminum. On the other hand, sulfur beat sulphur.

However, more extensive chemistry might track ionization states, or atomic and molecular forms.
For these cases, specify the element as a tag at the same level as `Abundances`/etc. (e.g. `Helium`) and then, instead of a dataset, use a group with that element name and specify the tracked forms as datasets under that group.
For common ionization states, like $\text{H}^+ \equiv \text{HII}$, $\text{He}^{++}\equiv \text{HeIII}$, where the state is specified by roman numerals, use the lower case roman numerals as the name.
For other cases, like $\text{H}_2$ or $\text{H}^{-}$, specify `molecular` or `minus` (but see [](#tag-chemistry-dust)).
So the following might occur with the helium tag:

```
/.../NumberDensities/Helium/i
/.../NumberDensities/Helium/ii
/.../NumberDensities/Helium/iii
```

or the hydrogen tag and tracking $\text{H}$, $\text{H}^{+}$, $\text{H}_2$, $\text{H}^{-}$, & $\text{H}_{3}^{+}$:

```
/.../Abundances/Hydrogen/i
/.../Abundances/Hydrogen/ii
/.../Abundances/Hydrogen/two
/.../Abundances/Hydrogen/minus
/.../Abundances/Hydrogen/three_ii
```

(tag-chemistry-dust)=
## Dust, Metals, and Compounds

:::{admonition} HELP WANTED
:class: attention
We are actively seeking input on this section! If you have opinions, please get in touch by contacting the authors or submitting an [issue](https://github.com/astrosocket/gusteau-spec/issues/new?assignees=&labels=add-missing&projects=&template=02-add-missing.md&title=)!
:::

To add dust chemistry, use the same format as the extended chemistry: a `Dust` tag, a `Dust` subgroup under the appropriate `Abundances`/etc. group, and labeling individually tracked dust species. 

The same idea holds for compounds, though the names are trickier.
We suggest using the IUPAC names for simpler names (like deuterated hydrogen for $\text{HD}$, as e.g. `/../Abundances/DeuteratedHydrogen`) or common names (`/../Abundances/MethaneIce`), but we do not yet have a solution for more complicated chemicals.

For generic tracking of *metals*, use the `Metals` tag and the `Metals` dataset, as demonstrated above.


(tag-chemistry-denominators)=
## Abundance and Mass Fraction denominators

:::::{tab-set}
::::{tab-item} Abundances
:sync: quantity-denominators
:::{embed} #tag-abundance-denominator
:::
::::
::::{tab-item} Mass Fractions
:sync: quantity-denominators
:::{embed} #tag-mass-frac-denominator
:::
::::
:::::

## Chemistry specific tags:

The following are chemistry specific tags:

:::{toc}
:context: children
:::

[^mass-frac]: Only included if [`MassFraction`](#tag-chem-mass-frac) or [`MassDensity`](#tag-chem-mass) is included.
