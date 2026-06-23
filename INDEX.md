# Project GUSTEAU

Specification for the **G**rand **U**nified **S**napshot **T**hat **E**veryone **A**grees **U**pon.

Version: 0.1.0

(index-abstract)=
## Abstract
GUSTEAU aims to provide a common, unifying snapshot format for particle-based
simulation codes. Specialized for use in astronomical and astrophysical
contexts, it is designed to be a self-describing format that enhances analysis,
simulation reproducibility, and, most importantly, data interopability. 

(index-description)=
## Description
GUSTEAU snapshots are HDF5 files with standardized datasets and attributes, agnostic to the simulation code that generated them. The specification includes a small collection of required fields (specifically attributes under the `/Header` group), a larger number of "best-effort" fields, and a composable framework of "tags" for indicating particle data that provide guarantees for what fields are available. Further, particle datasets fields include unit information as well as comoving <--> physical and "little $h$" transforms. 

The specification is designed to be easily extendable and backwards-compatible: GUSTEAU snapshots should be readable by common analysis packages (e.g. [pynbody](https://github.com/pynbody/pynbody), [swiftsimio](https://github.com/SWIFTSIM/swiftsimio), [yt](https://yt-project.org/)) roughly out of the box, regardless of the specification version or customizations. Particle datasets are defined by "tags", similar to `python`'s [protocols](https://typing.python.org/en/latest/spec/protocol.html), where a tag defines a set of named fields with defined meaning. Particle types can thus be defined on-the-fly, with no limit on the number of types, easing analysis tasks like visualization or spectral analysis. For example, a visualization tool could define a function for displaying `SPHParticles`, discriminating between `Stars`, `DarkMatter`, `Neutrinos`, etc., for a snapshot that contains `BulgeMainSequence`, `WhiteDwarfs`, `BlueGiants`, `SIDM`, `CDM`, `DarkStars`, and other types, without needing to know how to read possible additional fields.  New or custom tags are also easy to define, but not required. GUSTEAU does not prohibit fields: we set the floor, not the ceiling!

The names and meanings of the fields are community-driven, and it's easy to [propose new tags](https://github.com/astrosocket/gusteau-spec/issues/new?assignees=&labels=&projects=&template=01-tag-proposal.md&title=) or suggest [missing groups/attributes](https://github.com/astrosocket/gusteau-spec/issues/new?assignees=&labels=add-missing&projects=&template=02-add-missing.md&title=).


(index-aims)=
## Aims

* Universally readable (use HDF5)
* Simulation software (ie. GADGET/GIZMO/AREPO/Swift/etc.) agnostic
* Simulation _type_ (cosmological vs physical, whole-box vs zoom-in, 2D vs 3D, etc) agnostic 
* Easily/simply configurable/extendable
    * Adding/modifying a [](#fields) or [](#particle-groups-tags) should be easy for a non-coder to do
    * Adding/modifying a {term}`translation` should be easy for a simulation software developer to do
* Self-describing
    * Names should be meaningful and standardized
    * All `Dataset`s have metadata, including a description of the dataset at minimum
    * All fields (not just datasets) should be unit and cosmological (presence of little $h$/scale-factor $a$) aware if meaningful/possible
* Facilitate simulation reproducibility - provide all available information about how simulation was run
* Backwards compatability --> should not need new software to read a GUSTEAU snapshot.


(index-see-also)=
## See Also



See also our companion projects, [gusteau-translate](github.com/astrosocket/gusteau-translate) and [packingcubes](packingcubes.readthedocs.io)!