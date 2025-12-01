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

# Baseline Modeling

For each dataset, we begin by training the following **baseline models** using the full feature set:
- **Linear Regression (LR)**
- **Random Forest Regressor (RF)**
- **XGBoost Regressor (XGB)**

These models serve as performance references.

# Stage 1: Feature Selection + Optimized Model Training

This stage involves:
1. **Feature Selection Methods**:
   - **Random Forest (RF) importance**
   - **RFE with RF**
   - **XGBoost importance**
   - **Hybrid method (average of RF and XGB)**
2. **Model Training**:
   - Each feature subset is evaluated using:
     - **Random Forest**
     - **XGBoost**
   - Models are trained using **K-Fold Cross-Validation**.
   - Optimal number of top-k features is selected based on MAE, MSE, or R².
3. **Outputs**:
   - Trained models (`.pkl`)
   - Selected features (`.json`)
   - Predictions (`cv_train_predictions.csv`)
   - Performance metrics (`.csv`)

# Stage 2: Meta-Level Modeling

The predictions from Stage 1 models are used as features for a second-stage prediction.

# Landsat-8 Dataset
- **Meta-models trained on first-stage predictions**:
  - **Random Forest**
  - **Gradient Boosting**
  - **Linear Regression**
  - **Simple Averaging** of predictions from Stage 1 models is used.
- **Feature Selection** is also applied to Stage 1 predictions.

# LiDAR Dataset
- **Simple Averaging** of predictions from Stage 1 models is used.
  - No second-stage meta-models are trained.
  - This approach stabilizes predictions and reduces overfitting.


---

