---
short_title: Feedback
---
(tag-feedback)=
# Feedback-related Quantities

Tag: `Feedback`

Includes: [`Particles`](#tag-particles), ([`AGN`](#tag-agn)|[`SNII`](#tag-snii) on subgroup)

Tag-Description: Particles affected by various feedback events.

Subgroups: `Feedback`

Subgroup-Description: This subgroup is the primary location to store feedback-related subgrid quantities.

Particles with this tag **must** include the subgroup `Feedback` and specify at least one of [`AGN`](#tag-agn) or [`SNII`](#tag-snii) in the `/../Feedback.tags` attribute, indicating what kind of feedback is present.
The `AGN`/`SNII` groups will then be subgroups of `Feedback`.

While the quantities utilized in feedback-subgrid physics can vary significantly, especially between different feedback sources, **example** datasets are described below. 
None of them are required, but should use the specified name (and naming patterns) if present.

:::{admonition}
:class: attention
If a quantity is shared by multiple feedback types, it should be included at the `Feedback` level.
Otherwise, quantities should be placed under their respective sub-subgroups.
:::

:::{admonition} Other feedback models
:class: dropdown
:class: hint
If the snapshot includes a feedback source besides the above-mentioned models, include it using the same patterns:
 1. Add a subgroup to `Feedback` with a descriptive name (e.g. `SubDimensionCollapse`) and `Description` attribute ("Spillout from sub-dimension collapse")[^scifi]
 2. Add a tag with the same name (`SubDimensionCollapse`) to the `Feedback` subgroup
 3. Add appropriate fields (`/../Feedback/SubDimensionCollapse/Densities_before_last_event`)
 4. Add it to the specification by submitting an [issue](https://github.com/astrosocket/gusteau-spec/issues/new/choose).
:::

[^scifi]: The author has read too many Sci-Fi novels....

## Example Datasets

| Name                        | Description                                                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Densities_at_last_event     | Physical density (not subgrid) of the particle at the last feedback event. -1 if particles have never been affected.                                  |
| Densities_before_last_event | Physical density (not subgrid) of the particle immediately prior to the last feedback event. -1 if particles have never been affected.                |
| AGN/Energies_received       | Total amount of thermal energy from AGN feedback events received by the particles.                                                                    |
| SNII/Heated_by_feedback     | Flags the particles that have been directly hit by an SNII feedback event at some point in the past. If >0, contains the number of individual events. |
| Last_event_scale_factor     | Scale-factors at which the particles were last hit by a feedback event. -1 if a particle has never been hit by feedback                               |

