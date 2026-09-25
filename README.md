# Landslide Susceptibility Mapping for the NH-29 Corridor (Chümoukedima to Medziphema)

## Overview
This repository contains the data, methodology, and spatial outputs for a Landslide Susceptibility Mapping (LSM) project along the NH-29 corridor[cite: 7]. The project leverages cloud-based computing via Google Earth Engine (GEE) for environmental data extraction and advanced spatial modeling in ArcMap to perform a Multi-Criteria Decision Analysis (MCDA)[cite: 7]. The analytical framework utilizes the Analytic Hierarchy Process (AHP) to establish mathematically and geomorphologically sound weight distributions for twelve triggering and conditioning factors[cite: 10].

## Final Susceptibility Map
![Final Map](Maps/output_map/final%20sus%20map.png)

*Figure 1: Landslide Susceptibility Map categorized into five risk zones using Natural Breaks (Jenks)[cite: 11].*

**Susceptibility Classes:**
*   **Very Low (Dark Green):** Stable areas with flat terrain, dense forest cover, and low rainfall[cite: 9].
*   **Low (Light Green):** Areas with gentle slopes and minimal anthropogenic disturbance[cite: 9].
*   **Moderate (Yellow):** Transitional zones where susceptibility is balanced by environmental factors[cite: 9].
*   **High (Orange):** Highly susceptible areas with steep slopes, high rainfall, or sparse vegetation[cite: 9].
*   **Very High (Red):** Critical zones near road-cuts, active streams, or extremely steep barren slopes[cite: 9].

## Data Sources & Geospatial Parameters
Data was synthesized using Google Earth Engine and open-source vector repositories, processed at high resolution[cite: 7].

1.  **Topography (SRTM GL1, 30m):** Elevation, Slope, Aspect, Curvature (Plan & Profile), and Topographic Wetness Index (TWI)[cite: 7].
2.  **Land Cover:** LULC (Google Dynamic World, 10m) and NDVI (Sentinel-2, 10m)[cite: 7].
3.  **Hydrology (HDX/HOTOSM):** Distance to Streams and Drainage Density[cite: 7].
4.  **Meteorology:** Mean Annual Precipitation (CHIRPS, 5.5km)[cite: 7].
5.  **Infrastructure (HDX/HOTOSM):** Distance to Roads[cite: 7].
6.  **Geo-Environmental:** Soil Texture (OpenLandMap, 250m)[cite: 7].

## Methodology
### 1. Data Processing & Reclassification
All 12 geospatial layers were reclassified onto a standard 1 to 5 scale (where 1 = Very Low susceptibility and 5 = Very High susceptibility)[cite: 11]. For example, slopes between 34° and 58° were ranked 5 (critically steep), while stable plains (0°–5.7°) were ranked 1[cite: 11]. 

### 2. Analytic Hierarchy Process (AHP)
A $12 \times 12$ pairwise comparison matrix was constructed to rank the influencing factors based on their relative importance in slope instability[cite: 10]. The principal eigenvector was extracted to determine the following relative weights:

| Rank | Parameter | Weight (w) | Influence (%) | Scientific Justification |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Slope | 0.211 | 21.1% | Primary driver of shear stress and gravitational force[cite: 10]. |
| 2 | Rainfall | 0.168 | 16.8% | Dynamic temporal trigger that increases pore-water pressure[cite: 10]. |
| 3 | LULC | 0.126 | 12.6% | Influences surface stability and root cohesion[cite: 10]. |
| 4 | TWI | 0.098 | 9.8% | Identifies zones of potential soil saturation[cite: 10]. |
| 5 | Dist. to Streams | 0.079 | 7.9% | Accounts for basal support removal via toe-erosion[cite: 10]. |
| 6 | Dist. to Roads | 0.063 | 6.3% | Anthropogenic mechanical slope modification[cite: 10]. |
| 7 | Elevation | 0.052 | 5.2% | Influences climatic regime[cite: 10]. |
| 8 | Aspect | 0.051 | 5.1% | Affects soil moisture and solar exposure[cite: 7]. |
| 9 | Soil Type | 0.044 | 4.4% | Determines drainage and shear strength[cite: 11]. |
| 10 | Curvature | 0.042 | 4.2% | Affects flow acceleration and convergence[cite: 7]. |
| 11 | NDVI | 0.036 | 3.6% | Secondary modifier reflecting surface condition[cite: 10]. |
| 12 | Drainage Density | 0.030 | 3.0% | Represents runoff concentration potential[cite: 10]. |

**Model Validation:** The Consistency Ratio (CR) for this weighting scheme is **0.079**[cite: 10]. Because $CR < 0.10$, the pairwise comparison matrix is mathematically consistent and scientifically sound for mapping slope instability[cite: 10].

### 3. Spatial Integration
The reclassified layers were integrated in ArcMap using the Raster Calculator, applying the normalized AHP weights to generate the final contiguous susceptibility surface[cite: 11].
