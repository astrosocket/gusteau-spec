---
short_title: Transform
---
(tag-transform)=
# Transformed Particles

Tag: `Transform`

Includes: [`Particles`](#tag-particles)

Particles that transition between particle types.

Examples include gas collapsing into star or other sink particle, stars moving along the stellar evolution track, compact object formation.

For the purpose here, it does not matter how or why the particle transformed.

| Name                 | Description                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------- |
| TransformTimes       | Time of the most recent particle type transformation.                                    |
| PreviousParticleType | Previous particle type as an index into [`/Header.ParticleNames`](#header-particlenames) |
