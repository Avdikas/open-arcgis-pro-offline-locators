# Open ArcGIS Pro Offline Locators

Open offline geocoding locators for ArcGIS Pro, created from OpenStreetMap (OSM). 
Datasets are published via Zenodo DOI and support full address matching for offline GIS workflows.
Locator addresses are stored in the local language of each country.

These locators support address matching including:

- Street name
- House number
- City
- Postal code
- Region / subregion hierarchy
- Country
- WGS84 coordinates

Designed specifically for **offline table geocoding workflows** in ArcGIS Pro and ArcGIS Enterprise.  
**Note:** These locators are not compatible with ArcGIS Desktop (ArcMap).

---

# Current coverage

Available datasets:

- Europe (Zenodo DOI coming soon)

Planned coverage expansion:

- North America
- South America
- Asia
- Africa
- Oceania

This repository serves as the documentation hub for locator datasets published via Zenodo.

---

# Workflow overview

The locator build pipeline:

1. **OSM PBF** -> extract addresses and streets with `osmium`  
2. Convert data to **GeoPackage** using `fiona` and `shapely`  
3. Interpolate house number ranges along streets using Python logic  
4. Add postal codes, region/subregion hierarchy using `geopandas` + spatial join  
5. Export **GeoPackage -> File Geodatabase** using `arcpy`  
6. Generate **LOC file** for ArcGIS Pro, with metadata filled  

Environment:

- Python 3.13.7  
- ArcGIS Pro 3.5.4  

Libraries used:

`osmium`, `shapely`, `fiona`, `geopandas`, `arcpy`, `tqdm`

This workflow ensures fully automated generation of address locators suitable for **table geocoding**.

---

# Data sources

Primary source:

© OpenStreetMap contributors  
https://www.openstreetmap.org

Downloads:

https://download.geofabrik.de/

---

# License

Locator datasets are derived from OpenStreetMap data and distributed under:

Open Database License (ODbL) 1.0  
https://opendatacommons.org/licenses/odbl/1.0/

Required attribution:

© OpenStreetMap contributors

Repository documentation and workflow descriptions:

MIT License

---

# Usage

Locator datasets may be used:

- Offline
- In research
- In production GIS workflows
- Commercially

Attribution must be preserved:

© OpenStreetMap contributors

Locator datasets must **not** be presented as ESRI inc. products.

---

# Technical notes

- Addresses are smartly extracted from OpenStreetMap nodes and streets, keeping street names, house numbers, cities, postal codes, and country information.
- Street shapes are saved as lines, and house numbers along each street are interpolated for both sides of the road to create number ranges.
- All addresses and streets are exported to GeoPackage files and then converted to ArcGIS Pro geodatabases.
- LOC files include metadata, summaries, tags, and usage notes, making sure everything is properly documented.
- Designed for **offline table geocoding**, providing full address coverage for geocoding tasks.

---

# Disclaimer

- This project is not affiliated with ESRI inc.
- ArcGIS Pro requires a valid ESRI inc. license.  
- Generated LOC and LOZ files are ESRI proprietary format and require ESRI inc. software to create or use.
- Data accuracy depends on OpenStreetMap and other open datasets.  
- The author assumes no responsibility for geocoding errors or workflow results.

---

# Support the project

- There are many subscription-based geocoding services, and free offline locators are rare or often nonexistent.
- This project provides free, offline geocoding locators based on open data.
- These locators serve as a lifeline where no locators exist and provide a tangible alternative in places where commercial locators are available and open data quality is high.

If it helps your work, you can support future locator development here:

Revolut: https://revolut.me/andriuqo9t

Support is optional but helps expand locator coverage.

---

# Author

© Andrius Kučas, 2026
