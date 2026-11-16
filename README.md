### AI Disclosure & Transparency
A portion of the file structuring, documentation support, and repository setup for this project was assisted by **Claude (Anthropic)**. All content, design choices, final logic, and validation were thoroughly reviewed, directed, and curated by Christell García.

# AREO EVA — Plan a Mars Walk
**Team MISHEK · NASA Space Apps Challenge 2026 · Universidad del Valle de Guatemala**
**Live interactive mission map:** open the GitHub Pages site of this repo (or `index.html` locally).

AREO EVA is a hyperlocal mission-planning map for the first Marswalks: a complete, safety-driven EVA route on the **western rim of Jezero Crater**, built in **QGIS** exclusively from real NASA data.

## The mission
- **A (base):** flat plain, slope 1.0% — **B (science target):** ejecta blanket of a fresh ~2 km crater, a *natural drill hole* exposing Jezero's ancient subsurface.
- **Route:** 3,476 m · 123 min one way · +137 m climb · max slope 14.9% (hard limit 15%) · walk-back radius 2,723 m < 3 km ✓ · full EVA ≈ 5 h 10 min.

## Method (reproducible)
Slope (Horn, 3 m baseline) + RMS roughness (5 m) + THEMIS night-IR soil firmness + USGS DTM confidence → fused into a **walking-time cost surface** (Tobler-type speed adapted to a suited astronaut, 2.5 km/h flat) → **Least Cost Path** (r.cost/r.drain equivalent) → 15–120 min isochrones and walk-back envelope. Full methodology in [`report_eva.pdf`](report_eva.pdf) (Spanish).

## Repository contents
| Path | Content |
|---|---|
| `index.html` + `assets/` | Interactive web map (Leaflet; AI-generated code, see disclosure) |
| `report/` | Technical report (PDF + LaTeX source) |
| `results/` | Mission map, route profile, helmet HUD, route/waypoints/isochrones GeoJSON, timing table |
| `docs_submission.md` | Space Apps submission texts |

Raw NASA rasters (~40 GB) are not hosted here; download them from the official sources below.

## Data (all real, none invented)
- **MSR Terrain Relative Navigation HiRISE DTM & Orthoimage Mosaics** — USGS/NASA, CC0 — https://doi.org/10.5066/P13CPYYU
- **NASA/USGS Controlled THEMIS Mosaics (100 m)** — https://doi.org/10.5066/P96FA04Z
- **MRO CRISM MTRDR FRT00005850** — NASA PDS Geosciences Node — https://ode.rsl.wustl.edu/mars/
- HiRISE: NASA/JPL-Caltech/University of Arizona — https://www.uahirise.org

## AI (SI) use disclosure
- **AI-generated (Claude, Anthropic):** the web map code (`index.html`, `assets/data.js`) and the helmet HUD mockup (`results/hud_base.png`, visibly watermarked).
- **Human work (Team MISHEK):** data acquisition, QGIS processing and methodology, parameter design, verification, and all mission decisions.

## Team
- Christell García — Team MISHEK, Universidad del Valle de Guatemala, Facultad de ING Civil.
- Ian Castellanos — Team MISHEK, Universidad del Valle de Guatemala, Facultad CCHH Matemática Aplicada.
