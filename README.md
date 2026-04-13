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

# Support the project

- Many geocoding solutions are subscription-based, and free offline locators are rare.
- This project provides free offline geocoding locators built from open data.
- Building and maintaining these locators requires significant time and computing resources.  
- If they are useful for your workflows, you can support future locator development here:

[![Sponsor](https://img.shields.io/badge/Sponsor-Support%20locator%20development-pink?style=for-the-badge)](https://revolut.me/andriuqo9t)

---

# Current coverage

Available datasets:

Regional geolocator datasets are archived on Zenodo and can be downloaded here:

[![Locators Europe](https://img.shields.io/badge/Locators-Europe-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19282045)

[![Locators North America](https://img.shields.io/badge/Locators-North%20America-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19457691)

[![Locators Central America](https://img.shields.io/badge/Locators-Central%20America-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19475229)

[![Locators South America](https://img.shields.io/badge/Locators-South%20America-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19480756)

[![Locators Africa](https://img.shields.io/badge/Locators-Africa-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19480842)

[![Locators Asia](https://img.shields.io/badge/Locators-Asia-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19496593)

[![Locators Australia and Oceania](https://img.shields.io/badge/Locators-Australia%20and%20Oceania-blue?style=for-the-badge&logo=zenodo)](https://doi.org/10.5281/zenodo.19501614)

This repository serves as the documentation hub for locator datasets published via Zenodo.

---

# Workflow overview

The locator build pipeline is a fully automated, production-grade geospatial **ETL** system designed for global-scale offline geocoding in **ArcGIS Pro** ecosystem.

The architecture is modular and consists of four core stages: data ingestion, spatial transformation, geospatial enrichment, and locator deployment. This design ensures full reproducibility, scalability, and consistent OpenStreetMap (**OSM**)-based address coverage.

1. Data ingestion (**OSM PBF** parsing).
OpenStreetMap **PBF** datasets are processed using `osmium`, to extract raw address entities, street geometries, and associated metadata.

3. Spatial data standardisation (**GeoPackage** generation).
Extracted features are normalised and converted into **GeoPackage** format using `fiona` and `shapely`, ensuring geometry consistency and **WGS84** coordinate integrity.

4. Address intelligence and interpolation engine.
A custom geocoding engine interpolates house number ranges along street segments, generating complete left and right side address coverage and forming continuous addressable networks.

5. Spatial enrichment and administrative integration.
Features are enriched using `geopandas` spatial joins, integrating postal codes and hierarchical administrative boundaries (region/subregion structures) into a unified address model.

6. **File Geodatabase** conversion layer.
Processed **GeoPackage**  datasets are converted into **File Geodatabase** using **ArcGIS Pro** `arcpy`, for native compatibility with the **ArcGIS Pro** geocoding framework.

7. Locator synthesis and metadata generation.
Final **ArcGIS Pro** locators (**.LOC/.LOZ** formats) are generated using the **ArcGIS Pro** locator engine with automated metadata injection, including language codes, country codes, and usage constraints.

The entire **ETL** pipeline operates in an iterative, file-by-file processing mode, enabling scalable execution across large geospatial datasets without requiring full dataset loading into memory.

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

Locator datasets must **not** be presented as Esri Inc. products.

---

# Technical notes

- Addresses are extracted from OpenStreetMap nodes and streets, keeping street names, house numbers, cities, postal codes, and country information.
- Street shapes are saved as lines, and house numbers along each street are interpolated for both sides of the road to create number ranges.
- All addresses and streets are exported to GeoPackage files and then converted to ArcGIS Pro geodatabases.
- LOC files include metadata, summaries, tags, and usage notes, making sure everything is properly documented.
- Designed for **offline table geocoding**, providing full address coverage for geocoding tasks.

---

# Disclaimer

- This project is not affiliated with Esri Inc.
- ArcGIS Pro requires a valid Esri Inc. license.  
- Generated LOC and LOZ files are Esri Inc. proprietary format and require Esri Inc. software to create or use.
- Data accuracy depends on OpenStreetMap and other open datasets.  
- The author assumes no responsibility for geocoding errors or workflow results.

---

# Author

© Andrius Kučas, 2026
