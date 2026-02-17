# Sendust-ml-featurization-SHAP
# Machine Learning-Guided Design of Sendust Alloys with SHAP Interpretation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)

> **Note:** This repository contains the code and data for the research paper:  
> *Interpretable Machine Learning for Functional Properties Prediction of Fe-Si-Al Alloys via Feature Engineering* (in preparation)

## Overview

This repository implements an interpretable machine learning framework for predicting magnetic and electrical properties of Fe-Si-Al (Sendust) soft magnetic alloys. The study combines:

- **Composition-based prediction** using chemical composition as features
- **Featurization methods**: matminer.WenAlloys and CBFV.oliynyk (Composition-Based Feature Vector by Oliynyk)
- **Feature selection** via Optuna with LightGBM
- **ML algorithms**: Random Forest Regressor, Extra Trees Regressor, Gradient Boosting Regressor, XGBoost
- **Interpretability**: SHAP (SHapley Additive exPlanations) analysis with SHAP beeswarm and custom Grid-SHAP visualization

### Target Properties

- **Coercivity** (A/m) — magnetic property
- **Saturation Polarization** (T) — magnetic property  
- **Resistivity** (μΩ·cm) — electrical property

## Key Features

- ML pipeline from raw composition to property prediction  
- Two featurization strategies with manual and automated feature selection  
- Model interpretability with SHAP beeswarm and Grid-SHAP visualizations  
- External validation on independent test set  
- Reproducible workflow with pre-trained models  

---

## Project Structure
### Data (`data/`)
- `external_validation/` — Dataset for external validation
- `raw/` — Data for featurization
- `training/` — Processed training data with selected features

### Models (`models/`)
36 trained models organized by method and property:
- `composition/` — Baseline models (composition only)
- `wenalloys/` — Models with WenAlloys features
- `oliynyk/` — Models with Oliynyk features

Each subdirectory contains models for 3 properties × 4 algorithms (RFR, ETR, GBR, XGB)

### Notebooks (`notebooks/`)
15 Jupyter notebooks covering:
- Data preprocessing for each method
- Feature extraction and selection (Optuna)
- Model training for all property-method combinations
- SHAP interpretation and validation

### Results (`results/`)
- `metrics/` — Model performance metrics (Excel files)
- `shap/` — SHAP visualizations
  - `beeswarm/` — SHAP beeswarm plots
  - `grid-shap/` — Grid-SHAP visualizations
- `validation/` — External validation predictions

### Scripts (`scripts/`)
- `wenalloys_corrected.py` — Updated WenAlloys featurization

---

**Properties:** Hc (Coercivity, A/m), Js (Saturation Polarization, T), rho (Resistivity, μΩ·cm)  
**Algorithms:** RFR (Random Forest Regressor), ETR (Extra Trees Regressor), GBR (Gradient Boosting Regressor), XGB (XGBoost)
