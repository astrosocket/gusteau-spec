(data-layouts)=
# Data Layouts

Particle data can be organized in several ways:

1. Top-level cells - data is chunked at a low resolution, generally by a coarse grid. 
  These cells often correspond to a division across nodes in the cluster or leaves in a B-tree.
  All particle data in cell is contiguous on disk, with an internal order that usually follows one of the other layouts.
  Used in Swift snapshots.

2. Random layout - particles are arbitrarily laid out on-disk.
  Particles that are spatially located may far apart on disk and vice-versa.
  Simulation restart files may effectively appear to be in this format.

3. Space-filling curve - data is assigned to points along a space-filling curve.
  Particles that are spatially nearby ideally map to nearby regions on disk.
  Used in Gadget-2 snapshots.

4. Halo/structure-ordered - data is assigned to structures by a structure-finding algorithm.
  All particles in a structure are contiguous on disk, with an unspecified internal order.
  Particles not contained in a structure are dumped to the end, often in random order.
  Used in Arepo snapshots.

:::{image} /specification/data_layout.svg
:alt: Example data layouts. From left to right, a space-filing curve, halo-ordered, and top-level cell.
:::

These layouts can be recursive as well, for example mulitple levels of cells, with the smallest internally ordered using a space-filling curve.


(dl-cells_and_cubes)=
## Top-level Cells and `packingcubes`

Optionally on GUSTEAU creation or {term}`translation` some or all of the particle data can be run through the [`packingcubes`](packingcubes.readthedocs.io) tool.
`packingcubes` will chunk the data into a coarse, user-specified top-level grid, with the option to use any already-present top-level cell/chunk structure.
`packingcubes` will then spatially sort the particle data in each cell (aka `cube`), analogous to a [Z-order](wiki:Z-order_curve)[^future-z] curve, and create a [PackedTree](https://packingcubes.readthedocs.io/en/latest/Users-Guide/Reference/packed_format/) ("Packed Oct-tree") for each cube.
These packing cubes can be found in the [`/Cubes`](#cubes) optional group and used with the `packingcubes` package to perform fast ($\log{N}$) spatial searching of particle data.


[^future-z]: Currently. This may be changed in the future to Hilbert curve variant, or potentially even made user-configurable.