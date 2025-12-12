# Beyond Distance: Spatial Accessibility and Equity of Healthcare During COVID-19
### A Case Study of Philadelphia

**Author:** Haolong Chen  
**Course:** UPenn MUSA 5500 Geospatial Data Science in Python  
**Date:** December 12, 2025

---

## 🚀 Live Website

## Note on Deliverables (Panel Site vs Quarto Site)

The **primary deliverable** for this project is the original Panel-exported interactive website:

- Main site (full interactive dashboard):  
  https://chenhl0503-create.github.io/philly-healthcare-accessibility/

After realizing the course write-up rubric explicitly mentions a **multi-page Quarto site**, I also created a **separate Quarto-based documentation site**:

- Quarto site (multi-page documentation, lighter content):  
  https://chenhl0503-create.github.io/philly-healthcare-accessibility/quarto_site/

**Important:** The Quarto site is intentionally shorter and more “documentation-style”.  
For evaluation of the full technical implementation, interactivity, and final storytelling, please use the **main Panel site** as the core basis.


---

## 📖 Project Overview

COVID-19 acted as a stress test for urban healthcare systems. When mobility is restricted, traditional metrics such as “20-minute driving catchments” become unrealistic for low-income, carless, and essential workers.

This project investigates the **“Philadelphia Paradox”**: a city with world-class hospitals (Penn, Jefferson) that still suffers from severe health disparities by neighborhood and race. Moving beyond simple Euclidean distance, the analysis uses an **Enhanced Two-Step Floating Catchment Area (E2SFCA)** model to quantify the gap between:

* **Theoretical access:** All hospitals reachable on a driving network.
* **Actual access:** The subset of facilities that accept Medicaid, specifically for socially vulnerable populations.

The final product is the **Philadelphia Healthcare Equity Explorer**, a web-based dashboard that combines E2SFCA accessibility surfaces, Social Vulnerability Index (SVI), clustering, and priority indices to highlight who loses access, where, and by how much.

---

## 🎯 Research Questions

The project is organized around three core research questions:

* **RQ1 (Diagnosis):** How does spatial accessibility to acute healthcare facilities vary across Philadelphia when measured using a realistic road network and an E2SFCA travel time model under free-flow conditions?
* **RQ2 (Equity):** Is this accessibility equitably distributed, or does it systematically disadvantage socially vulnerable groups?
* **RQ3 (Intervention):** Where should new facilities be located to maximize impact for the most vulnerable?

---

## 🛠 Analytical Framework

This project employs a multi-level spatial analysis framework, implemented entirely in Python:

### Level 1: Baseline – Distance and p-median thinking
* Nearest-neighbor drive-time and simple distance-based thinking using an OSMnx driving network.
* This serves as a baseline and is used to debunk the **“distance myth”**: proximity to a hospital does not guarantee meaningful access.

### Level 2: Core – E2SFCA accessibility
* Implementation of the **Enhanced Two-Step Floating Catchment Area (E2SFCA)** model with Gaussian distance decay.
* Uses provider capacity (beds) and demand (population) to compute accessibility surfaces under free-flow conditions.
* **Edge-effect correction:** Application of a buffered bounding box (including hospitals in New Jersey and Pennsylvania suburbs) to eliminate artificial “deserts” caused purely by the study-area boundary.

### Level 4: Equity – SVI and Medicaid filters
* Integration of the **CDC Social Vulnerability Index (SVI)** and Medicaid acceptance to identify **“medical deserts”** where high vulnerability and low accessibility coincide.

### Level 3: Optimization – Priority index and siting logic
* Construction of a **Priority Index**:
    ```math
    Priority Index = Normalized Equity Gap \times Normalized SVI
    ```
* This surface is used to recommend candidate locations for new or expanded facilities.

---

## 📂 Repository Structure

```text
.
├── Data/                           # Raw geospatial and tabular data inputs
│   ├── raw/                        # Original inputs (ACS, SVI CSV, WorldPop, shapefiles)
│   └── processed/                  # Cleaned and merged tract-level datasets
├── results/                        # Intermediate analysis results (GeoJSONs, CSVs)
│   ├── final_E2SFCA_results.geojson
│   └── recommended_new_sites.geojson
├── docs/                           # GitHub Pages Website Source
│   └── index.html                  # The interactive dashboard file
├── Final_beta.ipynb                # MAIN JUPYTER NOTEBOOK (Source Code)
├── .gitignore                      # Git ignore file
└── README.md                       # Project documentation
```
## 💾 Data Sources

This analysis combines data collected from **4 distinct sources** using sophisticated methods (API, Scraping):

1. **Supply:**
   * **Hospitals:** OpenDataPhilly & CMS Hospital Compare (API/CSV).
   * **Health Centers:** Web scraped from `phila.gov` using `BeautifulSoup`.

2. **Demand:**
   * **Population:** US Census ACS 2021 via Census API.

3. **Network:**
   * **Roads:** OpenStreetMap drivable network via `OSMnx`.

4. **Equity:**
   * **SVI:** CDC Social Vulnerability Index 2020 (CSV).
   * **Policy:** HUD Qualified Census Tracts via ArcGIS REST API.

---

## 💻 How to Run

1. Clone this repository.

2. Make sure you have the required Python libraries installed:

   ```bash
   pip install geopandas osmnx panel hvplot holoviews rasterio scikit-learn requests beautifulsoup4

