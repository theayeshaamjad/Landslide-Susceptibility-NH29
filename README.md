# Landslide Susceptibility Mapping for the NH-29 Corridor (Chümoukedima to Medziphema)

## Overview
This repository contains the data, methodology, and spatial outputs for a Landslide Susceptibility Mapping (LSM) project along the NH-29 corridor. The project leverages cloud-based computing via Google Earth Engine (GEE) for environmental data extraction and advanced spatial modeling in ArcMap to perform a Multi-Criteria Decision Analysis (MCDA). The analytical framework utilizes the Analytic Hierarchy Process (AHP) to establish mathematically and geomorphologically sound weight distributions for twelve triggering and conditioning factors.

## Final Susceptibility Map
![Final Map](Maps/output_map/final%20sus%20map.png)

*Figure 1: Landslide Susceptibility Map categorized into five risk zones using Natural Breaks (Jenks).*

**Susceptibility Classes:**
*   **Very Low (Dark Green):** Stable areas with flat terrain, dense forest cover, and low rainfall.
*   **Low (Light Green):** Areas with gentle slopes and minimal anthropogenic disturbance.
*   **Moderate (Yellow):** Transitional zones where susceptibility is balanced by environmental factors.
*   **High (Orange):** Highly susceptible areas with steep slopes, high rainfall, or sparse vegetation.
*   **Very High (Red):** Critical zones near road-cuts, active streams, or extremely steep barren slopes.

## Data Sources & Geospatial Parameters
Data was synthesized using Google Earth Engine and open-source vector repositories, processed at high resolution.

1.  **Topography (SRTM GL1, 30m):** Elevation, Slope, Aspect, Curvature (Plan & Profile), and Topographic Wetness Index (TWI).
2.  **Land Cover:** LULC (Google Dynamic World, 10m) and NDVI (Sentinel-2, 10m).
3.  **Hydrology (HDX/HOTOSM):** Distance to Streams and Drainage Density.
4.  **Meteorology:** Mean Annual Precipitation (CHIRPS, 5.5km).
5.  **Infrastructure (HDX/HOTOSM):** Distance to Roads.
6.  **Geo-Environmental:** Soil Texture (OpenLandMap, 250m).

## Methodology
### 1. Data Processing & Reclassification
All 12 geospatial layers were reclassified onto a standard 1 to 5 scale (where 1 = Very Low susceptibility and 5 = Very High susceptibility). For example, slopes between 34° and 58° were ranked 5 (critically steep), while stable plains (0°–5.7°) were ranked 1. 

### 2. Analytic Hierarchy Process (AHP)
A $12 \times 12$ pairwise comparison matrix was constructed to rank the influencing factors based on their relative importance in slope instability. The principal eigenvector was extracted to determine the following relative weights:

| Rank | Parameter | Weight (w) | Influence (%) | Scientific Justification |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Slope | 0.211 | 21.1% | Primary driver of shear stress and gravitational force. |
| 2 | Rainfall | 0.168 | 16.8% | Dynamic temporal trigger that increases pore-water pressure. |
| 3 | LULC | 0.126 | 12.6% | Influences surface stability and root cohesion. |
| 4 | TWI | 0.098 | 9.8% | Identifies zones of potential soil saturation. |
| 5 | Dist. to Streams | 0.079 | 7.9% | Accounts for basal support removal via toe-erosion. |
| 6 | Dist. to Roads | 0.063 | 6.3% | Anthropogenic mechanical slope modification. |
| 7 | Elevation | 0.052 | 5.2% | Influences climatic regime. |
| 8 | Aspect | 0.051 | 5.1% | Affects soil moisture and solar exposure. |
| 9 | Soil Type | 0.044 | 4.4% | Determines drainage and shear strength. |
| 10 | Curvature | 0.042 | 4.2% | Affects flow acceleration and convergence. |
| 11 | NDVI | 0.036 | 3.6% | Secondary modifier reflecting surface condition. |
| 12 | Drainage Density | 0.030 | 3.0% | Represents runoff concentration potential. |

**Model Validation:** The Consistency Ratio (CR) for this weighting scheme is **0.079**. Because $CR < 0.10$, the pairwise comparison matrix is mathematically consistent and scientifically sound for mapping slope instability.

### 3. Spatial Integration
The reclassified layers were integrated in ArcMap using the Raster Calculator, applying the normalized AHP weights to generate the final contiguous susceptibility surface.
