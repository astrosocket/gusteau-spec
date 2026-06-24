# RunInfo

The `/RunInfo` top-level group contains information about the simulation run that produced this snapshot. 
The attributes on the top-level describe information about the actual run, like the system name and runtime.
`/RunInfo` also contains one or more child groups.
The `Parameters` and `ParameterFiles` groups are "Best-Effort"; the remainder are optional, and simulation code specific.

## Attributes

| Name           |  Type  | Brief Description           | Link                    |           Default Value            |
| -------------- | :----: | --------------------------- | ----------------------- | :--------------------------------: |
| System         | string | Host machine name           | [](#run-system)         |                 ""                 |
| SnapshotDate   | string | Snapshot creation time      | [](#run-snapshotdate)   | [snapshot file creation timestamp] |
| TotalRuntime   | number | Total simulation run time   | [](#run-totalruntime)   |                 -1                 |
| SessionRuntime | number | Simulation session run time | [](#run-sessionruntime) |                 -1                 |


(run-system)=
### `System`

The `System` field contains the name of the "host" machine, e.g. where the MPI rank 0 was placed for MPI simulation codes. Generally on a cluster, this name is whatever UNIX’s `gethostname()` function returns on that system on the primary node. 

(run-snapshotdate)=
### `SnapshotDate`

The `SnapshotDate` field contains the date and time when the file was written in ISO 8601 (extended) format. This should be identical to [`/Header.SnapshotDate`](#header-snapshotdate).

(run-totalruntime)=
### `TotalRuntime`

The total simulation run time (using system time as opposed to e.g. wall clock time) up until this snapshot was produced in seconds. If the simulation was run over multiple sessions (e.g. continued/restarted from a snapshot or restart file), this field should be the sum over each of those sessions' runtime. See also [](#run-sessionruntime).

(run-sessionruntime)=
### `SessionRuntime`

The simulation run time (using system time as opposed to e.g. wall clock time) up until this snapshot was produced in seconds. If the simulation was run over multiple sessions (e.g. continued/restarted from a snapshot or restart file), this field should only be the run time of the session that produced this snapshot. May be identical to [](#run-totalruntime) if there was only one session.

(run-subgroups)=
## Subgroups

The `Parameters` and `ParameterFiles` subgroups are **Best-Effort**.
We recommend including them in all snapshots of a simulation run, but recognize that could be a significant burden.
We suggest at least including them in the first snapshot of the run, thereby enabling post-processing tools to copy them to other snapshots if desired.

Other subgroups are simulation code-dependent.
The intention is that any information about running the simulation, e.g. Swift's `HydroScheme` and `Policy` groups will be stored here (and possibly linked to top-level versions).

(run-parameters)=
### Parameters

Effectively, `Parameters` should contain an attribute for every parameter used to run the simulation; however, as this is entirely simulation code dependent we cannot specify the names, types, etc., here.
Instead, the possible parameters are considered "Best-Effort", with defaults specified by either the simulation code or the {term}`translator`.


(run-parameterfiles)=
### ParameterFiles

The `ParameterFiles` group has two specified `Attribute`s and additional unspecified, optional `Attribute`s. 

| Name              | Description                                   | Link                                      |
| ----------------- | --------------------------------------------- | ----------------------------------------- |
| ParameterFile     | Text contents of main parameter file or error | [](#run-parameterfiles-parameterfile)     |
| ParameterFilePath | File path of main parameter file              | [](#run-parameterfiles-parameterfilepath) |

Additional parameter files can be included via the same mechanism, using descriptive names for each parameter file.
For example, a `GIZMO` run might include the "OutputList"/"Snapshot_Times_Table" file and the "GrackleData" file as:

| Name                  | Description                             |
| --------------------- | --------------------------------------- |
| SnapshotTimesFile     | Text contents of the "OutputListFile"   |
| SnapshotTimesFilepath | File path of the `SnapshotTimesFile`    |
| GrackleDataFile       | Text contensts of the "GrackleDataFile" |
| GrackleDataFilePath   | File path of the `GrackleDataFile`      |

with definitions analogous to [](#run-parameterfiles-parameterfile) and [](#run-parameterfiles-parameterfilepath)

(run-parameterfiles-parameterfile)=
#### `ParameterFile`

The `ParameterFile` attribute should be a string containing the text contents of the primary parameter file.
If that is not an applicable concept for the simulation code, the field should be the text "N/D".
If the file is not available (e.g. not found, unparseable, etc.), the field should be the text "N/A".

(run-parameterfiles-parameterfilepath)=
#### `ParameterFilePath`

The `ParameterFilePath` attribute should be a string containing the absolute file path of the parameter file or an empty string if it does not exist. 
