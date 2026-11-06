<p align="center"><img src="legend/ZONA_GDC_legend_EN.png" width="720" alt="ZONA GDC legend"></p>

# ZONA GDC — exposure guidance monitoring LUTs

**Languages:** English · [Română](README.ro.md) · [Español](README.es.md) · Website: <https://gordas.dev/zona-gdc/> · Companion project: [ETTR GDC](https://github.com/gordasgdc/ettr-gdc) (log → log compensation LUTs)

[![Licence: CC BY 4.0](https://img.shields.io/badge/licence-CC%20BY%204.0-blue-blue)](LICENSE)

ZONA GDC is a set of 33×33×33 `.cube` LUTs for **monitoring only**. Load one on a monitor, viewfinder or external recorder preview that receives the camera's log signal; the LUT shows a *diagnostic* false-colour map of scene exposure in stops from 18 % grey. It is an exposure aid, **not a look and not a colour correction**.

## Contract
- **Input:** the log profile named in the file (e.g. `VLog-VG` = V-Log / V-Gamut), full-range, no other transform applied.
- **Output:** diagnostic false-colour map for the monitor, full range, no further transform needed. It is **not** log → log (that is ETTR GDC).
- Apply it **once**. If the monitor or camera already applies a LUT/transform, switch that off or you get a double transform.
- Monitoring only: do not use it to grade, and do not bake it into the main recording on purpose. A `.cube` cannot enforce "monitor only"; depending on the device's routing, a monitoring LUT may also appear in recorded external outputs — check your device.

## What the colours mean
The map is computed **directly from the camera log signal**: each channel is decoded to scene-linear with the profile's own curve, luminance is taken with the profile's gamut weights, and the result is expressed in **stops from 18 % grey after the monitoring compensation**. No Rec.709 conversion, tone mapping or clipping happens before the analysis; the output colours are diagnostic and need no further transform.

One colour per whole stop (band *n* = *n* ± 0.5 stops). Same ladder for every profile — see the legend image:

| Stops | Colour | | Stops | Colour |
|---|---|---|---|---|
| ≥ +6.5 | pale cyan | | −1 | pale green-cyan |
| +6 | white | | −2 | mint |
| +5 | pale yellow | | −3 | cyan |
| +4 | magenta | | −4 | azure |
| +3 | orange | | −5 | blue |
| +2 | yellow | | −6 | indigo |
| **+1** | **pink** — around the skin tonal reference (a tonal level, not a skin detector) | | ≤ −6.5 | violet |
| **0** | **green** — grey card | | | |

Two more marks: **dark grey** = below the range this profile can resolve on a 33³ grid (or no usable signal); **red** = the *original* log code is ≥ 31/32 on any channel — a level of the encoding, **not** a sensor clip (sensor limits cannot be deduced from the curve name; the red mark ignores the compensation, so it does not disappear when you darken the picture).

## Compensation (file name `…_MONITOR-<step>EV.cube`)
`0EV` analyses the image as it is. `m1EV` analyses it after a −1 stop darkening: grey captured at +1 stop falls on the grey reference. Same for `m0_5EV` (−0.5) and `m1_5EV` (−1.5). No +0.5 EV in this release.

## Measured limits (33³, interpolated — `INDEX.md`, `audit.json`)
> **Warning — saturated colours.** The map follows *luminance*. Very saturated objects (especially dark, blue-dominant ones) can have a band edge shifted by up to about **1 stop**, and in wide gamuts a saturated blue can have zero or negative luminance and then shows as dark grey. Neutral and skin-like content is the reliable use. Do not read the 0.2–0.4-stop neutral figures below as precision for saturated colours.

- **Whole stops, not half stops.** Grid nodes are 0.3–0.55 stop apart along the neutral axis, so 0.5-stop bands cannot be placed reliably on a 33³ LUT.
- **Neutral band edges** (worst case over all 28 profiles and 4 compensations, 0.01-stop ramps): tetrahedral ≤ 0.44 stop, trilinear ≤ 0.29 stop.
- **Shadows.** Each profile has a *resolved floor* (`INDEX.md`): between roughly −1.6 and −5.2 stops at 0 EV the node spacing exceeds 0.7 stop and edges cannot be placed; darker areas are shown dark grey, never as a wrong colour. Compensation moves the floor by the same number of stops.
- **Saturated colours** (64 test colours, local band-edge shift versus the analytic model): 99 % of cases within 0.54 stop in the worst profile, ≤ 0.6 % of cases above 1 stop; the largest values reach the 1.5-stop search window (so "at least 1.5"). The earlier release note "≈ 7 stops" was a measurement artefact of the old audit (out-of-range colours, nearest-crossing matching) and is withdrawn.
- **Real footage** (Panasonic V-Log, 50 fps, two clips, local tests only): see `CHANGELOG.md`.
- Pointwise 8-bit error is large at band edges by construction. Not tested on physical monitors, viewfinders or recorders; thresholds are not guaranteed on hardware that re-samples or applies its own interpolation. No equivalence with any native exposure tool is claimed.

## Contents
28 profiles by brand (Sony, Canon, Panasonic, ARRI, RED, Blackmagic, Nikon, Fujifilm, Apple, FilmLight, DaVinci, ACES), 4 LUTs each; `Sony/_Viewfinder_6char/` has short-name copies for viewfinders with 6-character file names. `INDEX.csv/md`, `STATS.json`, `catalog.json`, `audit.json`, `MANIFEST_SHA256.txt`, legend images RO/EN/ES. Not included: GoPro Protune (no verified gamut source).

## Licence and attribution

The pre-generated LUTs and the documentation in this distribution are licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)** — https://creativecommons.org/licenses/by/4.0/ (`LICENSE`). You may use, copy, modify and redistribute them, including commercially, **as long as you credit “Dumitru Cristinel Gordas — ZONA GDC”, link the licence and indicate if you made changes.** Third-party components and provenance: `docs/PROVENANCE.md`. Independent project, not affiliated with or endorsed by any camera or software manufacturer; brand names only identify the formats they publish.
