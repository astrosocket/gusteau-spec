(units)=
# Units

The `/Units` top-level group contains the transformations between the Internal Unit system used in the _snapshot_ and the CGS system[^practical-cgs].
Generally, this is the same unit system used internally in the simulation code, but that is not required[^swift-units].

Each attribute is the equivalent of the unit multiplication factor $\frac{\text{internal unit}}{\text{CGS unit}}$ such that e.g. `BoundingBox_in_CGS = /Header.BoundingBox * UnitLength_CGS`.
Further, these are pure physical conversions; do _not_ include any $h$-factors (i.e. $cm$, not $cm/h$).

All attributes are simple numbers and are **required**.

:::{table} Unit Quantity Table
:label: unit-table
| Name                | CGS unit   | Abbreviation |
| ------------------- | ---------- | :----------: |
| UnitLength_CGS      | centimeter |     U_L      |
| UnitMass_CGS        | gram       |     U_M      |
| UnitTime_CGS        | second     |     U_t      |
| UnitTemperature_CGS | Kelvin     |     U_T      |
| UnitCurrent_CGS     | Ampere     |     U_I      |
:::


[^practical-cgs]: CGS here is more closely the [](wiki:Centimetre-gram-second_system_of_units#Practical_CGS_units).
[^swift-units]: See [Swift InternalCodeUnits](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#unit-systems) for example of where this may not be the case.
