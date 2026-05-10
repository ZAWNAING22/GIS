A **shapefile** isn’t just one file — it’s actually a **set of files** that together describe your spatial data. When you export or save a shapefile, you’ll see multiple files with the same name but different extensions. Here’s what each does:

---

## 📂 Core Shapefile Components
- **`.shp`** → the main file that stores the geometry (points, lines, polygons).  
- **`.shx`** → the index file that links geometry to attributes.  
- **`.dbf`** → the attribute table in dBASE format (columns + rows of data linked to each geometry).  

These three are **mandatory** — without them, the shapefile won’t work.

---

## 📂 Optional / Supporting Files
- **`.prj`** → projection file (stores coordinate system info, e.g., WGS84 or UTM).  
- **`.cpg`** → code page file (defines character encoding for text in the `.dbf`).  
- **`.qpj`** → alternative projection file used by some GIS software.  
- **`.sbn` / `.sbx`** → spatial index files (speed up queries).  
- **`.xml`** → metadata file (describes dataset contents).

---

## 🧩 How They Work Together
- The **`.shp`** holds the shapes.  
- The **`.dbf`** holds the attributes (like your “Probability” column).  
- The **`.shx`** ties them together.  
- The **`.prj`** ensures your data aligns correctly on the map.  

So when you share or move a shapefile, you must include **all these files together** in the same folder.

---

👉 In your case, when you saved `Karabuk_Propability.shp`, you actually created a bundle:  
`Karabuk_Propability.shp`, `Karabuk_Propability.shx`, `Karabuk_Propability.dbf`, and ideally `Karabuk_Propability.prj`.  

Would you like me to show you how to **inspect the `.dbf` table directly in Python** (so you can confirm your “Probability” values are stored correctly before rasterizing)?
