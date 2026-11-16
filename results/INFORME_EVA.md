# AREO EVA — Informe de análisis de ruta (borrador nocturno)
**Proyecto:** Plan a Mars Walk — NASA Space Apps Challenge
**Autora:** Christell García (carné 24958) · Análisis asistido por Claude
**Fecha de análisis:** 2026-11-15 (madrugada)

## 1. Zona de misión
- **Ubicación:** Borde occidental del cráter Jezero, Marte (zona Neretva Vallis / muralla oeste), dentro del mosaico **MSR TRN HiRISE v003 (USGS, ago-2024)**.
- **AOI:** 6.0 × 6.5 km. Esquina sup-izq (4,571,000 E; 1,085,500 N), proyección Equirectangular Marte (esfera Mars_2000, R=3,396,190 m, lat. escala verdadera 0°), metros. Centro aprox: 18.27°N, 77.15°E.
- **Justificación científica:** un **cráter fresco de ~2 km** de diámetro actúa como "perforación natural" que expone el subsuelo del terreno antiguo del rim de Jezero. El objetivo B se ubica en el borde seguro de su manto de ejecta: muestreo de bloques excavados de profundidad sin entrar en la cavidad (intransitable).

## 2. Datos utilizados (4 tipos, 3 instrumentos — cumple "≥3 capas")
| Capa | Fuente | Resolución | Rol |
|---|---|---|---|
| DTM (topografía) | MRO HiRISE — mosaico MSR TRN USGS | 1 m/px | pendiente, rugosidad, ruta |
| Ortomosaico (óptica) | MRO HiRISE | 0.25 m/px | base visual, QA de obstáculos |
| IR térmico día/noche | Mars Odyssey THEMIS (mosaicos controlados v2) | 100 m/px | proxy de firmeza del suelo (inercia térmica) |
| FOM Confidence | USGS (calidad del DTM) | 1 m/px | píxeles no confiables = riesgo |

## 3. Parámetros de diseño aplicados
- Pendiente máx. transitable **15%** (absoluta, NoData en el costo) + **zona de precaución 12–15%** (penalización ×2.5 en planificación).
- Pendiente calculada con línea base de 3 m (escala de zancada; evita ruido de píxel del DTM).
- Rugosidad RMS (ventana 5 m) como proxy de campos de bloques sub-píxel (obstáculos >40 cm) — a validar visualmente sobre la orto de 25 cm.
- Velocidad: 2.5 km/h en plano, decae tipo Tobler: v = 2.5·e^(−4·s) km/h.
- Costo (min/m) = (1/v)·(1 + 0.3·R_norm + 0.2·(1−firmeza_THEMIS) + 1.0·[conf<10]).
- Walk-back limit: 3 km de radio desde A (verificado).
- Ruta por **Least Cost Path** (equivalente a r.cost/r.drain; algoritmo MCP geométrico, 8-conectado).

## 4. Resultados
- **A (Base):** (4,573,123 E; 1,080,942 N) — llanura con pendiente 1.0%, >25 m de radio libre de obstáculos. z = −2,032 m.
- **B (Objetivo científico):** (4,574,762 E; 1,083,117 N) — borde SW del ejecta del cráter fresco, pendiente local 7.9%, a 950 m del centro del cráter. z = −1,924 m.
- **Ruta:** 3,476 m (3D), **123 min ida** (~4.1 h ida y vuelta), ascenso +137 m.
- Pendiente media 6.3%, máxima 14.9%; solo **1%** de la ruta en zona de precaución (12–15%).
- Radio máximo desde A: 2,723 m ✓ (< 3,000 m).
- Transitabilidad del AOI: 72% (<15%); componente conectado principal: 69%.
- Alcanzable en ≤60 min desde A: ~5.2 km².

### Tabla de tiempos (ida)
| Punto | Dist (m) | t (min) | z (m) |
|---|---|---|---|
| A | 0 | 0 | −2032 |
| W20 | 578 | 20 | −2008 |
| W40 | 1,124 | 40 | −1976 |
| W60 | 1,644 | 60 | −1974 |
| W80 | 2,136 | 80 | −1934 |
| W100 | 2,768 | 100 | −1935 |
| W120 | 3,395 | 120 | −1931 |
| B | 3,476 | 123 | −1924 |

Presupuesto EVA sugerido: 123' ida + 60' ciencia en B + 123' regreso ≈ **5 h 10 min** (margen OK para EVA de 6–8 h tipo Apolo/Artemis).

## 5. Archivos generados
- `02_procesado/`: dtm/orto/conf del AOI, THEMIS recortados, `slope_3m_pct.tif`, `roughness_rms_5m.tif`, `hillshade_1m.tif`, `mask_transitable.tif`, `cost_min_per_m.tif`, `cumtime_min_desde_A.tif` (base de isócronas).
- `03_resultados/`: `ruta_eva.geojson`, `puntos_eva.geojson` (A, B, waypoints c/20 min), `isocronas.geojson` (15/30/60/90/120 min), `walkback_3km.geojson`, `mapa_mision.png`, `perfil_ruta.png`, `tabla_tiempos.csv`, este informe.

## 6. Pendiente para la sesión conjunta
1. Revisar/ajustar A y B (tú decides; re-corro la ruta en minutos).
2. Curvas de nivel (2–5 m) y simbología final en QGIS.
3. Validación visual de la ruta sobre la orto 25 cm (bloques >40 cm).
4. qgis2web (mapa interactivo) + mockup HUD en Canva.
5. Citar fuentes: USGS/DOI 10.5066/P13CPYYU (CC0), THEMIS mosaics, NASA/JPL/UArizona.

## Advertencias honestas
- La rugosidad a 1 m NO detecta rocas de 40 cm individualmente (sub-píxel): es proxy estadístico; la verificación fina va sobre la orto de 25 cm en los 3.5 km de ruta.
- THEMIS a 100 m es contexto regional de firmeza, no detalle local.
- El DTM puede contener artefactos (cajas, costuras CCD) documentados por USGS; el raster FOM ya los penaliza.
