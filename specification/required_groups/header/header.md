---
numbering: false
---
# Header

Located at `/Header`. Only attribute information is required, no `Dataset`s. 

(Some parts paraphrased from [Swift documentation](https://swift.strw.leidenuniv.nl/docs/Snapshots/index.html#quick-access-to-particles-via-hash-tables))
The header group (`/Header`) contains basic information about the simulation and the number of particles. It is a required top-level group, and as such has several mandatory fields that may be duplicated/symbolically linked with fields/data elsewhere in the file.  Other fields are not mandatory, but should be provided if possible. There is no proscription against fields not already listed.

(header-attributes)=
## Header Attributes

The following attributes are required and are described in the remainder of this section. A quantity in brackets signifies an array of that length.  Fields without a default value must be provided by the simulation code, either directly or via a translation.

| Name                   |          Type          | Brief Description                                      | Link                               | Default Value          |
| ---------------------- | :--------------------: | ------------------------------------------------------ | ---------------------------------- | ---------------------- |
| Code                   |         string         | Simulation code identifier                             | [](#header-code)                   |                        |
| Source                 |         string         | Snapshot file format source                            | [](#header-Source)                 |                        |
| Source_style_file      |         string         | Translation file                                       | [](#header-source_style_file)      |                        |
| Particle_names         |      string[$P$]       | List of particle names                                 | [](#header-particle_names)         |                        |
| Particle_numbers       | uint64[$P$] [^partnum] | List of particle numbers                               | [](#header-particle_numbers)       |                        |
| Initial_mass_table     |      number[$P$]       | Initial particle masses                                | [](#header-initial_mass_table )    |                        |
| Bounding_box           |       double[6]        | `[x,y,z,dx,dy,dz]` of primary simulation region        | [](#header-bounding_box )          |                        |
| Time                   |         number         | Simulation time of this snapshot                       | [](#header-Time )                  |                        |
| Run_name               |         string         | User-specified descriptive name of simulation run      | [](#header-run_name)               | `""`                   |
| Num_files_per_snapshot |         int32          | Number of files per snapshot                           | [](#header-num_files_per_snapshot) | 1                      |
| Dimension              |          int           | Dimensionality of the simulation                       | [](#header-Dimension)              | 3                      |
| Part_type_mapping      |  int[6] or string[6]   | Particle name mapping to `PartType0`, `PartType1`, etc | [](#header-part_type_mapping)      | See description        |
| Snapshot_date          |         string         | Snapshot creation timestamp                            | [](#header-Snapshot_Date)          | snapshot creation time |
| Redshift               |         number         | Cosmological redshift of this snapshot                 | [](#header-Redshift)               | 0                      |

(header-code)=
### `Code`

The `Code` field should provide a short name for the simulation code, possible values could include `gadget-4`, `opengadget`, `arepo`, `swift`. The field must be normalized to lower case ASCII (i.e. `OpenGadget`=`opengadget`, `Arepo`=`AREPO`=`arepo`) to minimize ambiguity and simplify identification.  This field should not contain any version information (beyond e.g. `Gadget-2` vs `Gadget-4`); all information along those lines should be in the `/Code` group.
A non-exclusive list of possible values is provided here:
 
| Simulation Code | Normalized Name |
| --------------- | --------------- |
| Gadget-2        | gadget-2        |
| Gadget-3        | gadget-3        |
| OpenGadget      | opengadget      |
| Gadget-4        | gadget-4        |
| AREPO           | arepo           |
| GIZMO           | gizmo           |
| Swift           | swift           |

(header-source)=
### `Source`

The `Source` field should correspond to one of
1. `GUSTEAUvX.Y.Z`, where `X.Y.Z`  are the `Major.Minor.Patch` version numbers (so a snapshot following the format in this document would be `GUSTEAUv0.1.0`)
2. The [translations][translations] provided with Project GUSTEAU. See the [list](https://) of provided translations.
3. The full file path of a custom `.translation` file. So a `GizmoR2020.translation` file would be e.g. `/Data/user012345/GizmoR2020.translation`

(header-source_style_file)=
### `Source_style_file`

For option 1 of the `Source` field, the `Source_style_file` field will be empty.
For options 2 & 3, the `Source_style_file` field will contain the _full_ file contents of the translation style file as a utf8 string.
Note that this may be considered a [large attribute](https://docs.h5py.org/en/latest/high/attr.html#large-attributes), depending on the file size (i.e. if the file is > 64 KiB).

(header-particle_names)=
### `Particle_names`

The names of the top-level groups with particle data.
In a Gadget-2-based snapshot, an example would be `["PartType0", "PartType1", "PartType5"]` for a simulation with baryonic gas, dark matter, and sink particles.
A Swift-based snapshot might have `["gas", "dark_matter", "stars", "black_holes"]`.  
 
There is no restriction on number of particle types, but aliases should not be included.
So for example, if `PartType0` and `gas` are both links to the same dataset, only one  of `"PartType0"` and `"gas"` should be present in `Particle_names` (and preferably `"gas"`, as the more descriptive name).
  
The length of this array is the quantity $P$.

(header-particle_numbers)=
### `Particle_numbers`

The number of particles for each type in `Particle_names`. For a given particle group dataset, this sets the quantity $N$.

[^partnum]: uint64 is the minimum size for Particle_numbers (supporting $\sim10^{19}$ particles). Larger integer sizes are allowed if available.

(header-initial_mass_table)=
### `Initial_mass_table `

Specify a uniform initial mass for a particle type.
Specifying 0 for a particle type could mean one of two things.
Either the particle type is massless (and ideally uses the appropriate tag) or the mass is specified on a per-particle basis (requiring the `MassiveParticle` tag at minimum).

(header-bounding_box)=
### `Bounding_box `

Specify the region of interest for the simulation as `[x, y, z, dx, dy, dz]`, where `x/y/z` are the coordinates of the left-front-bottom vertex and `dx/y/z` are the width-depth-height of the box.
Note that if [[#`Dimension`|the dimension]] is less than 3, the corresponding terms can be skipped (i.e. `BoundingBox=[x, dx]` for 1D). 
`x/y/z` can be positive or negative; `dx/y/z` must be non-negative.

Particles are not required to be in contained in the `Bounding_box`, but likewise `Project GUSTEAU`-compatible software are not required to treat particles outside the bounding box in the same fashion as interior particles.
For example, they do not need to load or render particles outside the bounding box.  

(header-time)=
### `Time `

Snapshot time in internal units.

(header-run_name)=
### `Run_name`

User-specified name of this run.
Defaults to the empty string.[^runname] 

[^runname]: While we could default to the filename, since that is often a permutation of `snapshot_XXX.hdf5`, the likelihood of it being more useful than the empty string is low.

(header-num_files_per_snapshot)=
### `Num_files_per_snapshot`

The number of files that correspond to this snapshot.
Note that since GUSTEAU uses virtual datasets, this should not be especially relevant to the average user.

(header-dimension)=
### `Dimension`

Spatial dimensionality of the simulation.
This sets the quantity $D$, seen for example in the number of components in the `Positions` field of a particle.
Note that only 1, 2, & 3 dimensions are supported currently.
If not provided, defaults to 3.

(header-part_type_mapping)=
### `Part_type_mapping`

Mapping between particle types listed in `ParticleNames` and Gadget-2 style `PartTypeX` particle types.
Can be a 6-element array of indices (e.g. `[0, -1, -1, -1, 1, 2]` for `ParticleNames = ["gas","stars","bh"]`) or strings (e.g. `["gas",  "",  "",  "",  "stars", "bh"]`).
Placeholders (either `""` or `-1`) specify no particle type match.
  
If not provided, defaults to the order of particle-type groups found in the file in two passes.
First, look for the first particle-type group that fulfills the Gadget-2 roles (`PartType0`=`HydroParticle`, `PartType1`=`SPHParticle`, `PartType2`=`SPHParticle`, `PartType3`=`SPHParticle`, `PartType4`=`StarParticle`, `PartType5`=`SinkParticle`), then first particle-type group that has not yet been chosen.
Since this can lead to unexpected results, we highly suggest specifying this field.

(header-snapshot_date)=
### `Snapshot_date`

The ISO 8601 (extended) formatted snapshot creation time, pulled from the file creation time if not otherwise provided.
Time must be in UTC or have the time offset included.
Example: 2026-06-08T23:41:00.0Z or 2026-06-08T18:41:00.0-05:00.

(header-redshift)=
### `Redshift`

The cosmological redshift of this snapshot.
Defaults to 0.
Only well defined if simulation is cosmological (`/Cosmology.IsCosmological` is `True`),  and/or `Time`=0.
Identical to [`/Cosmology.Redshift`](#cosmo-redshift), if present.


## Gadget-2
:::{include} gadget-2.md
:::

