To understand your GIS + ML project, you mainly need to understand **2 major GIS data types**:

1. **Vector data** → points, lines, polygons
2. **Raster data** → grid/pixel images

Everything in your project is built from these.

---

# 1. VECTOR DATA (Shapefile)

A **Shapefile (.shp)** is the most common GIS vector format.

It stores:

* points
* lines
* polygons

Example in your project:

| Data                | Type              |
| ------------------- | ----------------- |
| Urban sample points | Point shapefile   |
| Non-urban points    | Point shapefile   |
| Roads               | Line shapefile    |
| Study area boundary | Polygon shapefile |

---

# WHAT YOU MUST KNOW ABOUT SHAPEFILES

A shapefile is NOT one file.

It is several files together:

| File   | Purpose           |
| ------ | ----------------- |
| `.shp` | geometry          |
| `.shx` | shape index       |
| `.dbf` | attribute table   |
| `.prj` | coordinate system |

You must keep them together in same folder.

---

# Example

```text
UrbanPoints.shp
UrbanPoints.shx
UrbanPoints.dbf
UrbanPoints.prj
```

If you delete `.dbf` or `.shx`, the shapefile may break.

---

# GEOMETRY TYPES

## A. Point

Single coordinate.

Example:

* urban sample point
* weather station

```text
(x,y)
```

---

## B. Line

Connected points.

Example:

* roads
* rivers

---

## C. Polygon

Closed shape/area.

Example:

* city boundary
* forest area

---

# ATTRIBUTE TABLE

Every shapefile has a table.

Example:

| ID | Label    |
| -- | -------- |
| 1  | Urban    |
| 2  | NonUrban |

For your project:

| Label | Meaning   |
| ----- | --------- |
| 1     | Urban     |
| 0     | Non-Urban |

This is VERY important for ML training.

---

# 2. RASTER DATA

Raster = image made of pixels.

Each pixel stores a value.

Satellite images are rasters.

Example:

| Raster      | Pixel Meaning  |
| ----------- | -------------- |
| NDVI        | vegetation     |
| Elevation   | height         |
| Temperature | °C             |
| NDBI        | built-up index |

---

# HOW RASTER WORKS

Raster is like Excel grid.

Example:

```text
12 13 15
18 20 22
25 30 31
```

Each cell = pixel value.

---

# IMPORTANT RASTER CONCEPTS

## Resolution

Pixel size.

Example:

| Resolution | Meaning                |
| ---------- | ---------------------- |
| 10m        | one pixel = 10m ground |
| 30m        | one pixel = 30m ground |

Sentinel-2:

* 10m resolution

Meaning:

* each pixel covers 10×10 meters.

---

## Bands

Satellite images contain multiple bands.

Example:

| Band  | Meaning            |
| ----- | ------------------ |
| Red   | visible red        |
| Green | visible green      |
| Blue  | visible blue       |
| NIR   | near infrared      |
| SWIR  | shortwave infrared |

---

# RGB IMAGE

Normal image uses:

* Red
* Green
* Blue

In GEE:

```javascript
bands: ['B4','B3','B2']
```

---

# NDVI

Vegetation index.

Uses:

* NIR
* Red

Formula:

NDVI=\frac{NIR-Red}{NIR+Red}

Meaning:

| Value | Interpretation |
| ----- | -------------- |
| high  | vegetation     |
| low   | urban/bare     |

---

# NDBI

Urban/building index.

NDBI=\frac{SWIR-NIR}{SWIR+NIR}

Meaning:

| Value | Interpretation |
| ----- | -------------- |
| high  | urban          |
| low   | vegetation     |

---

# MOST IMPORTANT THING IN YOUR PROJECT

You will:

## STEP 1

Create POINT shapefile:

```text
samplepoints.shp
```

with labels:

| Point    | Label |
| -------- | ----- |
| Urban    | 1     |
| NonUrban | 0     |

---

## STEP 2

Prepare raster layers:

* NDVI raster
* NDBI raster
* Elevation raster
* Slope raster

---

## STEP 3

Extract raster values INTO points.

Example:

| Point | NDVI | Elevation | NDBI | Label |
| ----- | ---- | --------- | ---- | ----- |
| P1    | 0.2  | 350       | 0.6  | 1     |
| P2    | 0.8  | 500       | -0.3 | 0     |

THIS becomes your ML dataset.

---

# MOST COMMON GIS FILE FORMATS

## VECTOR FORMATS

| Format     | Use          |
| ---------- | ------------ |
| `.shp`     | shapefile    |
| `.geojson` | web GIS      |
| `.kml`     | Google Earth |

---

## RASTER FORMATS

| Format           | Use              |
| ---------------- | ---------------- |
| `.tif` / `.tiff` | GeoTIFF raster   |
| `.img`           | raster           |
| `.jp2`           | Sentinel imagery |

---

# GEOREFERENCING

GIS data knows real-world location.

Every file has coordinates.

Example:

```text
Latitude: 41.2
Longitude: 32.6
```

Without coordinates:

* map is useless.

