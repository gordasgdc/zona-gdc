# Changelog

## 2.0.0 — 2026-11-06
**The LUTs changed — new files, new hashes. Do not mix with 1.0.0.**
- **New map:** one colour per whole stop of scene luminance from 18 % grey (−7 … +7, open-ended outside), computed directly from the camera log signal after the monitoring compensation. The 1.0.0 four-band scheme (skin / grey / "display white" / deep) and its Rec.709-level definitions are replaced; there is no Rec.709 conversion, tone mapping or clipping before the analysis. Same 28 profiles, same compensations (0 / −0.5 / −1 / −1.5 EV), same file names.
- **Honest shadows:** each profile has a resolved floor (a 33³ grid cannot place band edges where neighbouring nodes are more than 0.7 stop apart); darker areas are shown dark grey instead of a wrong colour. See `INDEX.md`.
- **Red mark** now documented as a level of the encoding (original code ≥ 31/32), not a sensor clip.
- **Corrected precision statement.** 1.0.0 reported saturated-colour band edges displaced by "≈ 7 stops"; that was a measurement artefact of the old audit. New audit (local band-edge shift versus the analytic model, 64 test colours, trilinear and tetrahedral): neutral edges ≤ 0.44 stop; saturated colours p99 ≤ 0.54 stop, ≤ 0.6 % of cases above 1 stop, largest values at the 1.5-stop search limit (dark, saturated, blue-dominant colours). Warning added to the README.
- **Real footage check** (50 fps V-Log, two clips, 744 frames, all four compensations, local only): band-edge shift p50 ≈ 0.015, p99 ≤ 0.27, maximum 0.49 stop, no sample above 0.5 stop; 0.1–0.7 % of pixels fell below the resolved floor, none at the top code.
- Half-stop bands are not offered: they do not fit a 33³ grid (node spacing 0.3–0.55 stop).
- New legend images (RO/EN/ES) and synthetic V-Log examples. Folder icons unchanged.

## 1.0.0 — 2026-11-06
Superseded by 2.0.0 (the saturated-colour precision statement in its README was wrong and its four-band map is replaced). First public release: 28 log profiles, 112 monitoring LUTs (33³ `.cube`, compensation 0 / −0.5 / −1 / −1.5 EV) + 12 Sony viewfinder short-name copies = 124 `.cube` files. Standalone generator (Python standard library), interpolation audit (trilinear and tetrahedral) and tests, RO/EN/ES documentation and legend images, portable and macOS-icons archives with SHA-256 checksums. 4 profiles are labelled experimental (see `INDEX.md`).
