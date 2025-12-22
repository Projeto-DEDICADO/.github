# 🛰️ DEDICADO System

**Detection of Forest Disturbances Using Algorithms Developed for Earth Observation Image Time Series**

<img width="719" height="618" alt="DEDICADO workflow overview" src="https://github.com/user-attachments/assets/4160cbc8-0a22-4de7-8888-080534b05270" />

---

## 💡 Overview and Objectives

The **DEDICADO System** is a research and development initiative focused on advancing **environmental monitoring** through the integration of **remote sensing**, **time series analysis**, and **artificial intelligence**.

The project aims to design, evaluate, and implement **automatic forest disturbance detection algorithms** operating in **near real-time**, with primary application over the **Brazilian Legal Amazon (BLA)** and the **Cerrado biome**.

DEDICADO emphasizes the combined use of **spatial and temporal patterns** extracted from Earth Observation image time series to generate **high-accuracy forest disturbance alerts**, supporting monitoring, research, and decision-making activities.

---

## 🎯 Main Goals

The core objectives of the DEDICADO System are:

- To build robust **reference datasets** representing multiple forest disturbance agents, regions, and time periods;
- To **systematically evaluate existing forest monitoring systems**, including PRODES, DETER, GLAD, RADD, TropiSCO, and others;
- To investigate the impact of **spatial, temporal, and spectral resolutions**, sensor technologies, and contextual information on detection performance;
- To identify and test **automatic disturbance detection methods** suitable for near real-time operation;
- To implement algorithms that achieve the **best trade-off between detection accuracy and computational efficiency**;
- To provide **open-source implementations and documentation**, including uncertainty assessments by region, season, and disturbance type.

---

## 🧭 Project Scope and Conceptual Architecture

DEDICADO is designed as a **modular system**, structured around three main conceptual components:

1. **Reference Sample Construction**  
   Creation and validation of disturbance and non-disturbance samples using multiple independent monitoring systems.

2. **Alert Generation Algorithms**  
   Development of automatic detection methods that generate spatially explicit forest disturbance alerts.

3. **Time Series Analysis of Alerts**  
   Analysis of the temporal behavior, consistency, and evolution of detected alerts using satellite image time series.

This repository serves as the **central project hub**, while specific components are implemented in dedicated repositories (see below).

---

## 🛠️ Technical Focus and Key Technologies

DEDICADO operates at the intersection of multiple advanced research areas and handles large volumes of Earth Observation data.

| Category | Key Topics |
|--------|-----------|
| **Application Domain** | Environmental Monitoring, Forest Disturbance Detection |
| **Data** | Satellite Image **Time Series**, **Analysis Ready Data (ARD)**, Large-scale mosaics |
| **Methods** | Artificial Intelligence, Machine Learning, Remote Sensing, Time Series Analysis |
| **Scale** | Regional to biome-wide (BLA and Cerrado) |

---

## 🧪 Development Workflow

The development of the DEDICADO System follows a structured and iterative workflow:

1. **Reference Sample Collection**  
   Collection of training and validation samples representing diverse forest disturbance agents, regions, and periods.

2. **Evaluation of Existing Systems**  
   Quantitative assessment of PRODES, DETER, GLAD, RADD, TropiSCO, and related systems, considering accuracy, sensor characteristics, and classification approaches.

3. **Parameter and Resolution Testing**  
   Evaluation of different spatial, temporal, and spectral resolutions, sensor technologies, and contextual features using multiple detection architectures (pixel-based, window-based, hierarchical).

4. **Method Selection**  
   Identification and testing of candidate methods with strong potential for **automatic near real-time detection**.

5. **Algorithm Implementation**  
   Development of the final detection algorithm, prioritizing **accuracy, robustness, and computational performance**.

6. **Documentation and Open Access**  
   Preparation of detailed documentation and publication of open-source code in INPE repositories, including uncertainty characterization.

---

## 🧩 Reference Sample Construction (Stage 1)

The first development stage focuses on building a high-quality **reference dataset** containing both disturbance and non-disturbance samples, derived from multiple official monitoring systems.

### 1.1 Data Processing Workflow (R-based)

The reference data pipeline involves harmonizing heterogeneous datasets with different spatial resolutions, temporal coverage, and data formats.

