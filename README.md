# Virginia Invasive Plant Species — Distribution Modeling & Analysis

**Ray Santiago Flores & Seun Oladipo · Computational Environmental Science · Spring 2026 · University of Virginia**

A spatial analysis and Species Distribution Model (SDM) for invasive plant species in Virginia, combining USFS occurrence records, WorldClim bioclimatic rasters, NLCD land cover data, and GADM administrative boundaries. Results were presented as a research poster.

---

## Overview

Invasive plant species represent a significant threat to Virginia's native ecosystems, forest health, and biodiversity. This project builds a data pipeline from raw occurrence and climate data through to a Random Forest–based Species Distribution Model that predicts suitable habitat across Virginia, with visualization of both current distribution and climate-driven spread risk.

---

## Key Deliverables

| File | Description |
|---|---|
| `virginia_invasives_analysis.Rmd` | Full analysis — data cleaning, EDA, spatial modeling, visualization |
| `EVSC_project_v2.Rmd` | Extended version with additional SDM iterations |
| `Final Poster.pdf` | Research poster presented at end-of-semester symposium |
| `PRJ - 4 - Final Presentation.docx` | Final presentation slides and write-up |

---

## Data Sources

| Dataset | Source | Description |
|---|---|---|
| VIPS Invasive Species List | Virginia Dept. of Conservation & Recreation | Oct 2024 — species inventory with presence flags |
| `S_USA.Bio_InvasivePlantCurrent` | USDA Forest Service | National shapefile of current invasive plant occurrences |
| WorldClim v2.1 (30s resolution) | [worldclim.org](https://worldclim.org) | 19 bioclimatic variables (USA tile + national layer) |
| NLCD 2021 | Multi-Resolution Land Characteristics Consortium | Virginia land cover raster |
| GADM v4.1 | [gadm.org](https://gadm.org) | U.S. state and county administrative boundaries (`.rds`) |

---

## Methods & Technical Stack

- **Language:** R
- **Key packages:** `sf`, `terra`, `tmap`, `dismo`, `randomForest`, `geodata`, `tidyverse`, `readxl`, `patchwork`, `scales`
- **Spatial methods:**
  - Shapefile loading and reprojection (`sf`)
  - Raster extraction and resampling (`terra`)
  - Background point sampling for SDM pseudo-absences (`dismo`)
  - Bioclim envelope modeling as baseline
- **Machine learning:** Random Forest classifier for SDM — predicts habitat suitability based on bioclimatic predictors
- **Visualization:** Choropleth maps by county, habitat suitability raster overlays, species richness plots

---

## Analysis Pipeline

```
1. Data Ingestion
   ├── VIPS spreadsheet → species presence matrix
   ├── USFS shapefile → point occurrences clipped to Virginia
   ├── WorldClim rasters → bioclim variable stack
   └── NLCD raster → land cover classification

2. Cleaning & EDA
   ├── Species presence encoding (binary flags)
   ├── County-level aggregation and choropleth mapping
   └── Exploratory climate envelope plots

3. Species Distribution Modeling
   ├── Background point generation (pseudo-absences)
   ├── Bioclim baseline model (dismo)
   ├── Random Forest SDM (climate + land cover predictors)
   └── Predicted suitability raster across Virginia

4. Visualization & Reporting
   ├── Habitat suitability maps
   ├── Top-10 most widespread species analysis
   └── Research poster (Final Poster.pdf)
```

---

## Repository Structure

```
├── virginia_invasives_analysis.Rmd    # Main analysis notebook
├── EVSC_project_v2.Rmd               # Extended SDM version
├── data/
│   ├── vips-list-oct2024.xlsx         # VIPS species inventory
│   ├── Bio_InvasivePlantCurrent/      # USFS shapefiles
│   ├── climate/
│   │   └── wc2.1_country/             # WorldClim rasters
│   ├── gadm/                          # Administrative boundaries
│   └── nlcd_2021_virginia.tif         # Land cover raster
└── deliverables/
    ├── Final Poster.pdf
    └── PRJ - 4 - Final Presentation.docx
```

> **Note:** Large raster files (WorldClim `.tif`, NLCD `.tif`) are excluded from version control via `.gitignore`. Download instructions are in the analysis notebook.

---

## About

Completed as the final project for Computational Environmental Science at the University of Virginia. Poster presented at the Spring 2026 end-of-semester symposium.

**Authors:** Ray Santiago Flores & Seun Oladipo | [raymondosf@gmail.com](mailto:raymondosf@gmail.com)
