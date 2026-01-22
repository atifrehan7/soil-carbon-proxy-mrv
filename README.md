# Soil–Vegetation–Climate Proxies for Cropland Analysis  
**Brandenburg, Germany (Summer JJA 2024)**

## Overview
This project demonstrates a complete, transparent Earth Observation (EO) workflow to analyze cropland vegetation and soil conditions using satellite-derived indices and reanalysis climate data.  
The focus is on **clear data processing, spatial interpretation, and reproducibility**, rather than model complexity.

The workflow follows good practice commonly used in soil monitoring and MRV-style (Measurement, Reporting, Verification) analyses.

---

## Study Area
- **Region:** Brandenburg, Germany  
- **Land-use focus:** Cropland only  
- **Season analyzed:** Summer (JJA 2024), representing peak vegetation activity

---

## Data Sources

### Satellite-based indices (Sentinel-2)
- **NDVI (Normalized Difference Vegetation Index)**  
  Proxy for vegetation greenness and biomass.
- **BSI (Bare Soil Index)**  
  Proxy for exposed soil and low vegetation cover.
- **SAVI (Soil Adjusted Vegetation Index)**  
  Vegetation index adjusted for soil background effects.

Spatial resolution: **10–20 m** (used at full resolution for analysis).

---

### Land cover
- **ESA WorldCover (10 m)**  
  Used to extract **cropland-only** pixels and exclude forests, urban areas, and water.

---

### Climate data
- **ERA5-Land reanalysis**
  - Volumetric soil moisture (top layer)
  - 2 m air temperature

Spatial resolution: **~9 km**  
Used as **climatic background information**, not field-scale truth.

---

## Methodology

1. **Data acquisition**
   - Seasonal summer composites generated in Google Earth Engine.
   - Exported as GeoTIFF for local processing.

2. **Cropland masking**
   - ESA WorldCover used to retain cropland pixels only.
   - All vegetation indices masked accordingly.

3. **Quality control**
   - Basic statistics (min, max, mean, std).
   - Histograms for all continuous variables.

4. **Spatial aggregation**
   - Cropland NDVI, BSI, and SAVI aggregated to the ERA5 grid.
   - NaN-aware averaging applied to avoid artificial zero values.
   - ERA5 cells with insufficient cropland coverage excluded.

5. **Exploratory analysis**
   - Scatter plots and correlation analysis between:
     - NDVI / BSI / SAVI
     - Soil moisture and temperature

6. **Visualization**
   - Spatial maps generated at reduced resolution **only for visualization**.
   - Full resolution preserved for analysis.
   - Figures saved for reproducibility and reporting.

---

## Project Structure

soil-carbon-proxy-mrv/
│
├── data/
│ ├── raw/
│ │ ├── ndvi/
│ │ ├── bsi/
│ │ ├── savi/
│ │ ├── worldcover/
│ │ └── era5_land/
│ │
│ └── processed/
│ ├── cropland_only/
│ └── aligned_to_era5/
│
├── notebooks/
│ ├── 01_data_check.ipynb
│ ├── 02_cropland_masking.ipynb
│ ├── 03_cropland_stats_histograms.ipynb
│ ├── 04_align_to_era5.ipynb
│ ├── 05_scatter_and_correlations.ipynb
│ └── 06_overview_statistics_and_maps.ipynb
│
├── outputs/
│ └── figures/
│
├── requirements.txt
└── README.md

## Key Results (Exploratory)

- After restricting the analysis to cropland areas and aggregating Sentinel-2 indices to the ERA5-Land grid, clear but moderate relationships between vegetation/soil indicators and climate variables are observed at the regional scale.

- NDVI and SAVI show a **positive association with air temperature**, indicating higher vegetation activity during warmer summer conditions at the ERA5 grid scale.

- Both NDVI and SAVI exhibit a **weak to moderate positive relationship with soil moisture**, with substantial scatter, reflecting the combined influence of crop type, management practices, and the coarse spatial resolution of ERA5-Land.

- The Bare Soil Index (BSI) shows a **strong negative relationship with NDVI and SAVI**, confirming its sensitivity to exposed soil versus vegetated surfaces.

- Relationships between BSI and soil moisture are weak and noisy, suggesting that BSI primarily captures surface cover conditions rather than direct soil moisture dynamics at the regional scale.

- ERA5-Land soil moisture and temperature provide **useful climatic context**, but the observed relationships should be interpreted as **exploratory and regional-scale**, not as field-level or causal links.


## Limitations

- ERA5-Land resolution is coarse and not suitable for field-level inference.
- Indices are **proxies**, not direct measurements of soil carbon.
- Seasonal snapshot only; interannual variability not addressed.

---

## Future Work (Planned)
- Incorporate simple, interpretable ML models (e.g. linear regression or random forest) as an **exploratory extension**, not a replacement for physical interpretation.
- Extend analysis to multi-year time series.
- Integrate field boundaries or additional soil datasets if available.

---

## Reproducibility
All processing steps are documented in notebooks and can be reproduced using the provided folder structure and requirements.

---

## Author
Prepared as a portfolio and research-oriented project demonstrating EO-based cropland analysis and climate-contextual interpretation.

