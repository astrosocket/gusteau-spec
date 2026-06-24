---

abbreviations:
    GUSTEAU: Grand Unified Snapshot That Everyone Agrees Upon
    VCS: Version Control Software
    HDF5: Hierarchical Data Format Version 5

---

# Code

The `/Code` group contains information about the simulation code used and contains only attributes. Its values should be filled on a best-effort basis, i.e. the attributes should be present, but may be empty.

(code-attributes)=
## Attributes

| Name                  | Type     | Brief Description                                | Link                       |
| --------------------- | -------- | ------------------------------------------------ | -------------------------- |
| Code                  | string   | Identical to `/Header.Code`                      | [](#header-code)           |
| Code_version          | string   | Descriptive simulation code version string       | [](#Code_version)          |
| Code_hash             | string   | Computed hash of the simulation code             | [](#Code_hash)             |
| HDF5_version          | string   | Version of the HDF5 library used                 | [](#HDF5_version)          |
| VCS                   | string   | Version control software used                    | [](#VCS)                   |
| VCS_id                | string   | VCS identifier                                   | [](#VCS_id)                |
| VCS_repository        | string   | VCS repository location                          | [](#VCS_repository)        |
| Library_versions      | string[] | List of versioned external libraries             | [](#Library_versions)      |
| Configuration_options | string   | Configuration options for running the simulation | [](#Configuration_options) |

(Code_version)=
### `Code_version`

Version of the simulation code used. This could be as simple as the year the code was downloaded (e.g. for Gadget-2) to a full semantic versioning number.

(code_hash)=
### `Code_hash`

Computed hash value of the simulation code/executable prefixed by the hashing function and postfixed by the file/directory, eg. "md5sum-4db7cb9c90cd687fa468f342cd47d287-gizmo".

(hdf5_version)=
### `HDF5_version`

Version of the HDF5 library used to generate the snapshot.

(vcs)=
### `VCS`

Type of version control system used for the simulation code. A non-exclusive list of possibilities includes git, mercurial, svn.

(VCS_id)=
### `VCS_id`

Id of the VCS artifact. In git, this would be the full git revision/commit. 

(VCS_repository)=
### `VCS_repository`

Location of the VCS repository, e.g. [https://github.com/pfhopkins/gizmo-public](https://github.com/pfhopkins/gizmo-public) or [https://github.com/SWIFTSIM/SWIFT](https://github.com/SWIFTSIM/SWIFT). Could also be a local location on a cluster.  This can include branch information.  

(vcs_checkout_data)=
### `VCS_checkout_date`

Date and timestamp that the simulation code was checked out, in [ISO 8601](wiki:ISO_8601) (extended, UTC)  format or ISO 8601 (extended, offset) format.

(library_versions)=
### `Library_versions`

Array of external libraries used, e.g. FFTW, MPI, GSL, and their version info in the form "Name - vVersion". For example, ["FFTW3 - v3.3.4", "GSL - v2.8"]

(configuration_options)=
### `Configuration_options`

String containing configuration options for the simulation code. For example, if the code was run via `./simulator -a --optionB parameter_file`, then `Configuration_options` would be "-a --optionB parameter_file"