---

# COORDINATE SYSTEMS (VERY IMPORTANT)

Two common systems:

| System     | Example |
| ---------- | ------- |
| Geographic | Lat/Lon |
| Projected  | UTM     |

---

# FOR YOUR PROJECT

Usually use:

```text
WGS84 (EPSG:4326)
```

or

```text
UTM Zone 36N
```

Türkiye often uses UTM.

---

# WHAT YOU REALLY NEED TO UNDERSTAND

For your project, focus on these concepts only:

| Must Know         | Why                |
| ----------------- | ------------------ |
| Point shapefile   | training labels    |
| Raster layer      | features           |
| Pixel values      | ML inputs          |
| Attribute table   | labels/data        |
| NDVI/NDBI         | important features |
| Coordinate system | map alignment      |
| Resolution        | detail level       |

That is enough to successfully complete your project.

---

# SIMPLE PROJECT FLOW

```text
Satellite Image (Raster)
        ↓
Create NDVI/NDBI Raster
        ↓
Create Urban/NonUrban Points (Shapefile)
        ↓
Extract Raster Values to Points
        ↓
Create ML Dataset
        ↓
Train Random Forest
        ↓
Predict Urban Growth Map
        ↓
Visualize in QGIS/Web GIS
```

---

# VERY IMPORTANT UNDERSTANDING

## VECTOR = OBJECTS

Example:

* road
* building
* point

## RASTER = CONTINUOUS SURFACE

Example:

* temperature
* vegetation
* satellite image

That distinction is the core of GIS.

---

## 📂 Core GIS File Types
- **Shapefile (.shp, .shx, .dbf)**  
  - `.shp` → geometry (points, lines, polygons)  
  - `.shx` → spatial index linking geometry to attributes  
  - `.dbf` → attribute table (columns + rows of data)  
  - These three are mandatory for a shapefile to work.

- **Projection file (.prj)**  
  - Stores coordinate system info (e.g., WGS84, UTM).  
  - Without it, your data may not align correctly on maps.

---

## 📂 Supporting Files
- **.cpg** → character encoding for text in `.dbf`  
- **.qpj** → alternative projection file (used by QGIS)  
- **.sbn / .sbx** → spatial index files (speed up queries)  
- **.xml** → metadata (dataset description)

---

## 🗂 Other Common GIS Formats
- **GeoTIFF (.tif)** → raster data (elevation, NDVI, probability maps).  
- **KML/KMZ** → Google Earth vector format.  
- **GeoJSON (.geojson)** → web‑friendly vector format.  
- **File Geodatabase (.gdb)** → ESRI’s database format for large projects.  
- **CSV with coordinates** → tabular data that can be converted into points.

---

## 🧩 Best Practices for GIS Projects
1. **Keep shapefile bundles together** → always move `.shp`, `.shx`, `.dbf`, `.prj` together.  
2. **Check CRS** → projection files (`.prj`) ensure correct alignment.  
3. **Document metadata** → use `.xml` or a README to explain your dataset.  
4. **Raster vs Vector** → know when to use rasters (continuous data like NDVI) vs vectors (discrete features like rivers).  
5. **Version control** → store datasets in GitHub or cloud storage with clear naming.  
6. **Interoperability** → prefer open formats (GeoJSON, GeoTIFF) if sharing outside ArcGIS/QGIS.

---

👉 For your wildfire susceptibility project, you’ll mainly handle:
- **Shapefiles** (points with probability values, rivers, AOI boundaries).  
- **GeoTIFFs** (rasterized probability maps, DEM, NDVI layers).  

Here’s a clean **workflow diagram** idea for your wildfire susceptibility project. It shows how the different file types interact from start to finish:

---

## 🔄 GIS Project Workflow

```text
CSV (Exported from Google Earth Engine)
   │
   ▼
Python (ML Model Prediction)
   - Clean dataset (drop metadata)
   - Align features with training set
   - Predict probabilities
   │
   ▼
Shapefile (.shp + .shx + .dbf + .prj)
   - Geometry: AOI points
   - Attributes: Probability values
   │
   ▼
Rasterization (GeoTIFF .tif)
   - Convert point probabilities → continuous raster surface
   - Resolution: 100 m
   │
   ▼
Visualization (QGIS / ArcMap)
   - Load shapefile (vector) for inspection
   - Load GeoTIFF (raster) for probability map
   - Symbolize burned/unburned points, probability gradients
```

---

## 📂 File Roles in the Workflow
- **CSV** → raw tabular data exported from Earth Engine.  
- **Shapefile bundle** (`.shp`, `.shx`, `.dbf`, `.prj`) → vector dataset with geometry + attributes.  
- **GeoTIFF (.tif)** → raster dataset for probability surface.  
- **QGIS/ArcMap project** → visualization, styling, and final maps.

---

This diagram makes it clear:  
- **CSV** is your input.  
- **Shapefile** is your intermediate vector output.  
- **GeoTIFF** is your raster output.  
- **QGIS/ArcMap** is your visualization environment.  

---
