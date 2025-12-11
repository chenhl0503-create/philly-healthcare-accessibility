# Beyond Distance: Spatial Accessibility and Equity of Healthcare During COVID-19
### A Case Study of Philadelphia

**Author:** Haolong Chen  
**Course:** UPenn CPLN 5080 Urban Research Methods  
**Date:** December 8, 2025

---

## 📖 Project Overview

COVID-19 acted as a "stress test" for urban healthcare systems. When mobility is restricted, traditional metrics like "20-minute driving catchments" become unrealistic for low-income, car-less, and essential workers.

This project investigates the **"Philadelphia Paradox"**: a city with world-class hospitals (UPenn, Jefferson) that still suffers from severe health disparities by neighborhood and race. Moving beyond simple Euclidean distance, this research uses the **Enhanced Two-Step Floating Catchment Area (E2SFCA)** method to quantify the disparity between *theoretical access* (all hospitals) and *actual access* (Medicaid-accepting facilities) for vulnerable populations.

### 🎯 Research Questions

* **Diagnosis:** How does spatial accessibility vary when measured using realistic road networks and capacity constraints?
* **Equity:** Is accessibility equitably distributed, or does it systematically disadvantage socially vulnerable groups?
* **Intervention:** Where should new facilities be located to maximize impact for the most vulnerable?

---

## 🛠 Methodology

This project employs a multi-level spatial analysis framework using Python:

* **Level 1 (Baseline):** Nearest Neighbor Drive Time analysis using OpenStreetMap (OSM) networks.
* **Level 2 (Core Analysis):** Implementation of **E2SFCA** (Enhanced 2-Step Floating Catchment Area) with Gaussian distance decay to measure supply-to-demand ratios.
* **Correction:** Application of buffer zones (including hospitals in NJ and PA suburbs) to eliminate **Edge Effects**.
* **Level 3 (Equity):** Integration of the **CDC Social Vulnerability Index (SVI)** to identify "Medical Deserts" (High SVI + Low Access).
* **Level 4 (Optimization):** Development of a "Priority Index" (Gap × SVI) to recommend sites for new facilities.

---

## 📂 Repository Structure

```text
├── Data/                           # Raw geospatial and tabular data inputs 
├── cache/                          # OSMnx cache files for network graphs 
├── final_deliverables/             # Final publication-ready maps and legends 
│   └── publication_maps_v5/ 
├── project_outputs_optimized/      # Processed outputs and visualization assets 
├── results/                        # Intermediate analysis results (GeoJSONs, CSVs) 
├── .gitignore                      # Git ignore file 
├── Final_beta.ipynb                # MAIN JUPYTER NOTEBOOK (Source Code) 
└── README.md                       # Project documentation
