# GIS + Machine Learning Project Notes (Organized Guide)

# 1. Introduction to GIS Data

GIS mainly works with **two major data types**:

| Data Type   | Description         | Example                             |
| ----------- | ------------------- | ----------------------------------- |
| Vector Data | Discrete objects    | Roads, buildings, points            |
| Raster Data | Continuous surfaces | Satellite images, NDVI, temperature |

Everything in a GIS + ML project is built from these two concepts.

---

# 2. Vector Data

Vector data represents real-world objects using geometry.

## Geometry Types

### A. Point

A single coordinate location.

Example:

* Urban sample point
* Weather station
* Fire incident location

```text
(x, y)
```

---

### B. Line

Connected points forming a path.

Example:

* Roads
* Rivers
* Power lines

---

### C. Polygon

Closed area representing boundaries.

Example:

* City boundary
* Forest area
* Study area (AOI)

---

# 3. Shapefile (.shp)

The most common GIS vector format is the **Shapefile**.

A shapefile is NOT a single file.

It is a group of files that must stay together.

---

## Essential Shapefile Components

| File   | Purpose           |
| ------ | ----------------- |
| `.shp` | Stores geometry   |
| `.shx` | Geometry index    |
| `.dbf` | Attribute table   |
| `.prj` | Coordinate system |

Example:

```text
UrbanPoints.shp
UrbanPoints.shx
UrbanPoints.dbf
UrbanPoints.prj
```

If `.dbf` or `.shx` is missing, the shapefile may fail.

---

## Supporting Shapefile Files

| File        | Purpose                     |
| ----------- | --------------------------- |
| `.cpg`      | Text encoding               |
| `.qpj`      | Alternative projection info |
| `.sbn/.sbx` | Spatial indexing            |
| `.xml`      | Metadata                    |

---

# 4. Attribute Table

Every shapefile has an attribute table.

Example:

| ID | Label    |
| -- | -------- |
| 1  | Urban    |
| 2  | NonUrban |

For ML projects:

| Label | Meaning   |
| ----- | --------- |
| 1     | Urban     |
| 0     | Non-Urban |

This label column becomes the target variable for Machine Learning.

---

# 5. Raster Data

Raster data is made of pixels arranged in a grid.

Each pixel stores a value.

Examples:

* Satellite imagery
* NDVI
* Elevation
* Temperature

---

# 6. Raster Structure

Raster behaves like a matrix or Excel grid.

Example:

```text
12 13 15
18 20 22
25 30 31
```

Each cell = one pixel value.

---

# 7. Important Raster Concepts

## A. Resolution

Resolution = pixel size on the ground.

| Resolution | Meaning                  |
| ---------- | ------------------------ |
| 10m        | 1 pixel = 10 × 10 meters |
| 30m        | 1 pixel = 30 × 30 meters |

Example:

* Sentinel-2 → 10m resolution
* Landsat → 30m resolution

Higher resolution = more detail.

---

## B. Bands

Satellite images contain multiple spectral bands.

| Band  | Meaning             |
| ----- | ------------------- |
| Blue  | Visible blue light  |
| Green | Visible green light |
| Red   | Visible red light   |
| NIR   | Near Infrared       |
| SWIR  | Shortwave Infrared  |

---

# 8. RGB Images

Normal color images use:

* Red
* Green
* Blue

In Google Earth Engine:

```javascript
bands: ['B4','B3','B2']
```

| Band | Color |
| ---- | ----- |
| B4   | Red   |
| B3   | Green |
| B2   | Blue  |

---

# 9. NDVI (Vegetation Index)

NDVI measures vegetation health.

Formula:

NDVI=\frac{NIR-Red}{NIR+Red}

---

## NDVI Interpretation

| NDVI Value | Meaning               |
| ---------- | --------------------- |
| High       | Dense vegetation      |
| Medium     | Sparse vegetation     |
| Low        | Urban/bare soil/water |

---

# 10. NDBI (Built-Up Index)

