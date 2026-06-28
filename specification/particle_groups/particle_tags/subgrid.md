---
short_title: Subgrid
---
(tag-subgrid)=
# Subgrid physics

Tag: `Subgrid`

Includes: [`Particles`](#tag-particles)

Tag-Description: Particles with generic subgrid physics

Subgroups: `Subgrid`

Subgroup-Description: This subgroup is the primary location to store miscellaneous subgrid quantities.

Particles with this tag **must** include the subgroup `Subgrid`.

This tag/subgroup is intended as sort of a catch-all for various quantities that do not fit cleanly into one of the other tags/subgroups.
Because this is intended for miscellaneous, highly specific fields, there are no specified datasets or attributes.

This tag also facilitates moving the majority of simulation/subgrid quantities out of the top-level group, leaving predominantly kinematic quantities, if that is of interest.

