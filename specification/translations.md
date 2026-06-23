---
abbreviations:
    GUSTEAU: Grand Unified Snapshot That Everyone Agrees Upon

---

(translations)=
# Translations

While the intention is for simulation codes to eventually add GUSTEAU-specified snapshots as an output option, equivalently to how many currently offer GADGET-2's formats 1, 2, and HDF5, in the near term snapshots will need to be _translated_ from their current format to GUSTEAU.
This introduces three concepts:

:::{glossary}
Translating
: Reading in a snapshot in an arbitrary format, converting the fields such that they follow the GUSTEAU specifications, (optionally) running the data through [`packingcubes`](packingcubes.readthedocs.io), and saving to a new file.


Translator
: Program or script to convert snapshots into the GUSTEAU format. 
  Project GUSTEAU is working on [gusteau-translate](https://github.com/astrosocket/gusteau-translate), but simulation developers and third-parties may create their own.


Translation
: Mapping between the fields in a given format and their corresponding GUSTEAU fields.
  This includes any transformation functions, unit definitions, and necessary defaults.

:::

For an example translator and translations, check out [gusteau-translate](https://github.com/astrosocket/gusteau-translate).