(tag-chemistry)=
# Chemistry

Includes:  [`Massive`](#tag-massive)[^mass-frac]

Particles with an internal state that represents some form of "chemistry".
For consistancy, tags in the chemistry group **must pick one and only one** of [](#tag-chem-abundance), [](#tag-chem-mass) [](#tag-chem-mass-frac), or [](#tag-chem-number) to represent chemical quantities for inclusion.

Thus an example tag set could be `["Abundance", "Hydrogenic", "Metallic"]` to represent [abundance-based](#tag-chem-abundance), [metallic](#tag-chem-metallic) particle chemistry.

[^mass-frac]: Only included if [](#tag-chem-mass-frac) or [](#tag-chem-mass) is included.