According to your teacher’s requirements in the PDF, the web part is mainly for:

* visualizing the susceptibility map
* interacting with GIS layers
* allowing users to explore risk areas

It does NOT need to be a complex professional system.

From the project document: the web app should let users:

* define/view areas of interest
* visualize susceptibility/risk maps
* interact with layers and scenarios 

For your urban growth version, you can adapt this into a simple and clean Web GIS application.

# BEST SIMPLE WEB APP STRUCTURE

Use:

* HTML
* CSS
* JavaScript
* [Leaflet.js](https://leafletjs.com?utm_source=chatgpt.com)

This is enough for a student GIS project.

---

# WHAT YOUR WEB APP SHOULD SHOW

## 1. Base Map

Use:

* OpenStreetMap
* satellite layer

Example:

* city roads
* buildings
* terrain

---

# 2. Urban Growth Susceptibility Layer

Main output layer.

Show:

* High growth risk → red
* Medium → orange
* Low → green

This is your ML prediction map.

MOST IMPORTANT PART.

---

# 3. Before vs After Layers

Show:

* 2015 urban image
* 2025 urban image

Use layer switcher.

Teacher will like this a lot because it clearly shows change.

---

# 4. Interactive Popup

When clicking map:

Show:

* susceptibility level
* NDVI
* NDBI
* land type

Example popup:

```text id="3f9bfs"
Location Info
Risk: High
NDVI: 0.21
NDBI: 0.67
Class: Urban
```

---

# 5. Layer Control

Allow user to toggle:

☑ Urban growth map
☑ 2015 image
☑ 2025 image
☑ Roads
☑ Rivers

Very easy in Leaflet.

---

# 6. Legend

Required for GIS professionalism.

Example:

```text id="b45ueh"
Red = High Growth
Orange = Medium
Green = Low
```

---

# 7. Zoom + Pan

Leaflet already provides this automatically.

---

# BEST MINIMUM VERSION

If short on time, your app only needs:

✅ base map
✅ susceptibility map
✅ layer switcher
✅ legend
✅ popup

This is already acceptable.

---

# HOW YOUR FINAL WEB APP FLOW LOOKS

## User opens web app

Sees:

* map of Karabük

Then:

* turns on susceptibility layer
* clicks area
* sees growth risk
* compares 2015 vs 2025

That already satisfies most teacher expectations.

---

# SIMPLE WEB LAYOUT

```text id="rqqvbw"
--------------------------------
| Title: Urban Growth System |
--------------------------------
| Layer Control              |
| ☑ Risk Map                 |
| ☑ 2015                     |
| ☑ 2025                     |
--------------------------------
|                            |
|         MAP AREA           |
|                            |
--------------------------------
| Legend                     |
--------------------------------
```

---

# IMPORTANT

Teacher is grading:

* GIS workflow
* ML integration
* visualization
* interactivity

NOT:

* beautiful frontend design
* advanced backend
* enterprise software

So keep it:

* clean
* functional
* understandable

That is the winning strategy for this course project.
