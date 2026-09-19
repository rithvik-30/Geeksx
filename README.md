# GroundTruth AI

## AI-Powered Geospatial Data Verification & Freshness Engine

GroundTruth AI uses deep-learning analysis of remote-sensing imagery to identify locations where existing geographic data may no longer match observed development.

Rather than automatically modifying maps, the system produces evidence-backed discrepancy candidates with confidence and verification priority for human review.

## Current Prototype

Satellite imagery
→ AI building segmentation
→ building masks / footprints
→ evaluation against SpaceNet 7 annotations

Planned map verification stage:

AI building observations
+
OpenStreetMap reference data
→ discrepancy detection
→ confidence / priority
→ human verification

## Current Baseline

Evaluated on 10 SpaceNet 7 scenes.

| Metric | Mean ± Std |
|---|---:|
| Precision | 0.7377 ± 0.0916 |
| Recall | 0.7057 ± 0.1296 |
| F1 / Dice | 0.7201 ± 0.1104 |
| IoU | 0.5738 ± 0.1434 |

Representative cases:

- Best: F1 = 0.9016
- Typical: F1 = 0.7416
- Hard: F1 = 0.5719

## Neural Model

- XDXD SpaceNet-4 U-Net
- VGG16 encoder
- ~29.3M parameters
- 512 × 512 inference tiles
- PyTorch

## Tech Stack

Python, PyTorch, Solaris, Rasterio, GeoPandas, Shapely, GDAL,
SpaceNet 7, OpenStreetMap / Overpass API, PostgreSQL/PostGIS,
FastAPI, React, Leaflet, Google Colab / NVIDIA T4.

## Data Sources

### SpaceNet 7
Labelled building segmentation and temporal imagery.

### OpenStreetMap
Existing geographic reference layer for the map-verification stage.

### Sentinel-2
Planned broad-area current monitoring/supporting evidence.

## Roadmap

- [x] SpaceNet 7 baseline
- [x] Real-image inference
- [x] 10-scene benchmark
- [x] Best / Typical / Hard analysis
- [ ] AI vs OpenStreetMap polygon matching
- [ ] Discrepancy confidence scoring
- [ ] Human verification interface
- [ ] India-focused evaluation
- [ ] Model improvement
- [ ] End-to-end web prototype


## Benchmark Evidence

The current prototype was evaluated on 10 SpaceNet 7 scenes across five AOIs and two time points.

The repository includes:

- `results/benchmark_results.csv` — numerical benchmark results
- `results/benchmark_visuals/` — visual analysis for all 10 scenes
- `results/benchmark_visuals/10_scene_contact_sheet.png` — overview of all scenes
- `results/demo_cases/` — detailed Best / Typical / Hard case analysis

### Representative Cases

| Case | F1 | IoU |
|---|---:|---:|
| Best | 0.9016 | 0.8208 |
| Typical | 0.7416 | 0.5893 |
| Hard | 0.5719 | 0.4004 |

The hard case is intentionally included to show model limitations and avoid presenting performance from a single cherry-picked scene.