NDBI identifies urban/built-up areas.

NDBI=\frac{SWIR-NIR}{SWIR+NIR}

---

## NDBI Interpretation

| NDBI Value | Meaning         |
| ---------- | --------------- |
| High       | Urban/buildings |
| Low        | Vegetation      |

---

# 11. Other Important Raster Layers

## DEM (Digital Elevation Model)

Stores terrain elevation.

Example:

* Mountain height
* Valley depth

---

## Slope

Derived from DEM.

Represents terrain steepness.

Useful in:

* Wildfire analysis
* Flood modeling
* Urban planning

---

## Aspect

Direction terrain faces.

Example:

* North-facing slope
* South-facing slope

Important in environmental analysis.

---

# 12. Coordinate Systems (CRS)

GIS data must know its real-world location.

Without coordinates:

* maps cannot align properly.

---

## Common Coordinate Systems

| System     | Example            |
| ---------- | ------------------ |
| Geographic | Latitude/Longitude |
| Projected  | UTM                |

---

## Common CRS for Türkiye

### WGS84

```text
EPSG:4326
```

Uses latitude/longitude.

---

### UTM Zone 36N

Projected coordinate system commonly used in Türkiye.

Better for:

* distance
* area
* measurement accuracy

---

# 13. Georeferencing

Georeferencing means attaching real-world coordinates to data.

Example:

```text
Latitude: 41.2
Longitude: 32.6
```

All GIS datasets require spatial reference information.

---

# 14. Common GIS File Formats

# Vector Formats

| Format     | Use              |
| ---------- | ---------------- |
| `.shp`     | Shapefile        |
| `.geojson` | Web GIS          |
| `.kml`     | Google Earth     |
| `.gdb`     | ESRI Geodatabase |

---

# Raster Formats

| Format       | Use              |
| ------------ | ---------------- |
| `.tif/.tiff` | GeoTIFF raster   |
| `.img`       | Raster           |
| `.jp2`       | Sentinel imagery |

---

# 15. CSV in GIS

CSV files can store coordinates.

Example:

| ID | Latitude | Longitude |
| -- | -------- | --------- |
| 1  | 41.2     | 32.6      |

GIS software can convert CSV to point layers.

---

# 16. Machine Learning in GIS

GIS + ML combines:

* spatial data
* raster analysis
* predictive modeling

---

# 17. Core ML Workflow in GIS

## STEP 1 — Create Training Points

Create shapefile:

```text
samplepoints.shp
```

Example:

| Point    | Label |
| -------- | ----- |
| Urban    | 1     |
| NonUrban | 0     |

---

# STEP 2 — Prepare Raster Layers

Examples:

* NDVI raster
* NDBI raster
* DEM raster
* Slope raster
* Temperature raster

These become ML features.

---

# STEP 3 — Extract Raster Values to Points

Example result:

| Point | NDVI | Elevation | NDBI | Label |
| ----- | ---- | --------- | ---- | ----- |
| P1    | 0.2  | 350       | 0.6  | 1     |
| P2    | 0.8  | 500       | -0.3 | 0     |

This table becomes the ML dataset.

---

# STEP 4 — Train ML Model

Common algorithms:

| Algorithm     | Use                    |
| ------------- | ---------------------- |
| Random Forest | Classification         |
| XGBoost       | Advanced boosting      |
| LightGBM      | Fast gradient boosting |
| SVM           | Binary classification  |

---

# STEP 5 — Prediction

Model predicts:

* urban growth
* wildfire susceptibility
* flood risk
* land cover

Output:

* probability map
* classified raster

---

# STEP 6 — Visualization

Visualize outputs in:

* QGIS
* ArcGIS
* Web GIS

---

# 18. Raster vs Vector (Most Important Concept)

## VECTOR = OBJECTS

Examples:

* roads
* rivers
* buildings
* sample points

Discrete features.

---

## RASTER = CONTINUOUS SURFACE

Examples:

* satellite image
* temperature
* NDVI
* elevation

Continuous data.

