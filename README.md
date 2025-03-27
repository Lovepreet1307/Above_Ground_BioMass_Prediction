# Multi-Stage Hybrid Modeling for Above-Ground Biomass Estimation

This repository presents a machine learning framework for predicting forest **Above-Ground Biomass (AGB)** using remote sensing datasets (Landsat-8 and LiDAR) from the **Petawawa Research Forest (PRF), Canada**. The approach leverages **multi-stage modeling**, **feature selection techniques**, and **ensemble learning** to improve predictive performance.

---

# Project Workflow Overview

The complete pipeline consists of two main stages:

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

- **Purpose**: Combine predictions from Stage 1 to build a second-stage model.
- **Approaches Used**:
  - **Landsat-8**:
    - Performs additional feature selection on Stage 1 model predictions.
    - Trains meta-models: **Random Forest**, **Gradient Boosting**, and **Linear Regression**.
  - **LiDAR**:
    - Uses **simple averaging** of Stage 1 predictions to reduce error and improve generalization.
- **Outputs**:
  - Test set predictions
  - Final performance metrics
  - Final saved models for deployment

---

