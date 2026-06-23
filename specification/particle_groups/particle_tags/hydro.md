---
short_title: Hydro
---
(tag-hydro)=
# Hydrodynamical

Tag: `Hydro`

Includes:  [`Massive`](#tag-massive)

Particles that are being evolved hydrodynamically.
Generally, these particles map to some sort of volume element and are not simply point particles.

| Name             | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| InternalEnergies | Particle-specific internal energy per unit mass                          |
| Densities        | Particle-specific density at this coordinate position                    |
| KernelLengths    | Kernel length for resolution elements, e.g. the smoothing length for SPH |