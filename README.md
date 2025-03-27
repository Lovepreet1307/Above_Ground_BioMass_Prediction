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

# Stage 1: Baseline and Feature-Optimized Modeling

- **Purpose**: Train individual models on the original datasets using various feature selection techniques to generate predictions and metrics.
- **Key Steps**:
  1. **Data Splitting**: Dataset is split into training and test sets.
  2. **Feature Selection Techniques**:
     - **Random Forest (RF)** feature importance
     - **RFE with RF**
     - **XGBoost feature importance**
     - **Hybrid (RF + XGB)**
  3. **Model Training**:
     - Trains models such as **Random Forest** and **XGBoost** on top-k selected features.
     - Performs **K-Fold Cross-Validation** to select best feature subset size (`k`).
  4. **Model Saving**:
     - Saves trained models and selected features.
     - Stores predictions on both training and test sets.
     - Outputs performance metrics (MAE, MSE, R²).

# Stage 2: Meta-Level Modeling

The predictions from Stage 1 models are used as features for a second-stage prediction.

# Landsat-8 Dataset
- **Meta-models trained on first-stage predictions**:
  - **Random Forest**
  - **Gradient Boosting**
  - **Linear Regression**
  - **Averaging Ensemble** (mean of all model predictions)
- **Feature Selection** is also applied to Stage 1 predictions.

# LiDAR Dataset
- **Simple Averaging** of predictions from Stage 1 models is used.
  - No second-stage meta-models are trained.
  - This approach stabilizes predictions and reduces overfitting.


---

