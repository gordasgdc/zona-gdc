<p align="center"><img src="legend/ZONA_GDC_legend_RO.png" width="720" alt="Legenda ZONA GDC"></p>

# ZONA GDC — LUT-uri de monitorizare pentru ghidaj de expunere

**Limbi:** [English](README.md) · Română · [Español](README.es.md) · Site: <https://gordas.dev/zona-gdc/> · Proiect însoțitor: [ETTR GDC](https://github.com/gordasgdc/ettr-gdc) (LUT-uri de compensare log → log)

[![Licență: CC BY 4.0](https://img.shields.io/badge/licence-CC%20BY%204.0-blue-blue)](LICENSE)

ZONA GDC este un set de LUT-uri `.cube` 33×33×33 **doar pentru monitorizare**. Se încarcă pe un monitor, vizor sau previzualizare de recorder extern care primește semnalul log al camerei; LUT-ul arată o hartă *diagnostică* în fals-culori a expunerii de scenă, în trepte față de grey 18%. Este un ajutor de expunere, **nu un look și nu o corecție de culoare**.

## Contract
- **Intrare:** profilul log din numele fișierului (ex. `VLog-VG` = V-Log / V-Gamut), full range, fără altă transformare aplicată.
- **Ieșire:** hartă diagnostică în fals-culori pentru monitor, full range, fără altă transformare. **Nu** este log → log (asta face ETTR GDC).
- Aplică-l **o singură dată**. Dacă monitorul sau camera aplică deja un LUT/transformare, oprește-o, altfel ai dublă transformare.
- Doar monitorizare: nu îl folosi pentru etalonare și nu îl „arde" intenționat în înregistrarea principală. Un `.cube` nu poate impune „doar monitor"; în funcție de rutarea dispozitivului, un LUT de monitorizare poate apărea și în ieșirile externe înregistrate — verifică dispozitivul.

## Ce înseamnă culorile
Harta se calculează **direct din semnalul log al camerei**: fiecare canal e decodat în scene-linear cu curba profilului, luminanța se ia cu ponderile gamutului profilului, iar rezultatul e exprimat în **trepte față de grey 18% după compensarea de monitorizare**. Nu există conversie Rec.709, tone mapping sau tăiere înaintea analizei; culorile de ieșire sunt diagnostice și nu cer altă transformare.

O culoare pe treaptă întreagă (banda *n* = *n* ± 0,5 trepte). Aceeași scară pentru toate profilele — vezi imaginea legendei:

| Trepte | Culoare | | Trepte | Culoare |
|---|---|---|---|---|
| ≥ +6,5 | cyan pal | | −1 | verde-cyan pal |
| +6 | alb | | −2 | mentă |
| +5 | galben pal | | −3 | cyan |
| +4 | magenta | | −4 | azur |
| +3 | portocaliu | | −5 | albastru |
| +2 | galben | | −6 | indigo |
| **+1** | **roz** — în jurul referinței tonale pentru piele (nivel tonal, nu detector de piele) | | ≤ −6,5 | violet |
| **0** | **verde** — grey card | | | |

Încă două marcaje: **gri închis** = sub domeniul pe care profilul îl poate rezolva pe o grilă 33³ (sau fără semnal utilizabil); **roșu** = codul log *original* e ≥ 31/32 pe orice canal — un nivel al codării, **nu** o tăiere a senzorului (limitele senzorului nu se pot deduce din numele curbei; marcajul roșu ignoră compensarea, deci nu dispare când întunecați imaginea).

## Compensare (nume fișier `…_MONITOR-<pas>EV.cube`)
`0EV` analizează imaginea ca atare. `m1EV` o analizează după o întunecare de −1 treaptă: grey capturat la +1 treaptă cade pe referința de grey. La fel `m0_5EV` (−0,5) și `m1_5EV` (−1,5). Fără +0,5 EV în această versiune.

## Limite măsurate (33³, interpolat — `INDEX.md`, `audit.json`)
> **Avertisment — culori saturate.** Harta urmează *luminanța*. Obiectele foarte saturate (mai ales întunecate, dominant albastre) pot avea o margine de bandă decalată cu până la circa **1 treaptă**, iar în gamuturi largi un albastru saturat poate avea luminanță zero sau negativă și apare gri închis. Utilizarea de încredere: conținut neutru și de tip piele. Nu citiți cifrele de 0,2–0,4 trepte de la neutre ca precizie pentru culori saturate.

- **Trepte întregi, nu jumătăți.** Nodurile grilei sunt la 0,3–0,55 trepte pe axa neutră, deci benzi de 0,5 trepte nu pot fi plasate fiabil pe un LUT 33³.
- **Margini de bandă pe neutre** (cel mai rău caz pe 28 de profile și 4 compensări, rampe de 0,01 trepte): tetraedric ≤ 0,44 trepte, trilinear ≤ 0,29.
- **Umbre.** Fiecare profil are un *prag rezolvat* (`INDEX.md`): între aprox. −1,6 și −5,2 trepte la 0 EV, distanța dintre noduri depășește 0,7 trepte și marginile nu pot fi plasate; zonele mai întunecate apar gri închis, niciodată într-o culoare greșită. Compensarea mută pragul cu același număr de trepte.
- **Culori saturate** (64 de culori de test, decalajul local al marginii față de modelul analitic): 99 % din cazuri în 0,54 trepte în cel mai rău profil, ≤ 0,6 % peste 1 treaptă; cele mai mari valori ating fereastra de căutare de 1,5 trepte („cel puțin 1,5"). Nota anterioară „≈ 7 trepte" a fost un artefact de măsurare al auditului vechi (culori în afara domeniului, potrivire pe cea mai apropiată trecere) și este retrasă.
- **Material real** (Panasonic V-Log, 50 fps, două clipuri, doar teste locale): vezi `CHANGELOG.md`.
- Eroarea punctuală pe 8 biți e mare la marginile benzilor prin construcție. Netestat pe monitoare, vizoare sau recordere fizice; pragurile nu sunt garantate pe hardware care re-eșantionează sau folosește propria interpolare. Nu se pretinde echivalență cu vreun instrument nativ de expunere.

## Conținut
28 de profile pe branduri (Sony, Canon, Panasonic, ARRI, RED, Blackmagic, Nikon, Fujifilm, Apple, FilmLight, DaVinci, ACES), câte 4 LUT-uri; `Sony/_Viewfinder_6char/` are copii cu nume scurt pentru vizoare cu nume de fișier de 6 caractere. `INDEX.csv/md`, `STATS.json`, `catalog.json`, `audit.json`, `MANIFEST_SHA256.txt`, imagini de legendă RO/EN/ES. Neincluse: GoPro Protune (fără sursă verificată pentru gamă).

## Licență și atribuire

LUT-urile pregenerate și documentația din această distribuție sunt licențiate sub **Creative Commons Atribuire 4.0 Internațional (CC BY 4.0)** — https://creativecommons.org/licenses/by/4.0/deed.ro (`LICENSE`). Le poți folosi, copia, modifica și redistribui, inclusiv comercial, **cu condiția să menționezi „Dumitru Cristinel Gordas — ZONA GDC”, să oferi linkul licenței și să indici dacă ai făcut modificări.** Componente terțe și proveniență: `docs/PROVENANCE.md`. Proiect independent, fără afiliere sau susținere din partea vreunui producător de camere sau software; numele de brand identifică doar formatele pe care le publică.
