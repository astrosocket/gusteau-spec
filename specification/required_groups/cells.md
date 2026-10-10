(cells)=
# Cells

(cells-backwards)=
:::{admonition} Backwards Compatibility
:class: caution
A number of fields are copied directly from the Swift format for backwards compatibility (i.e. so various analysis tools can work as is on GUSTEAU snapshots).
As such the naming conventions and other aspects in the following may not match the rest of the GUSTEAU standard.
:::

GUSTEAU enforces a top-level grid structure on all particles, called cells, similar to that found in [Swift](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#quick-access-to-particles-via-hash-tables).

Every cell contains some number of particles, say $n_i$, and for given particle $P_j$, will contain all of the information about that particle.

The purposes are two-fold:

1. *Keep contiguous particles together.*
    For multi-part files, each file corresponds to a sub-set of the cells, either a 1-1 mapping or multiple cells per file.
    :::{admonition}
    :class: danger
    Cells are **not** permitted to be split over multiple files.
    :::
    The files are then split at cell boundaries, i.e. file 0 may contain cells 0-5, file 1 contains cells 6-11, etc.

    - If `packingcubes` _is not_ being used, each file will map 1-1 to a cell.
        Note, however, that there is no implied particle ordering within the cell, so you may need to load all particles within the cell to find a particular subset.
        (This is usually how multipart snapshot files are implemented in e.g. Gizmo.)
    - If `packingcubes` is being used, the particles in $\text{cell}_i$ are additionally guaranteed to be spatially close and spatially ordered.
        Thus, particles in the beginning region of the cell are spatially closer together than to particles in later regions.

  
2. *Speed up spatial search.*
    - If `packingcubes` _is not_ being used on the dataset, you can spatial search at the cell level to reduce that amount of data loaded/traversed/etc. 
        So if you wanted to interogate the properties of particles in a region, you first compute the cell overlap with that region, which can be done without loading any particle data.
        Then, for the cells that overlap, you can load the data for just those cells from their corresponding files or from the original virtual dataset.
    - If `packingcubes` _is_ being used on the dataset, each cell gets its own tree. 
        So one can quickly spatially search for particles by
        1. Computing which cells overlap the region of interest. 
            Note that this is a relatively trivial calculation that requires no data loading.
        2. For each overlapping cell
            1. If the cell is entirely contained, load the entire cell (or at least the datasets of interest)
            2. Otherwise, load the corresponding tree (i.e. for cell 64, load tree 64) as a `PackedTree`
            3. Search the `PackedTree` with the original region of interest and load the returned dataset slices
    
    (Note that `packingcubes` (and soon `swiftsimio`) does all of these steps for you...)

(cells-gridding)=
## Gridding
The grid is assumed to be a $D$ dimensional rectangular prism with $C_i$ cells per dimension.
Note, however, that there may exist additional cells out-/along-side the grid (e.g. see [zoom-in sims](#cells-bounding_boxes-zoom)). 
To support that, the gridded cells are assumed to occupy the first $C_g=\prod_i C_i$ (like $C_{x}\times C_{y}\times C_{z}$) rows of any relevant field, with the $C_{ng}$ leftover cells following.

Thus, the total number of cells, $C=C_g + C_{ng}$.

(cells-bounding-boxes)=
## Bounding boxes
Each cell has a bounding box, and all particles in the cell are guaranteed to be within that bounding box.

:::{admonition} Caution
:class: caution
Bounding boxes can be larger than their corresponding grid space!
:::

(cells-bounding-box-overlap)=
### Overlapping bounding boxes

For the most part, bounding boxes are mutually exclusive, but in some cases they can overlap:

:::{admonition} `packingcubes`
:class: tip
If you use `packingcubes` with the default options on an ungridded snapshot, it will form a grid at the top layer of the simulation's bounding box, and each particle will be sorted within one of those grid cells.

(cells-bounding_boxes-zoom)=
**Zoom-in sims:**
However, you could specify a _smaller_ bounding box than the overall simulation, at which point `packingcubes` generates a special _overflow_ grid cell (so if the grid is $N$ cubes on a side, there are $N+1$ total cells).
The _overflow_ grid cell is the same size as the overall simulation bounding box, and captures all particles not
contained in the smaller, specified box.
As such, it overlaps with _all_ of the other grid cells.

This process could be useful for the case of zoom-in simulations, for example, where the total simulation could occupy a large volume, but the interesting physics only occurs in a smaller subvolume.
:::

::::{admonition} Simulation-supplied cells
:class: tip
Alternatively, the simulation code can specify grid cells, at which point GUSTEAU makes no guarantees on which bounding boxes overlap or not.

:::{admonition} Example: Swift Drift
:class: example
:class: dropdown
Particles in Swift can _drift_ outside of their top-level cells between tree rebuilds[^SwiftDrift].
When this occurs, the cell bounding boxes will overlap, even though the cells, as defined, do not.

[^SwiftDrift]: Second paragraph [here](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#quick-access-to-particles-via-hash-tables).
:::
::::



(cells-attrib_datasets)=
## Attributes and Datasets

The `/Cells` group contains the following attributes and datasets.
All fields are **required**.
Note that some of the following attributes are attached to the `Meta-data` subgroup, rather than on the `Cells` group directly.
We have substituted the most common values for some of the attribute sizes in the following table, like 6 for the length of a bounding box instead of $2D$, or 3 for the width of the `Centres` array.

| Name                                                                        | Field Type                              | Description                             |
| --------------------------------------------------------------------------- | --------------------------------------- | --------------------------------------- |
| [`Grid_box`](#cells-attrib_datasets-Grid_box)                               | attribute, (6,) - sized numeric array   | Overall bounding box for the grid boxes |
| [`Number_of_grid_cells`](#cells-attrib_datasets-Number_of_grid_cells)       | attribute, positive integer             | Total number of cells in the grid       |
| [`Number_of_nongrid_cells`](#cells-attrib_datasets-Number_of_nongrid_cells) | attribute, positive integer             | Total number of cells not in the grid   |
| [`BoundingBoxes`](#cells-attrib_datasets-BoundingBoxes)                     | dataset, ($C$, 6) - sized numeric array | Bounding box for each cell              |
| [`Centres`](#cells-attrib_datasets-Centres)                                 | dataset, ($C$, 3) - sized numeric array | Center point of each cell               |
| [`Meta-data.dimension`](#cells-attrib_datasets-dimension)                   | attribute, (3, ) - sized numeric array  | Number of grid cells in each dimension  |
| [`Meta-data.nr_cells`](#cells-attrib_datasets-nr_cells)                     | attribute, positive integer             | Total number of cells                   |
| [`Meta-data.size`](#cells-attrib_datasets-size)                             | attribute, (3, ) - sized numeric array  | Size of a single grid cell              |

(cells-attrib_datasets-Grid_box)=
### `/Cells.Grid_box`
The overall bounding box for the grid in the form `[x, ..., dx, ...]`.
This field has the same units (simulation units) as [`/Header.Bounding_box`](#header-bounding_box), including any cosmological factors.
For most use-cases, this will be equivalent to [`/Header.Bounding_box`](#header-bounding_box), but may be smaller.

(cells-attrib_datasets-Number_of_grid_cells)=
### `/Cells.Number_of_grid_cells`
Total number of cells in the grid.
This is defined as $\prod_i C_i = C_{g}$ , assuming the definitions used above.

(cells-attrib_datasets-Number_of_nongrid_cells)=
### `/Cells.Number_of_nongrid_cells`
Total number of not-in-the-grid cells ($C_{ng}$).
This number is typically 0, but could be 1 for example if `packingcubes` is using an overflow box or all the cells, if the simulation uses an unusual gridding scheme like spherical coordinates.

(cells-attrib_datasets-BoundingBoxes)=
### `/Cells/BoundingBoxes`

$[C, 2D]$ dataset with each row corresponding to that cell's bounding box in the form `[x, ..., dx, ...]` in simulation units.
If only one cell is requested/provided, then the sole entry will match [](#cells-attrib_datasets-Grid_box).

(cells-attrib_datasets-Centres)=
### `/Cells/Centres`

$[C, D]$ dataset with each row corresponding to that cell's center point in simulation units.

(cells-attrib_datasets-dimension)=
### `/Cells/Meta-data/dimension`
The total number of cells in each dimension in the grid.

(cells-attrib_datasets-nr_cells)=
### `/Cells/Meta-data/nr_cells`
The total number of cells, equivalent to [$C_g$](#cells-attrib_datasets-Number_of_grid_cells) + [$C_{ng}$](#cells-attrib_datasets-Number_of_nongrid_cells).

(cells-attrib_datasets-size)=
### `/Cells/Meta-data/size`
The size in simulation units of a single _grid_ cell.
Note that nongridded cells may be differently sized and potentially nonuniform.

(cells-subgroups)=
## Per-cell Subgroups

The `/Cells` group contains the following subgroups.
Each subgroup contains $P$ datasets, one for each particle type, that specify the described quantity for that particle type.
For example, `/Cells/Counts/gas` would be a $[C,1]$ array specifying the number of gas particles in each cell, `/Cells/Counts/stars` would specify the number of star particles per cell, etc.

All subgroups have an attribute, "Description", with the value in this table:

| Name                     | Description                                                                            |
| ------------------------ | -------------------------------------------------------------------------------------- |
| [](#cells-Counts)        | The number of particles of the particular type.                                        |
| [](#cells-Files)         | The number of the actual file containing the cell's particles.                         |
| [](#cells-MaxPositions)  | Maximum coordinates of the particular particle type for that cell in simulation units. |
| [](#cells-MinPositions)  | Minimum coordinates of the particular particle type for that cell in simulation units. |
| [](#cells-OffsetsInFile) | Index to the start of the cell in the file it's stored in.                             |


(cells-Counts)=
### `/Cells/Counts`
The number of particles of the particular type.

(cells-Files)=
### `/Cells/Files`
The number of the actual file containing the cell's particles.

Only relevant when the number of files ([`/Header.Num_files_per_snapshot`]) is $>1$.
Thus, if `/Cells/Files/gas[42] = 15`, then the gas particles for cell 42 are all contained in the 15th partfile.

(cells-MaxPositions)=
### `/Cells/MaxPositions`
Maximum coordinates of the particular particle type for that cell in simulation units.

If the cell does not contain any particles of that type, $-\infty$ in all dimensions.

If the cell does contain particles, then the max position is strictly contained with the bounding box, i.e. `/Cells/MaxPositions/PartTypeX[i,:] <= /Cells/Bounding_boxes[i,:3] + /Cells/Bounding_boxes[i,3:]`.

(cells-MinPositions)=
### `/Cells/MinPositions`
Minimum coordinates of the particular particle type for that cell in simulation units.

If the cell does not contain any particles of that type, $\infty$ in all dimensions.

If the cell does contain particles, then the min position is strictly contained with the bounding box, i.e. `/Cells/MinPositions/PartTypeX[i,:] >= /Cells/Bounding_boxes[i,:3] + /Cells/Bounding_boxes[i,3:]`.

(cells-OffsetsInFile)=
### `/Cells/OffsetsInFile`
Index to the start of the cell in the file it's stored in. 

Note that this is specific to the containing file, not the overall array!

See [](#cells-single-cell) for more details

(cells-Trees)=
## The `/Cells/Trees` Subgroup
The `Trees` subgroup is optional and is only present when packing cubes is used.
It has a slightly different structure than the [](#cells-subgroups) and so has been separated out, but it otherwise behaves similarly.

**Description**: The `Trees` subgroup stores the `PackedTree` data for each cell.

Since the length of the tree data depends on the number of particles in cell, vertically concatenating the trees into a $C$-row dataset would produce a ragged matrix, which does not support efficient, rapid access.
Instead, each tree is stored as a separate dataset, with `tree_i` corresponding to `cell_i`, aka the $i$th row.

Just like the other subgroups, the trees are sorted by particle type, as particle type mixing is disallowed.

So an example layout could look like
```
/Cells/
    Trees/
        gas/
            tree_0
            tree_1
            ...
        stars/
            tree_0
            tree_1
            ...
        ...
```

:::{admonition} Have a better layout?
:class: help
Since this can be difficult to easily parse when manually exploring, we are actively exploring other organizational layouts.
If you have a better idea, please contact us!
:::


(cells-single-cell)=
## Application: Loading the data in a single cell

To access individual cells:

0. (Assume we are interested in all gas particle temperatures in cell 54 (zero-indexed))
1. Find the file cell 54 is in: 
   ```python
   file_number = snapshot["/Cells/Files/gas"][54]
   ```
2. Find the slice corresponding to cell 54:
   ```python
   slice_beg = snapshot["/Cells/OffsetsInFile/gas"][54]
   slice_len = snapshot["/Cells/Counts/gas"][54]
   slice_end = slice_beg + slice_len
   ```
3. Load only the temperature data corresponding to cell 54 slice:
   ```python
   with h5py.File(snapshot_partfiles[file_number]) as partfile:
     temp_slice_54 = partfile["/gas/Temperature"][slice_beg:slice_end]
   ```

(cells-load-subregion)=
#### Load gas temperatures in specific subregion only
(requires `packingcubes`)

1. Complete steps 1 & 2, from above
2. Load the PackedTree for the cell
    ```python
    # ideally all the trees would be loaded ahead of time and cached, but if not..
    tree = packingcubes.PackedTree(snapshot["/Cells/Trees/gas/tree_54"])
    ```
3. Search the tree[^tree-search]
    ```python
    index_array = tree.get_particle_indices_in_box(box)
    # or
    index_array = tree.get_particle_indices_in_sphere(sphere)
    ```
4. Load region data
    ```python
    temps = []
    with h5py.File(snapshot_partfiles[file_number]) as partfile:
        for chunk_beg, chunk_stop, _ in index_array:
            temps.append(partfile["/gas/Temperature"][chunk_beg:chunk_end])
    ```


[^tree-search]: From [tutorials/ParticlesWithinShape](https://packingcubes.readthedocs.io/en/latest/Users-Guide/Tutorials/ParticlesWithinShape)
