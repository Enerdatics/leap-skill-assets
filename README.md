# leap-skill-assets

Static files that Enerdatics' Leap skills load at runtime from jsDelivr.

| File | Used by | Loaded as |
|---|---|---|
| `criteria-form.js` | `developer-targets` skill, Step 1 criteria form | `https://cdn.jsdelivr.net/gh/Enerdatics/leap-skill-assets@criteria-form-<version>/criteria-form.js` with a `sha384` Subresource Integrity hash |
| `gis-map-form.js` | `gis-map` skill, Step 1 criteria form | `https://cdn.jsdelivr.net/gh/Enerdatics/leap-skill-assets@gis-map-form-<version>/gis-map-form.js` with a `sha384` Subresource Integrity hash |
| `gis-layers/` | `gis-map` skill, public map overlays (transmission lines, state boundaries) | `https://cdn.jsdelivr.net/gh/Enerdatics/leap-skill-assets@<commit>/gis-layers/index.json`, pinned by commit and checked by sha256 |

- **Generated, do not edit.** Each file is built in Enerdatics' private skills repository and copied here byte for byte.
  Any edited byte breaks the integrity hash and the skill refuses the file.
- **Versions are tags or commits** (`criteria-form-v3`, …). A published tag is never moved or deleted, so a skill that pins it keeps working.
- The form files contain form code, option lists and brand assets only: no data, credentials or user information.
- `gis-layers/` holds public-domain U.S. Government map data, modified by Enerdatics. Its licences are in
  `gis-layers/NOTICE` and `gis-layers/README.md`; the copyright line below does not apply to those data files.

© Enerdatics. All rights reserved, except the data files in `gis-layers/` (see `gis-layers/NOTICE`).
