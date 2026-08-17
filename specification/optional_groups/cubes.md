(cubes)=
# Cubes
This group contains the serialized data needed for the [`packingcubes`](packingcubes.readthedocs.io) structures.

:::{admonition}
:class: warning
Since `packingcubes` is in active development and not yet stable, the save format listed here is not finalized and may change significantly and without warning.
:::

(cubes-structure)=
## Structure

The basic structure is 
```
- cubes/
    - ParticleType/
        - indices
        - tree_i
        - tree_i.Bounding_box
    - ParticleType.Number_of_cubes
- cubes.Packingcubes_version
```
where the `i` in `box_i`/`tree_i` ranges from 0 to the number of cubes ([`NumberOfCubes`](#cubes-number)), e.g. `box_0`, `tree_100`.

The `ParticleType` substructure is duplicated for each [particle type](#header-particle_names) that has a [`ParticleCubes`](https://packingcubes.readthedocs.io/en/latest/Users-Guide/Reference/Cubes/#packingcubes.cubes.ParticleCubes) object associated with it.

The fields are defined as follows:

(cubes-indices)=
### `indices`

The starting indices into the particle datasets of each cube. Currently a `uint64[N]` array.

(cubes-number)=
### `Number_of_cubes`

The number of cubes in the `ParticleCubes` object. 


(cubes-trees)=
### `tree_i`

The serialized `PackedTree` of the `i`th cube. See the [packed format specification](https://packingcubes.readthedocs.io/en/latest/Users-Guide/Reference/packed_format/).

:::{admonition}
:tip:
This field is semi-optional.
Simulations can provide a collection of bounding-box-like objects in their outputs, similar to SWIFT's [top-level grid](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#quick-access-to-particles-via-hash-tables).
Then, during the translation process `packingcubes` will generate the `PackedTree`, including sorting data positions, etc.
Thus, simulations do not need to compute or provide the `PackedTree` structures or do any data sorting beyond providing top-level boxes to provide this group. 
:::

(cubes-box)=
### `Bounding_box`

The overall bounding box of the `i`th cube as `[x, y, z, dx, dy, dz]`, where `x/y/z/` are the coordinates of the left-front-bottom corner and `dx/dy/dz` are width, depth, and height of the box. Note that for 2 (1) dimensional data, `z` (& `y`) and `dz` (& `dy`) are set to 0 and 1, respectively.

(cubes-version)=
### Packingcubes_version

The version of `packingcubes` used to create the cubes structure.


See also [](#data-layouts).