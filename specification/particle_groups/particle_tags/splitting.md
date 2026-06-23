---
short_title: Merge-split
---
(tag-merge-split)=
# Splittable/Mergeable Particles

Tag: `Merge-split`

Includes: [`Particles`](#tag-particles)

Particles that undergo splitting and merging.

For the purpose here, it does not matter exactly what it means to be the "original" particle vs "new" particle, but as an example, the "original" particle would be the one that kept the `ParticleID` while the "new" particle received a new ID.

| Name                  | Description                                                                                                                                                                                                                                                                                                                        |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SplitCounts           | Number of times this particle has been split, including splits when this particle may have been a different type (e.g. conversion from hydro particle into sink)                                                                                                                                                                   |
| SplitTrees            | Binary tree describing splitting events. The "original" particle has a value of zero for that splitting event, the "new" particle has a value of one.                                                                                                                                                                              |
| ProgenitorParticleIDs | ID of the progenitor of this particle. If this particle is the result of one (or many) splitting events, this ID corresponds to the ID of the particle in the initial conditions that its lineage can be traced back to. If the particle was never split, this is the same as the `ParticleIDs` dataset under the `Particles` tag. |
