Your project is a **GIS + Machine Learning Decision Support System** for predicting areas that are likely to experience **urban growth** in the future.

It is based on your teacher’s wildfire project, but you adapted it into an **Urban Growth Susceptibility Mapping System**. 

# Your Project Title

A possible final title:

> **GIS and Machine Learning-Based Urban Growth Susceptibility Mapping System for Decision Support**

---

# What Your Project Does

Your system:

1. Collects satellite and GIS data
2. Learns patterns of existing urban areas
3. Uses machine learning to predict where future urban expansion is likely
4. Creates a susceptibility/risk map
5. Displays results in a Web GIS application

You are basically teaching the computer:

> “These are the characteristics of urban areas. Find other places that may become urban in the future.”

---

# Simple Explanation

Your project answers questions like:

* Which areas are most likely to become urbanized?
* Where may new buildings and roads appear?
* Which natural areas are under pressure from urban expansion?
* Which zones are suitable or unsuitable for future development?

---

# How the System Works

## Step 1 — Before vs After Images

You compare satellite images from different years:

* Before urbanization (example: 2015)
* After urbanization (example: 2025)

This helps identify urban expansion areas. 

---

## Step 2 — Create Training Points

You manually create:

| Type      | Label |
| --------- | ----- |
| Urban     | 1     |
| Non-Urban | 0     |

The ML model learns from these examples. 

---

## Step 3 — Collect Environmental Features

Your project uses factors affecting urban growth such as:

* NDVI
* NDBI
* Elevation
* Slope
* Distance to roads
* Population density
* Night lights
* Temperature
* Land use
* Distance to rivers

These layers already appear in your GEE scripts. 

---

## Step 4 — Train Machine Learning Models

You train models like:

* Random Forest
* SVM
* Decision Tree

The models learn the relationship between urban areas and environmental conditions. 

---

## Step 5 — Generate Susceptibility Map

The trained model predicts urban growth probability for every pixel.

Output example:

| Susceptibility Level | Meaning                         |
| -------------------- | ------------------------------- |
| High                 | Very likely future urban growth |
| Medium               | Possible growth                 |
| Low                  | Unlikely growth                 |

---

# What “Decision Support” Means

Your project is not only making maps.

It helps people make **better planning decisions**.

That is why it is called a:

> **Decision Support System (DSS)**

---

# Who Can Use Your System

Your web GIS system can help:

* city planners
* municipalities
* environmental agencies
* construction planners
* transportation planners
* disaster management authorities

---

# How It Helps Decision Making

## 1. Urban Planning

Officials can identify:

* where the city is expanding
* where future development may happen
* where infrastructure is needed

Example:
If the map shows high growth probability in western Karabük, planners may prepare roads and utilities there.

---

## 2. Environmental Protection

The system helps detect:

* forest areas under urban pressure
* agricultural land at risk
* green area reduction

This supports sustainable planning.

---

## 3. Infrastructure Planning

Authorities can decide where to build:

* roads
* schools
* hospitals
* drainage systems
* electricity networks

before uncontrolled urbanization happens.

---

## 4. Risk Reduction

Urban growth in dangerous areas can be identified early:

* steep slopes
* flood-prone zones
* landslide areas

This helps avoid unsafe construction.

---

## 5. Smart City Development

Your project supports:

* sustainable urban development
* smart land-use planning
* data-driven governance

instead of random city expansion.

---

# What Makes Your Project “GIS + ML”

## GIS Part

GIS handles:

* maps
* spatial layers
* satellite imagery
* raster analysis
* visualization

Examples from your work:

* NDVI maps
* slope maps
* land cover maps
* susceptibility maps

---

## Machine Learning Part

ML handles:

* pattern learning
* classification
* prediction
* susceptibility estimation

The ML model learns:
f(x)=P(urban\ growth\mid NDVI,NDBI,Slope,Elevation,Distance\ to\ Roads,...)

Meaning:

> Probability of urban growth depends on environmental and spatial factors.

---

# Final Output of Your Project

Your final system includes:

## 1. Susceptibility Map

Shows high/medium/low urban growth probability.

## 2. Interactive Web GIS App

Users can:

* zoom
* turn layers on/off
* click areas
* view risk levels
* compare years

## 3. Decision Support Tool

Helps planners make informed spatial decisions.

---

# In One Sentence

Your project is:

> A GIS and machine learning system that predicts future urban growth areas using satellite and environmental data to support smarter urban planning and decision-making.
