# Provenance

Copyright © 2026 Dumitru Cristinel Gordas. Licence of the distributed files: see `../LICENSE`.

## What is distributed
- The pre-generated `.cube` LUTs, `INDEX.*`, `STATS.json`, `catalog.json`, `audit.json` (measurement results), documentation, legend images and folder icons. The tools used to produce them are not part of this distribution.
- Band thresholds, colours and the BT.709-based skin/grey reference levels are working conventions of this project, not a published standard.
- The log curves are implemented from each format owner's public document (constants are published facts); the same curves are used by the companion project ETTR GDC.
- Luminance weights are computed from the published primaries and white points of each gamut; they were cross-checked against the Colour library (BSD-3-Clause), used offline only — nothing from it is included. N-Gamut and F-Gamut use Rec.2020 primaries as in the manufacturers' documents.
- Folder icons and legend images: own typographic design; typeface Inter (SIL OFL 1.1) used for rendered glyphs only, font files not distributed. No manufacturer logo or brand asset is used; no affiliation is implied.
- No third-party footage or images. Example images use synthetic charts only.

## Known limits
GoPro Protune is not included (no verified gamut source). See README for precision and hardware limits.
