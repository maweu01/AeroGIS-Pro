# AeroGIS Pro v4 — Aerial Survey Intelligence Platform

<div align="center">

![AeroGIS Pro](https://img.shields.io/badge/AeroGIS_Pro-v4.0-38bdf8?style=for-the-badge)
![KCAA Compliant](https://img.shields.io/badge/KCAA-LN_182%2F2022_Compliant-22d3a0?style=for-the-badge)
![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-f5a623?style=for-the-badge)
![Single File](https://img.shields.io/badge/Architecture-Single_File_HTML-b48ef8?style=for-the-badge)

**Professional drone survey planning, airspace intelligence, and environmental land-use modelling**  
**for operators, GIS engineers, and county planners working across Kenya and East Africa.**

[⚡ Launch Application](https://maweu01.github.io/AeroGIS-Survey-Planner) · [📖 Documentation](#table-of-contents) · [🐛 Report Bug](https://github.com/maweu01/AeroGIS-Survey-Planner/issues) · [✨ Request Feature](https://github.com/maweu01/AeroGIS-Survey-Planner/issues)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Quick Start](#quick-start)
- [Feature Modules](#feature-modules)
- [Aircraft Database](#aircraft-database)
- [Camera & Sensor Catalogue](#camera--sensor-catalogue)
- [Environmental Planning Lab](#environmental-planning-lab)
- [Export Formats](#export-formats)
- [KCAA Compliance System](#kcaa-compliance-system)
- [Airspace & NFZ Database](#airspace--nfz-database)
- [Weather Integration](#weather-integration)
- [Technology Stack](#technology-stack)
- [Author](#author)

---

## Overview

AeroGIS Pro v4 is a **zero-dependency, single-file HTML application** that delivers a complete aerial survey planning and environmental intelligence platform. No server, no build process, no npm. Open `index.html` in any modern browser and the entire system — interactive maps, drone and sensor databases, KCAA pilot registry, and a 7-step Environmental Planning Lab — is immediately available.

```
index.html        181 KB   Complete application
                  2,122    Lines of code
                    134    JavaScript functions
                      0    npm packages
                      0    Server-side dependencies
```

| Metric | Value |
|---|---|
| Drone Platforms | **16** across 4 categories |
| Camera / Sensors | **13** across 6 spectral types |
| Application Modules | **9** fully integrated |
| Export Formats | **7** GCS and GIS formats |
| JavaScript Functions | **134** ES5 — no transpiler needed |
| npm Dependencies | **0** |
| Server Requirements | **None** |

---

## Quick Start

### Option A — Live Deployment (no setup required)

```
https://maweu01.github.io/AeroGIS-Survey-Planner
```

Open in Chrome, Edge, Firefox, or Safari. No login, no account, no API key required.

### Option B — Run Locally

```bash
# Clone the repository
git clone https://github.com/maweu01/AeroGIS-Survey-Planner
cd AeroGIS-Survey-Planner

# Open directly in browser (all features work via file://)
open index.html

# Or serve over HTTP (recommended for Web Bluetooth BLE)
python3 -m http.server 8080
# Then visit: http://localhost:8080
```

### System Requirements

| Requirement | Detail |
|---|---|
| Browser | Chrome 90+ · Edge 90+ · Firefox 88+ · Safari 15+ |
| Web Bluetooth (BLE) | Chrome / Chromium only |
| Internet connection | Required — tile maps, weather API, Esri DEM, CDN scripts |
| Screen resolution | 1280 × 768 px minimum |
| JavaScript | Must be enabled |
| Node.js / npm | Not required |
| Server runtime | Not required |

### Your First Mission — 5 Steps

1. **Select a survey area** — click a preset shape (Rect / L-Shape / Triangle / Corridor / Circle) in the SURVEY sidebar, or click **Custom Draw** to polygon any area on the map.
2. **Choose platform and sensor** — open the AIRCRAFT sidebar tab, select drone category, model, camera type, and sensor. Specs populate automatically and altitude enforces KCAA class limits.
3. **Set flight parameters** — adjust altitude, FOV, side overlap, forward overlap, and wind direction. Swath width and line spacing update live.
4. **Generate the flight plan** — click **Generate Flight Plan**. Parallel lawnmower flight lines and waypoints appear on the map. The Mission Summary panel shows line count, waypoint count, area (ha), swath width (m), GSD (cm/px), and estimated image count.
5. **Export** — use the Quick Export buttons in the Mission Summary panel, or switch to the **Export** tab for all seven GCS/GIS formats.

---

## Feature Modules

All nine modules share the same Leaflet map canvas and data state. Draw a survey area once — it flows automatically into the flight planner, site assessment engine, change detection module, Environmental Planning Lab, and all export formats.

### ✈ Flight Planner

- Five preset survey shapes: **Rectangle, L-Shape, Triangle, Corridor, Circle**
- Freehand polygon draw via Leaflet Draw — click vertices, double-click to close
- All shapes are fully resizable by dragging Leaflet Draw vertex handles after placement
- Flight parameters: altitude (0–500 m AGL), camera FOV (30–120°), side overlap (50–95%), forward overlap (50–95%), wind direction (0–315°)
- Auto-generates parallel lawnmower flight lines with correct swath spacing and inter-line transit paths
- Mission Summary panel: line count, waypoint count, area (ha), swath (m), GSD (cm/px), estimated image count

### 📐 Coordinate Entry

Five precision input methods, all producing resizable Leaflet Draw polygons:

| Method | Input Format | Use Case |
|---|---|---|
| Point-by-point | Decimal lat / lng per vertex | Manual precision entry |
| Bounding Box | N / S / E / W in decimal degrees | Rectangular AOI from known extents |
| Circle | Centre lat/lng + radius in metres (min 10 m) | Buffer zones, circular survey areas |
| WKT Import | `POLYGON((lng lat, lng lat, ...))` | Paste from any GIS software |
| DMS Converter | `1°17'10.8"S 36°49'2"E` | Convert field GPS coordinates |

### 🏗 Site Assessment

Six automated assessment types that generate a scored suitability report from the drawn survey area:

| Type | Key Output Metrics |
|---|---|
| **Real Estate** | Buildable area (ha), plot yield, infrastructure cost (KSH/ha) |
| **Urban Planning** | Population capacity (persons), road requirement (km), water demand (m³/day) |
| **Solar Feasibility** | Capacity (kWp), annual generation (kWh), annual revenue (KSH) |
| **Flood Risk** | 10-yr and 100-yr return periods, drainage coefficient, mitigation measures |
| **Soil & Agriculture** | Nitisols classification, pH range 5.8–7.2, crop suitability by species |
| **Infrastructure** | Tarmac km, grid proximity (km), 4G coverage availability |

### 🚧 Airspace Intelligence

Pre-loaded Kenya airspace database — see [Airspace & NFZ Database](#airspace--nfz-database). All five zones are rendered on the map as colour-coded radius circles with centroid markers that open info popups when clicked.

### 🔄 Change Detection

Six bi-temporal multi-spectral analysis types against a January 2024 → March 2026 baseline using Sentinel-2 10 m imagery:

| Type | Analysis Method | Key Output |
|---|---|---|
| **Land Use Change** | Pixel classification comparison | Change area (ha), confidence % |
| **Deforestation** | NDVI differencing | Canopy loss (ha), CO₂ equivalent (tonnes) |
| **Illegal Mining** | Spectral anomaly detection | Site count, disturbed area (ha), NEMA alert |
| **Flood Mapping** | SAR Sentinel-1 backscatter | Inundation extent (ha), depth range (m) |
| **Urban Expansion** | Built-up index growth | New built-up area (ha), growth rate (%/yr) |
| **Bathymetric LiDAR** | 532 nm + 1064 nm dual-wavelength | Water depth (m), point density (pts/m²) |

### 📡 Drone Log & Telemetry

- **Live telemetry dashboard** — six channels: altitude AGL (m), ground speed (m/s), battery % (low-battery colour warning), compass heading (°), RC signal strength (%), distance flown (m)
- **Animated canvas chart** — dual overlay of altitude profile and battery decay, redraws at 500 ms intervals
- **Demo flight mode** — animates a drone marker along generated waypoints in real time
- **Flight history** — four pre-loaded Kenya missions; supports CSV/JSON import from any GCS

**Pre-loaded flight logs:**

| Log ID | Date | Platform | Survey Area | Duration | Coverage | Status | Data Quality |
|---|---|---|---|---|---|---|---|
| KE-2026-001 | 2026-03-15 | DJI Phantom 4 RTK | Kiambu Survey Block A | 38 min | 45.2 ha | ✅ Completed | 98.3% |
| KE-2026-002 | 2026-03-14 | senseFly eBee X | Nakuru Road Corridor | 72 min | 210 ha | ✅ Completed | 99.1% |
| KE-2026-003 | 2026-03-12 | DJI Matrice 300 RTK | Nairobi CBD | 45 min | 80 ha | ✅ Completed | 97.8% |
| KE-2026-004 | 2026-03-10 | DJI Mavic 3 Enterprise | Athi River Industrial | 29 min | 22 ha | ❌ Aborted | — |

### 🔌 Aircraft Connection

| Protocol | API | Compatible Hardware |
|---|---|---|
| **Web Bluetooth BLE** | `navigator.bluetooth` | DJI RC, Herelink, Skydroid, FrSky — Chrome only |
| **WebSocket MAVLink** | `WebSocket` at host:port | Mission Planner, QGroundControl, ArduPilot over WiFi |
| **DJI Cloud API** | DJI SDK | Phantom 4 RTK, Mavic 3 Enterprise, Matrice 300/400 |

### 🪪 KCAA Pilot Registry

Full licence management system — see [KCAA Compliance System](#kcaa-compliance-system).

### 🌍 Environmental Planning Lab

Full-stack 7-step GIS pipeline — see [Environmental Planning Lab](#environmental-planning-lab).

---

## Aircraft Database

### Multirotor — 7 Platforms

| Platform | Max Alt | Speed | Endurance | Sensor Suite | Coverage | KCAA |
|---|---|---|---|---|---|---|
| DJI Phantom 4 RTK | 120 m | 14 m/s | 30 min | 20 MP RGB + RTK GNSS | 2 km² @ 120 m | C2 |
| DJI Mavic 3 Enterprise | 120 m | 15 m/s | 45 min | 20 MP RGB + Multispectral | 2.5 km² @ 120 m | C2 |
| DJI Matrice 300 RTK | 120 m | 23 m/s | 55 min | Multi-payload (up to 3) | 5 km² @ 120 m | C3 |
| DJI Matrice 400 | 120 m | 21 m/s | 42 min | Multi-payload | 4.5 km² @ 120 m | C3 |
| Autel EVO Nano+ | 120 m | 15 m/s | 28 min | 50 MP RGB | 1 km² @ 100 m | C1 |
| Yuneec H520E | 120 m | 12 m/s | 28 min | RGB / Thermal | 2 km² @ 120 m | C2 |
| Parrot Anafi USA | 120 m | 15 m/s | 32 min | 21 MP RGB + Thermal + 32× Zoom | 1.5 km² @ 100 m | C2 |

### Fixed-Wing — 4 Platforms

| Platform | Max Alt | Speed | Endurance | Camera | GSD | KCAA |
|---|---|---|---|---|---|---|
| senseFly eBee X | 150 m | 57 km/h | 90 min | RGB / MS / Thermal | 2 cm @ 120 m | C2 |
| senseFly eBee SQ | 120 m | 54 km/h | 55 min | Parrot Sequoia+ MS | 3 cm @ 120 m | C2 |
| WingtraOne GEN II | 150 m | VTOL hover | 55 min | Sony RX1R II 42 MP | 0.7 cm @ 120 m | C3 |
| Trimble UX5 | 300 m | 80 km/h | 50 min | Sony NEX-5T | 2.5 cm @ 120 m | C3 |

### VTOL Hybrid — 2 Platforms

| Platform | Endurance | Coverage | KCAA |
|---|---|---|---|
| Quantum Trinity F90+ | 90 min | 500 ha / sortie | C3 |
| Sky-Hero SPEAR | 60 min | 300 ha @ 120 m | C3 |

### Manned Aircraft — 3 Platforms

| Platform | Service Ceiling | Speed | Endurance | Daily Coverage |
|---|---|---|---|---|
| Cessna 172 Skyhawk | 4,000 m | 226 km/h | 4 h | 500 km²/day |
| Beechcraft King Air B200 | 10,668 m | 540 km/h | 8 h | 2,000 km²/day |
| Cessna 206 Stationair | 4,572 m | 278 km/h | 6 h | 800 km²/day |

> **Auto-validation:** Selecting a drone automatically caps the altitude slider at the platform's operational ceiling and enforces KCAA class limits before any flight plan is generated.

---

## Camera & Sensor Catalogue

### RGB — 3 Sensors

| Sensor | Resolution | Sensor Format | GSD | Bit Depth | Compatible Software |
|---|---|---|---|---|---|
| Sony RX1R II | 42 MP | 35 mm Full Frame | 1.5 cm @ 100 m | 14-bit RAW | Pix4D · Agisoft · ArcGIS |
| DJI Zenmuse P1 | 45 MP | Full Frame | 2.7 cm @ 200 m | DNG RAW | DJI Terra · Pix4D |
| Phase One iXM-100 | 100 MP | Medium Format | 0.8 cm @ 100 m | 16-bit RAW | All GIS software |

### Multispectral — 3 Sensors

| Sensor | Resolution | Bands | GSD | Bit Depth | Compatible Software |
|---|---|---|---|---|---|
| MicaSense RedEdge-P | 2 MP | B, G, R, RE, NIR + Panchro | 6.5 cm @ 120 m | 16-bit TIF | QGIS · ArcGIS · Pix4D |
| Parrot Sequoia+ | 1.2 MP | G, R, RE, NIR (4-band) | 4.8 cm @ 100 m | 16-bit TIF | Pix4Dfields |
| MicaSense Altum-PT | 2 MP | B, G, R, RE, NIR + Thermal | 3.2 cm @ 100 m | 16-bit + IR | Pix4D · ArcGIS |

### Thermal — 2 Sensors

| Sensor | Type | GSD | Temperature Range | Bit Depth |
|---|---|---|---|---|
| FLIR Zenmuse XT2 | Radiometric FLIR | 20 cm @ 100 m | −25 to 135 °C | 16-bit |
| DJI Zenmuse H20T | RGB + Thermal + Laser | Dual mode | −40 to 150 °C | 14-bit |

### LiDAR — 3 Sensors

| Sensor | Point Density | Range | Channels |
|---|---|---|---|
| DJI Zenmuse L2 | 250 pts/m² | 250 m | 5 returns |
| Velodyne VLP-16 | 300 K pts/sec | 100 m | 16 channels |
| YellowScan Mapper+ | 200 pts/m² | 75 m | Full waveform |

### Hyperspectral — 1 Sensor

| Sensor | Spectral Range | Bands | GSD | Bit Depth |
|---|---|---|---|---|
| Resonon Pika XC2 | 400–1000 nm | 281 bands | 30 cm @ 100 m | 12-bit |

### Oblique — 1 Sensor

| Sensor | Configuration | GSD | Coverage |
|---|---|---|---|
| Leica CityMapper-2 | 5-lens: nadir + 4 oblique | 3 cm @ 400 m | Full city block |

---

## Environmental Planning Lab

The EPL is a full-stack 7-step GIS modelling pipeline launched from the **Environmental Planning** nav tab. It accepts four preset Kenya study regions or any custom polygon drawn anywhere on the map, producing a complete land-use zoning plan and a print-quality cartographic master plan.

### Study Regions

| Region | Centre (WGS 84) | Zoom | Study Area |
|---|---|---|---|
| Nairobi Metropolitan | 1.2864° S, 36.8172° E | 12 | 420 ha |
| Mombasa Port & Coast | 4.0435° S, 39.6682° E | 12 | 285 ha |
| Kisumu Lakeside | 0.0917° S, 34.7680° E | 12 | 310 ha |
| Nakuru Rift Valley | 0.3031° S, 36.0800° E | 12 | 375 ha |
| Custom AOI | User-drawn on the EPL map | Dynamic | Computed from real bounds |

### Drawing a Custom AOI

1. Open the Planning Lab and select **Custom AOI from Map** in the region dropdown.
2. Click **Draw AOI** in the EPL toolbar — cursor changes to a crosshair.
3. Click vertices on the map. A green preview line closes back to the first point with each click.
4. **Double-click** to finish. The polygon is locked and area is calculated from real geodetic bounds.
5. Click **Run Pipeline** — all seven steps execute within your drawn area.

The pipeline centre coordinates, swath scale, zone geometry, MCE suitability grid, and master plan all adapt to the actual extent of the drawn polygon automatically.

### The 7-Step Pipeline

```
Step 1  Satellite Ingestion        900 ms
Step 2  DEM Extraction           1,100 ms
Step 3  Watershed & Drainage     1,400 ms
Step 4  Hydrology Modelling      1,800 ms
Step 5  Suitability (MCE)        1,300 ms
Step 6  Urban Zoning             1,000 ms
Step 7  Cartographic Render        700 ms
────────────────────────────────────────
Total pipeline duration         ~8.2 sec
```

#### Step 1 — Satellite Ingestion
Band compositing, cloud masking, and NDVI calculation on Sentinel-2 10 m imagery.
Sources: Sentinel-2 (free) · Landsat 8 · Planet Labs 3 m · WorldView-3 0.3 m.
Bands: B2, B3, B4, B8 (RGB + NIR).

#### Step 2 — DEM Extraction & Terrain Analysis
Elevation model ingestion from SRTM 30 m, ALOS 12.5 m, or Copernicus 30 m.
Computed derivatives: slope, aspect, hillshade, curvature.
Esri World Hillshade tile overlay activated at 62% opacity, plus terrain contour rings, spot elevation markers, and slope aspect arrows.

```
Slope:  S = √ ( (∂z/∂x)² + (∂z/∂y)² )
```

#### Step 3 — Watershed & Drainage Delineation
D8 flow direction algorithm (Jenson & Domingue, 1988) on a depression-filled DEM.
Outputs: flow accumulation raster, stream network, pour-point watershed boundary, drainage density (km/km²).
Tools: GRASS GIS `r.watershed` · GDAL · WhiteboxTools.

#### Step 4 — Hydrological Modelling

**SWAT+ simulation outputs:**

| Parameter | Value |
|---|---|
| Annual runoff | 485 mm/yr |
| Baseflow | 120 mm/yr |
| Evapotranspiration | 840 mm/yr |
| Peak flow | 380 m³/s |
| Drainage density | 2.4 km/km² |

**HEC-RAS 1D hydraulic analysis:**

| Parameter | Value |
|---|---|
| Water surface elevation | 12.4 m |
| Flow velocity | 1.8 m/s |
| Manning's roughness (n) | 0.045 |
| 100-year flood extent | Delineated on map |

#### Step 5 — Multi-Criteria Suitability Evaluation (MCE)

```
Suitability = Σ ( wᵢ × cᵢ )   for i = 1 … 4
```

| Criterion | Default Weight | Description |
|---|---|---|
| Elevation | 25% | Higher ground preferred — reduced flood exposure |
| Flood Risk | 35% | Distance from flood extent — dominant factor |
| Slope | 20% | Gentler slopes preferred for construction |
| Distance to Water | 20% | Proximity to water bodies |

Weights are user-adjustable via live sliders (must sum to 100%). MCE can be recalculated independently without re-running the full pipeline.

#### Step 6 — Urban Zoning Generation

Eight land-use zone types assigned from MCE scores with area statistics in hectares:

| Zone | Colour | Pattern | MCE Level | Description |
|---|---|---|---|---|
| Urban Centre | Purple | Solid | Very High | Commercial & civic core |
| Residential Area | Amber | Solid | High | Low/medium density housing |
| Agriculture | Light Green | Solid | Moderate | Mixed-use farming |
| Conservation Zone | Dark Green | ╱╱ Diagonal hatch | Low | Ecological buffer |
| Wetlands | Light Blue | ╱╱ Diagonal hatch | Very Low | Protection corridors |
| Flood Risk Zone | Red-Orange | Solid | No-build | 100-year flood inundation |
| Marina / Port | Blue | Solid | — | Water-adjacent maritime |
| Infrastructure Corridor | Tan / Ochre | Solid | — | Roads, utilities, easements |

> Conservation and wetland zones use diagonal hatch fill per British Ordnance Survey convention for restricted and sensitive land.

#### Step 7 — Cartographic Rendering & Master Plan

Generates a professional A3 landscape cartographic master plan on an HTML Canvas (1754 × 1240 px).

**Cartographic design standards applied:**

- **White page**, cream map background — matches Ordnance Survey / IGN topographic convention
- **OSM-style base map** — road network (primary roads in gold with casing, secondary in white), building footprints (tan), vegetation patches
- **Zone fills at 72% opacity** — street context remains visible beneath all planning overlays
- **Hydrological layer** — main river (USGS blue `#2166AC`, 3.5 px weight), tributaries (1.8 px), 100-yr flood extent (dashed red), watershed boundary (dashed blue)
- **North arrow** — inside the map frame, bottom-left, white circular backing, red north needle, all four cardinal points
- **Scale bar** — alternating black/white blocks, 0–4 km at 1:50,000, inside the map frame
- **Coordinate graticule** — lat/lng tick labels on left and bottom margins inside the neatline
- **Seven-section legend** — fully inside the neatline: Land Use Zones · Hydrological Features · Infrastructure · Data Summary · Model Parameters · Regulatory Notes · Coordinate System
- **Double-rule neatline frame** — thick outer rule + thin inner rule, standard cartographic convention
- **Navy title block** — organisation name, document title, region, date, reference, CRS, scale
- **Navy footer bar** — generation timestamp, KCAA compliance note, planning disclaimer
- **Times New Roman** — all labels, legend entries, titles, and marginalia

**Export options:**

| Output | Format | Method |
|---|---|---|
| PNG | 1754 × 1240 px | Automatic download on generation |
| PDF | Print-quality A3 | Browser print dialog (`Ctrl+P` / `⌘P`) from preview window |

### EPL Export Formats

| Export | Format | Content |
|---|---|---|
| Planning Layer | GeoJSON (EPSG:4326) | All 8 zone polygons with `zone_id`, `zone_label`, `area_ha`, `description` |
| Planning Report | Plain text (.txt) | MCE weights, SWAT outputs, land classification, algorithm references, regulatory notes |
| Master Plan | PNG + PDF | A3 landscape cartographic map |

> The GeoJSON planning layer loads directly into ArcGIS Pro, QGIS, PostGIS, or AutoCAD Map 3D without any conversion step