| Step | R Packages / Tools | Description |
|----|-------------------|-------------|
| **Initial Data Acquisition** | `terra`, STAC APIs | Partition the study area into large image tiles and intersect them with the BLA boundary. |
| **Reference Data Collection** | `terra`, `sf` | Retrieve GLAD and RADD detections within each tile. |
| **Data Harmonization** | `terra` | Reproject and resample GLAD/RADD products to match PRODES/DETER spatial standards. |
| **Hierarchical Tiling Strategy** | Custom R scripts | Split tiles into subtiles and sub-subtiles (tile → tile/4 → tile/16) to ensure memory-efficient processing. |
| **PRODES/DETER Integration** | R spatial libraries | Load consolidated PRODES and DETER vector datasets for comparison and validation. |

---

### 1.2 Validation and Sampling Logic

Validation is performed at the **sub-subtile level** to maximize spatial consistency:

1. Each sub-subtile is divided into **100 validation cells**;
2. Disturbances detected by **GLAD + RADD** and **PRODES + DETER** are spatially compared;
3. Classification rules:
   - **Confirmed Disturbance (High Confidence):**  
     Detected by all four systems **or** detected by PRODES + DETER but not by GLAD + RADD;
   - **Potential False Positives:**  
     Detected by GLAD + RADD but not by PRODES + DETER, requiring manual or semi-automatic verification;
4. For each sub-subtile, **three disturbance samples** and **three stable forest samples** are selected after validation.

---

## 💻 Technology Stack

DEDICADO is primarily developed in **R**, leveraging high-performance spatial and data science libraries:

| R Package | Main Purpose |
|---------|--------------|
| `terra` | High-performance raster data processing and analysis |
| `sf` | Vector data manipulation and spatial operations |
| `mapview` | Interactive visualization of raster and vector layers |
| `tidyverse` | Data manipulation, analysis, and visualization |

---

## 📦 Repository Structure

This repository acts as the **umbrella project repository**.

Planned and related repositories include:

- **Alert Table Construction**  
  Repository dedicated to generating, organizing, and validating forest disturbance alert tables.

- **Alert Time Series Analysis**  
  Repository focused on analyzing the temporal dynamics of alerts using satellite image time series.

Links will be added as these repositories become available.

---

## 🔗 Useful Links

### 🌍 Forest Monitoring Systems
- **PRODES (INPE)** – Official Brazilian deforestation monitoring program  
  https://www.obt.inpe.br/OBT/assuntos/programas/amazonia/prodes

- **DETER (INPE)** – Near real-time deforestation detection system  
  https://www.obt.inpe.br/OBT/assuntos/programas/amazonia/deter

- **GLAD Alerts (University of Maryland)** – Global forest disturbance alerts  
  https://glad.umd.edu

- **RADD Alerts (Wageningen University & Research)** – Radar-based deforestation alerts  
  https://www.raddalerts.org

- **TropiSCO** – Tropical forest disturbance monitoring initiative  
  https://tropisco.org

---

### 🛰️ Earth Observation Data Sources
- **Sentinel-1 / Sentinel-2 (ESA Copernicus Programme)**  
  https://sentinel.esa.int

- **Landsat Collection (USGS / NASA)**  
  https://www.usgs.gov/landsat-missions

- **Brazil Data Cube (INPE)** – Analysis Ready Data for Brazil  
  https://brazildatacube.org

---

### 🧠 Time Series and Change Detection
- **LandTrendr** – Time series change detection framework  
  https://emapr.github.io/LT-GEE

- **BFAST** – Breaks For Additive Season and Trend  
  https://bfast.r-forge.r-project.org

- **CCDC** – Continuous Change Detection and Classification  
  https://github.com/klh5/CCDC

---

### 🧰 Tools and Libraries
- **R Project for Statistical Computing**  
  https://www.r-project.org

- **terra (R package)** – Raster data processing  
  https://rspatial.org/terra

- **sf (R package)** – Simple features for spatial data  
  https://r-spatial.github.io/sf

- **STAC Specification** – SpatioTemporal Asset Catalogs  
  https://stacspec.org

---

## 🤝 Contributing

Researchers, developers, and remote sensing specialists are welcome to contribute.  
Feel free to open an *Issue* for discussions or submit a *Pull Request*.

---

## 🔗 Related Repositories and Resources

- [INPE official repository – to be linked when available]
