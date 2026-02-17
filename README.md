# 🌍 Urban Land-Cover Classification – London  
### Sentinel-2 + Random Forest (Geospatial AI Project)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnbkoloth/sentinel2-landcover-classification-london/blob/main/london_landcover_ml.ipynb)

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Random%20Forest-green)
![Remote Sensing](https://img.shields.io/badge/Data-Sentinel--2-orange)
![Geospatial AI](https://img.shields.io/badge/Field-Geospatial%20Artificial%20Intelligence-purple)

---

## 📌 Overview

This project demonstrates supervised machine learning applied to multi-spectral Sentinel-2 satellite imagery for multi-class urban land-cover classification in London, UK.

Using spectral indices and ensemble learning techniques, the model classifies land into:

- 🌱 Vegetation  
- 🌊 Water  
- 🏙 Built-up / Urban  

The workflow reflects a practical Geospatial Artificial Intelligence pipeline, including preprocessing, spectral feature engineering, supervised classification, model evaluation, and spatial interpretation.

---

## 🛰 Data Source

**Sentinel-2 Level-2A Surface Reflectance Imagery**  
Copernicus Open Access Hub  

- Tile: T30UXC (London)  
- Spatial Resolution: 10 metres  
- Acquisition Date: February (winter conditions)

### Bands Used
- B02 – Blue  
- B03 – Green  
- B04 – Red  
- B08 – Near Infrared (NIR)  

Level-2A data is provided as scaled reflectance (reflectance × 10000), requiring correction before analysis.

---

## 🧠 Methodology

### 1️⃣ Preprocessing
- Reflectance scaling correction (division by 10000)
- Cropping to defined study region
- Spectral feature extraction

### 2️⃣ Spectral Indices

**NDVI (Vegetation Detection)**  
\[
NDVI = \frac{NIR - Red}{NIR + Red}
\]

**NDWI (Water Detection)**  
\[
NDWI = \frac{Green - NIR}{Green + NIR}
\]

These indices enhance spectral separability between vegetation, water, and urban materials.

---

### 3️⃣ Multi-Class Label Generation

Spectrally informed proxy labels were generated:

- Vegetation → NDVI > 0.4  
- Water → NDWI > 0.05  
- Built-up → Remaining pixels  

These labels serve as training masks rather than manually annotated ground truth.

---

### 4️⃣ Feature Engineering

Input features:
- Blue
- Green
- Red
- NIR

NDVI was excluded from training features to avoid data leakage.

---

### 5️⃣ Model Training

- Algorithm: Random Forest Classifier  
- Ensemble size: 100 trees  
- Subsampled training set (100,000 pixels)  
- 70/30 train-test split  
- Parallel processing enabled (`n_jobs=-1`)

Subsampling improves computational efficiency while preserving class representativeness.

---

## 📊 Results

The classifier demonstrates strong separability between vegetation, water, and built-up areas.

### Key Observations:

- High precision and recall for vegetation
- Slight confusion between water and built surfaces (urban spectral similarity)
- Built-up class dominant but well separated
- NIR identified as the most informative spectral band

The River Thames is clearly identified in the final classified output.

---

## 🔬 Feature Importance

NIR reflectance dominates classification performance, aligning with established remote sensing theory regarding vegetation spectral behaviour.

This confirms physical consistency between the model and spectral principles.

---

## ⚠ Limitations

- Training labels are spectrally derived, not manually annotated
- Class imbalance present (urban dominant)
- Winter imagery reduces vegetation contrast
- SWIR bands were not included

---

## 🚀 Future Improvements

- Incorporate SWIR bands for improved water discrimination  
- Add manually labelled training polygons  
- Compute Cohen’s Kappa statistic  
- Compare Random Forest with Logistic Regression or CNN models  
- Perform multi-temporal land-cover analysis  

---

## 🛠 Technologies Used

- Python  
- NumPy  
- Rasterio  
- Scikit-learn  
- Matplotlib  
- Seaborn  
