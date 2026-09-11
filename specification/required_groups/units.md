(units)=
# Units

The `/Units` top-level group contains the transformations between the Internal Unit system used in the _snapshot_ and the CGS system[^practical-cgs].
Generally, this is the same unit system used internally in the simulation code, but that is not required[^swift-units].

Each attribute is the equivalent of the unit multiplication factor $\frac{\text{internal unit}}{\text{CGS unit}}$ such that e.g. `BoundingBox_in_CGS = /Header.Bounding_box * Unit_length_CGS`.

:::{admonition} CGS vs PhysCGS
:class: note
The `Unit_X_CGS` fields are pure unitary conversions; do _not_ include any $h$- or $a$-factors (i.e. $cm$, not $cm/h$).
The `Unit_X_PhysCGS` fields _are_  physical conversions and _should_ include relevant $h$- or $a$-factors.
So e.g. `Unit_length_CGS=Unit_length_PhysCGS` if the simulation is in physical units to begin with, or $a=h=1$.
:::

All attributes are simple numbers and are **required**.

:::{table} Unit Quantity Table
:label: unit-table

| Name                     | CGS unit   | Abbreviation |
| ------------------------ | ---------- | :----------: |
| Unit_length_CGS          | centimeter |     U_L      |
| Unit_mass_CGS            | gram       |     U_M      |
| Unit_time_CGS            | second     |     U_t      |
| Unit_temperature_CGS     | Kelvin     |     U_T      |
| Unit_current_CGS         | Ampere     |     U_I      |
| Unit_length_PhysCGS      | centimeter |     U_pL     |
| Unit_mass_PhysCGS        | gram       |     U_pM     |
| Unit_time_PhysCGS        | second     |     U_pt     |
| Unit_temperature_PhysCGS | Kelvin     |     U_pT     |
| Unit_current_PhysCGS     | Ampere     |     U_pI     |
:::


[^practical-cgs]: CGS here is more closely the [](wiki:Centimetre-gram-second_system_of_units#Practical_CGS_units).
[^swift-units]: See [Swift InternalCodeUnits](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#unit-systems) for example of where this may not be the case.
