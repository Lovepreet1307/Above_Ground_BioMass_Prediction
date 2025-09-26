# Multi-Stage Hybrid Modeling for Above-Ground Biomass Estimation

This repository presents a machine learning framework for predicting forest **Above-Ground Biomass (AGB)** using remote sensing datasets (Landsat-8 and LiDAR) from the **Petawawa Research Forest (PRF), Canada**. The approach leverages **multi-stage modeling**, **feature selection techniques**, and **ensemble learning** to improve predictive performance.

---

# Problem Statement

Accurately estimating AGB is crucial for forest management and climate change mitigation. While traditional field-based measurements are accurate, they are resource-intensive. Remote sensing provides scalable alternatives, but challenges like feature redundancy, sensor variability, and overfitting persist.

This project addresses these challenges using:
- Baseline modeling,
- Systematic feature selection,
- Multi-model ensembling, and
- Meta-level learning.

---

# Project Workflow Overview

## 📂 Dataset Description

The study uses four distinct datasets derived from the PRF supersite:

1. **PRF-Landsat8-9**
   - **Description:** Raw Landsat-8 dataset with 9 features
   - **Features:** 6 spectral bands (B1–B5, B7) + 3 biophysical attributes (AREA, AGE, SITE_INDEX)
   - **Samples:** 624 plots
   - **Year:** 2000

2. **PRF-Landsat8-54**
   - **Description:** Engineered Landsat-8 dataset with polynomial features
   - **Features:** 9 raw features + 45 polynomial/interaction terms (total = 54)
   - **Samples:** 624 plots
   - **Year:** 2000

3. **PRF-LiDAR-36**
   - **Description:** LiDAR-derived structural metrics
   - **Features:** 36 structural features (height percentiles, distribution metrics)
   - **Samples:** 249 plots
   - **Collection:** Airborne Laser Scanning (ALS)

4. **PRF-LiDAR-702**
   - **Description:** High-dimensional LiDAR dataset with polynomial expansion
   - **Features:** 36 raw features + 666 polynomial/interaction terms (total = 702)
   - **Samples:** 249 plots
   - **Collection:** Airborne Laser Scanning (ALS)

---

## 🏗️ Project Architecture

### **Phase 1: Data Preprocessing**
- MinMax normalization to [0, 1] range  
- 90:10 train-test split  
- No missing value imputation required  

### **Phase 2: Baseline Modeling**
- Models:  
  - Linear Regression (LR)  
  - Random Forest Regressor (RF)  
  - XGBoost Regressor (XGB)  
- Evaluation: 10-fold cross-validation  
- Metrics: MAE, MSE, R²  

### **Phase 3: Stage 1 – Feature Selection & Base Model Training**
- **Feature Selection Methods:**
  - RF Importance (feature ranking from Random Forests)  
  - RFE with RF (Recursive Feature Elimination with RF estimator)  
  - XGB Importance (feature ranking from XGBoost)  
  - Hybrid RF-XGB (average of RF and XGB importance scores)  

- **Model Training:**
  - Train RF and XGB models on selected features  
  - Determine optimal feature count (k*) via cross-validation  
  - Perform hyperparameter tuning using GridSearchCV  
  - Build a pool of base models with varying feature subset sizes  

### **Phase 4: Stage 2 – Ensemble Modeling**
- **Random Model Averaging**
  - Average predictions from k randomly selected models  
  - Test different ensemble sizes (k = 10, 20, ..., K_max)  

- **Top-k Model Averaging**
  - Average predictions from k best-performing models (based on CV R²)  
  - Emphasizes high-performing base models  

- **Meta-Learning with Feature Selection**
  - Use Stage 1 predictions as meta-features  
  - Apply feature selection on the prediction matrix  
  - Train a Linear Regression meta-model on selected predictions  
  - Optimize subset size based on test performance  

# Requirements

To run this project, you need the following Python packages:

- numpy
- pandas
- scikit-learn
- xgboost
- joblib

---

