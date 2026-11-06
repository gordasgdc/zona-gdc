# ZONA GDC - profile index

28 profiles, 112 LUTs in profile folders + 12 Sony viewfinder copies. Verified: 28, experimental: 0.

Map: one colour per whole stop of scene luminance from 18 % grey (compensated). *Resolved from* = lowest stop at 0 EV compensation (shifts by the compensation) that a 33^3 grid can place band edges for; darker is drawn dark grey. *Encoding reaches* = stops above grey at code 1.0 (a property of the log curve, NOT the sensor limit). Misalignment = local shift of a band edge in stops, interpolated LUT vs analytic model, worst case over the 4 compensations, 64 colours for 'saturated'. *verified* = neutral band edges within 0.5 stop (tetrahedral and trilinear) inside the resolved range; it says nothing about saturated colours (see README warning).

| Brand | Profile (folder) | Gamut | Status | Resolved from (stops, 0 EV) | Encoding reaches (stops, 0 EV) | Neutral misalignment, tetra / trilinear | Saturated p99, tetra | Note |
|---|---|---|---|---|---|---|---|---|
| Sony | `S-Log2_S-Gamut` | S-Gamut | verified | -2.8 | +6.3 | 0.37 / 0.28 | 0.25 |  |
| Sony | `S-Log3_S-Gamut3.Cine` | S-Gamut3.Cine | verified | -4.2 | +7.7 | 0.44 / 0.19 | 0.52 |  |
| Sony | `S-Log3_S-Gamut3` | S-Gamut3 | verified | -4.2 | +7.7 | 0.44 / 0.17 | 0.18 |  |
| Canon | `Canon-Log_Cinema-Gamut` | Cinema Gamut | verified | -1.6 | +5.5 | 0.34 / 0.29 | 0.18 |  |
| Canon | `Canon-Log2_Cinema-Gamut` | Cinema Gamut | verified | -3.4 | +8.5 | 0.33 / 0.27 | 0.29 |  |
| Canon | `Canon-Log3_Cinema-Gamut` | Cinema Gamut | verified | -1.7 | +6.5 | 0.36 / 0.23 | 0.22 |  |
| Panasonic | `V-Log_V-Gamut` | V-Gamut | verified | -4.0 | +8.0 | 0.35 / 0.27 | 0.31 |  |
| ARRI | `LogC3_AWG3_EI0160` | ARRI Wide Gamut 3 | verified | -3.2 | +7.6 | 0.42 / 0.23 | 0.22 |  |
| ARRI | `LogC3_AWG3_EI0200` | ARRI Wide Gamut 3 | verified | -3.2 | +7.7 | 0.41 / 0.22 | 0.24 |  |
| ARRI | `LogC3_AWG3_EI0250` | ARRI Wide Gamut 3 | verified | -3.2 | +7.8 | 0.41 / 0.22 | 0.25 |  |
| ARRI | `LogC3_AWG3_EI0320` | ARRI Wide Gamut 3 | verified | -3.2 | +7.9 | 0.40 / 0.22 | 0.24 |  |
| ARRI | `LogC3_AWG3_EI0400` | ARRI Wide Gamut 3 | verified | -3.2 | +8.0 | 0.40 / 0.21 | 0.23 |  |
| ARRI | `LogC3_AWG3_EI0500` | ARRI Wide Gamut 3 | verified | -3.2 | +8.1 | 0.37 / 0.22 | 0.23 |  |
| ARRI | `LogC3_AWG3_EI0640` | ARRI Wide Gamut 3 | verified | -3.9 | +8.2 | 0.35 / 0.29 | 0.30 |  |
| ARRI | `LogC3_AWG3_EI0800` | ARRI Wide Gamut 3 | verified | -3.9 | +8.3 | 0.34 / 0.28 | 0.29 |  |
| ARRI | `LogC3_AWG3_EI1000` | ARRI Wide Gamut 3 | verified | -3.9 | +8.3 | 0.33 / 0.27 | 0.26 |  |
| ARRI | `LogC3_AWG3_EI1280` | ARRI Wide Gamut 3 | verified | -3.9 | +8.5 | 0.31 / 0.26 | 0.25 |  |
| ARRI | `LogC3_AWG3_EI1600` | ARRI Wide Gamut 3 | verified | -3.9 | +8.6 | 0.31 / 0.25 | 0.25 |  |
| ARRI | `LogC4_AWG4` | ARRI Wide Gamut 4 | verified | -1.8 | +11.3 | 0.36 / 0.27 | 0.54 |  |
| RED | `Log3G10_REDWideGamutRGB` | REDWideGamutRGB | verified | -2.7 | +10.0 | 0.44 / 0.27 | 0.30 |  |
| Blackmagic | `Film-Gen5_BMD-WG-Gen5` | Blackmagic Wide Gamut Gen5 | verified | -3.7 | +10.3 | 0.42 / 0.24 | 0.48 |  |
| Nikon | `N-Log_N-Gamut` | N-Gamut (Rec.2020 primaries) | verified | -2.4 | +6.4 | 0.36 / 0.22 | 0.25 |  |
| Fujifilm | `F-Log_F-Gamut` | F-Gamut (Rec.2020 primaries) | verified | -3.6 | +5.3 | 0.34 / 0.18 | 0.17 |  |
| Fujifilm | `F-Log2_F-Gamut` | F-Gamut (Rec.2020 primaries) | verified | -3.4 | +8.3 | 0.33 / 0.20 | 0.22 |  |
| Apple | `Apple-Log_Rec2020` | Rec.2020 | verified | -3.9 | +6.1 | 0.30 / 0.19 | 0.22 |  |
| FilmLight | `T-Log_E-Gamut` | E-Gamut | verified | -3.7 | +9.5 | 0.43 / 0.23 | 0.42 |  |
| DaVinci | `DaVinci-Intermediate_DWG` | DaVinci Wide Gamut | verified | -4.0 | +9.1 | 0.32 / 0.28 | 0.33 |  |
| ACES | `ACEScct_AP1` | ACES AP1 | verified | -5.2 | +10.3 | 0.36 / 0.16 | 0.19 |  |
