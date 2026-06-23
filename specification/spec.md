---

abbreviations:
    GUSTEAU: Grand Unified Snapshot That Everyone Agrees Upon
    VCS: Version Control Software
    HDF5: Hierarchical Data Format Version 5

---

# Specification

## Notation
Table of quantities used in multiple places throughout. 

(quantity-table)=

| Name | Brief Description                | Definition                                   |
| ---- | -------------------------------- | -------------------------------------------- |
| $P$  | Number of unique particle types  | [`ParticleNames`](#header-ParticleNames)     |
| $N$  | Number of particles in that type | [`ParticleNumbers`](#header-ParticleNumbers) |
| $D$  | Dimensionality of the simulation | [`Dimension`](#header-Dimension)             |

(field-notation)=
### Fields
We use the notation `/GroupName/Dataset` for HDF5 `Group`s and `Dataset`s, and denote group/dataset attributes with a period, i.e. `/Header.Code` or `/gas/density.Description`. A _field_ could then be either an attribute or a dataset.

## File format
Snapshots will be stored as HDF5 files using HDF5 v2.0 (v2.1.1+ preferred, but not yet supported by h5py pre-built v3.16)

Snapshots will be compressed using lossless compression unless otherwise specified.  This compression is transparent to the user. 

The files will be composed of a number of groups and datasets. Only 5 groups are required: **Header**, **Code**, **Cosmology**, **RunInfo** and **Units**. They are described in the [Required Groups](#Required-Groups) subsection.

The file may additionally contain groups about particles, initial conditions,  runtime parameters, and other relevant information. They are described in the [Optional Groups](#Optional-Groups) subsection.


(fields)=
## Fields

(see [](#field-notation) for notation and definition)

(field-names)=
### Field names 
`Attribute` and `Dataset` names should not contain any punctuation or whitespace besides _ (underscores). Upper and lower case names are distinct, so for example, `h` and `H` could be different  attributes under `/Cosmology` (though see [](#Attribute-units), below).  Whitespace should be converted to underscores; punctuation should be converted to underscores or omitted on a case by case basis. For example, the field `Conversion factor to CGS (not including cosmological corrections)` could be converted to `Conversion_factor_to_CGS_not_including_cosmological_corrections`.

There is no preference for CamelCase vs snake_case; either is valid but clarity is most important.

(field-types)=
### Field types
In the following sections, fields and datasets often have types specified, like `string` or `int`. In general, these should match the types available in the HDF5 standard, and are only as restrictive as specified. So a `number` type could be stored as any of the integer or floating types available, while a `uint32` type should strictly be stored as a 32-bit unsigned integer. `string`s  are UTF-8 encoded and can be any valid characters unless otherwise noted.

(attribute-units)=
### Attribute units
Some attributes are unit-ful and/or cosmological quantities (e.g. `/Header.Time_CGS`).  If units are not specified, assume that they are in the internal unit system (see [](#Units)). If not in internal units, specify the units in the name, i.e. `Time_CGS` or `Time_Gyr` as opposed to just `Time`. Four abbreviations are also available for simplicity. They can be designated via `_NAME`, e.g. `_CGS` or `_IU`.
 * CGS - centimeter-gram-second unit system. Quantities must be in the _base_  CGS units (time in seconds, distances in centimeters, etc.)
 * IU - internal unit system. Quantities are in whatever unit is used by the simulation code (see [](#Units))
 * NAT - natural units. Similar to IU, quantities may be in an arbitrary base, (eg. setting the gravitational constant $G$ = speed of light $c$ = 1). **Important**: the natural unit definition **must** be provided in the `/Units.NaturalUnitDefinition` field, and the definition **must** be consistent across the entire file.  So if `M_hydrogen_NAT` is approximated as 1 via, e.g. $m_{\rm proton} =1$, `StellarMass_NAT` must also be given in terms of units of $m_{\rm proton}$.
 * SI or MKS - metric system. Quantities must be in the SI base units (kg, s, m, A, K, mol, cd)

Note that these rules only apply to `Attribute`s. `Dataset`s have different rules (see eg. [](#particle-groups-datasets)), though dataset _attributes_ should follow these rules.

(field-best-effort)=
### Required vs. "Best Effort" vs Optional Fields
Required 
: Any field marked as required or mandatory **must** be present in the file *with that name*, e.g. `file['/Header'].attrs['Code']` or `file['/Units']` cannot raise an error/exception. 
  Furthermore, the contents of that field **must** be provided by either the simulation code or the {term}`translator` and no default values are provided. 
  If the value is not known, an error or exception should be raised.
  Hard, soft, or external links are perfectly valid, however; mandatory datasets do not need to be duplicated.
  
  A snapshot missing required fields is assumed to be violating this spec.

"Best Effort"
: Some fields have default values provided or are marked "Best Effort". 
  For those fields, the intention is to provide as much information as possible or indicate that the information is unavailable.
  The field **must** still be present in the file, but the originating code can silently substitute the provided default value if necessary.
  If the default value is present, it is usually safer to assume the value was unknown rather than that specific value.

Optional
: The intention is that very few, if any fields are considered optional, unlike [](#optional-groups).
  If a field is marked optional, it does not _need_ to be present in the snapshot, though it preferably is.


## Group list

The GUSTEAU spec defines the following groups:

:::{toc}
:context: children
:::

(required-groups)=
### Required Groups

These top-level groups are **required** to be present in the file, though some of them may contain minimal information.

(optional-groups)=
### Optional Groups

These groups are **not required** to be present. For example, GUSTEAU snapshots do not actually need to contain any particle data, found in a [](#particle-groups), though they generally do. Likewise, simulation code developers might want to output GUSTEAU snapshots without creating the optional packingcubes structure.