This distinction is the core of GIS.

---

# 19. Wildfire Susceptibility Project Workflow

```text
Google Earth Engine
        ↓
Export CSV
        ↓
Python ML Processing
        ↓
Predict Probabilities
        ↓
Create Shapefile
        ↓
Rasterization
        ↓
Generate GeoTIFF
        ↓
Visualization in QGIS
```

---

# 20. Detailed Workflow

## A. Data Collection

Sources:

* Sentinel-2 imagery
* DEM
* Weather data
* Fire history

---

## B. Feature Preparation

Generate:

* NDVI
* NDBI
* Slope
* Elevation
* Distance to roads
* Temperature

---

## C. Training Dataset

Combine:

* raster values
* labeled points

Final dataset:

| NDVI | Elevation | Slope | Temp | Label |
| ---- | --------- | ----- | ---- | ----- |
| 0.3  | 500       | 20    | 35   | 1     |

---

## D. Model Training

Train:

* Random Forest
* XGBoost
* LightGBM

---

## E. Prediction

Predict wildfire probability for every pixel.

Output:

* probability raster

---

## F. Rasterization

Convert predictions into GeoTIFF.

Example:

* 100m resolution wildfire risk map

---

## G. Visualization

Use QGIS:

* style layers
* create maps
* analyze results

---

# 21. Important GIS Operations

| Operation | Purpose                 |
| --------- | ----------------------- |
| Clip      | Cut data to AOI         |
| Buffer    | Create distance zones   |
| Intersect | Find overlapping areas  |
| Rasterize | Convert vector → raster |
| Vectorize | Convert raster → vector |
| Reproject | Change CRS              |

---

# 22. Common GIS Software

| Software            | Use                       |
| ------------------- | ------------------------- |
| QGIS                | Open-source GIS           |
| ArcGIS              | ESRI GIS platform         |
| Google Earth Engine | Cloud remote sensing      |
| SNAP                | Sentinel image processing |

---

# 23. Python Libraries for GIS + ML

| Library      | Purpose             |
| ------------ | ------------------- |
| GeoPandas    | Vector processing   |
| Rasterio     | Raster processing   |
| GDAL         | GIS data handling   |
| Shapely      | Geometry operations |
| scikit-learn | Machine Learning    |
| XGBoost      | Boosting models     |
| NumPy        | Numerical arrays    |
| Pandas       | Tables/dataframes   |

---

# 24. Best Practices

## A. Keep Shapefile Files Together

Never separate:

* `.shp`
* `.shx`
* `.dbf`
* `.prj`

---

## B. Check CRS

Always ensure layers use the same coordinate system.

Misaligned CRS causes mapping errors.

---

## C. Use Open Formats

Prefer:

* GeoTIFF
* GeoJSON

for sharing projects.

---

## D. Organize Project Structure

Example:

```text
Project/
│
├── data/
├── raster/
├── vector/
├── output/
├── scripts/
└── maps/
```

---

## E. Store Metadata

Document:

* data source
* CRS
* resolution
* date

---

# 25. Final Core Understanding

For your GIS + ML projects, the MOST important ideas are:

| Concept           | Why Important       |
| ----------------- | ------------------- |
| Point shapefile   | Training labels     |
| Raster layers     | ML features         |
| Pixel values      | Model inputs        |
| Attribute table   | Labels/data         |
| NDVI/NDBI         | Important indices   |
| Coordinate system | Alignment           |
| Resolution        | Spatial detail      |
| Raster vs Vector  | Core GIS foundation |

---

# 26. Final Simplified Pipeline

```text
Satellite Image (Raster)
        ↓
Generate NDVI/NDBI
        ↓
Create Sample Points
        ↓
Extract Raster Values
        ↓
Build ML Dataset
        ↓
Train Model
        ↓
Predict Probability Map
        ↓
Export GeoTIFF
        ↓
Visualize in QGIS/Web GIS
```

This is the complete foundation of a modern GIS + Machine Learning workflow.
