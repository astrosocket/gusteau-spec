---
short_title: Reordered
---
(tag-reordered)=
# Reordered Particles

Tag: `Reordered`

Includes:  [`Particles`](#tag-particles)

Tag-Description: Particles that have been reordered from simulation output.

This tag should be used when the particle ordering has been changed from the original snapshot ordering, regardless of the actual process.

## Attributes

| Name            | Description                                                                                                     |
| --------------- | --------------------------------------------------------------------------------------------------------------- |
| Reordering_info | The manner of, and reason for, reordering, for example: "Spatial reordering via z-order curve by packingcubes". |

## Datasets

| Name            | Description                            |
| --------------- | -------------------------------------- |
| OriginalIndices | The original indices of the particles. |
