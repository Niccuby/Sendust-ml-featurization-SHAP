# Sendust-ml-featurization-SHAP
# Machine Learning-Guided Design of Sendust Alloys with SHAP Interpretation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

> **Note:** This repository contains the code and data for the research paper:  
> *Interpretable Machine Learning for Functional Properties Prediction of Fe-Si-Al Alloys via Feature Engineering* (in preparation)

## Overview

This repository implements an interpretable machine learning framework for predicting magnetic and electrical properties of Fe-Si-Al (Sendust) soft magnetic alloys. The study combines:

- **Composition-based prediction** using chemical composition as features
- **Featurization methods**: WenAlloys and CBFV (Composition-Based Feature Vector by Oliynyk)
- **Feature selection** via Optuna with LightGBM
- **ML algorithms**: Random Forest, Extra Trees, Gradient Boosting, XGBoost
- **Interpretability**: SHAP (SHapley Additive exPlanations) analysis with custom Grid-SHAP visualization

### Target Properties

- **Coercivity** (A/m) — magnetic property
- **Saturation Polarization** (T) — magnetic property  
- **Resistivity** (Ω·cm) — electrical property

## Key Features

✅ Comprehensive ML pipeline from raw composition to property prediction  
✅ Two featurization strategies with manual automated feature selection  
✅ Model interpretability with SHAP beeswarm and Grid-SHAP visualizations  
✅ External validation on independent test set  
✅ Reproducible workflow with pre-trained models  

---

## Project Structure
Sendust-ml-featurization-SHAP/
│
├── data/
│ ├── external_validation/ # Dataset for external validation
│ ├── raw/ # Data for featurization
│ └── training/ # Processed training data with selected features
│
├── models/ # Trained models (36 total: 3 methods × 3 properties × 4 algorithms)
│ ├── composition/ # Baseline models (composition only)
│ ├── wenalloys/ # Models with WenAlloys features
│ └── oliynyk/ # Models with CBFV features
│ └── [property]/ # Subdirectories: coercivity, saturation_polarization, resistivity
│
├── notebooks/ # Jupyter notebooks (15 total)
│ ├── preprocessing_.ipynb # Data preprocessing for each method
│ ├── oliynyk_optuna_fs.ipynb # Optuna feature selection
│ ├── 1-3_composition_.ipynb # Baseline training (3 properties)
│ ├── 4-6_wenalloys_.ipynb # WenAlloys training (3 properties)
│ ├── 7-9_oliynyk_.ipynb # CBFV training (3 properties)
│ └── 10-12_oliynyk_*_extraction.ipynb # Feature extraction
│
├── results/
│ ├── metrics/ # Model performance metrics (.xlsx files)
│ │ ├── composition/
│ │ ├── wenalloys/
│ │ └── oliynyk/
│ │
│ ├── shap/ # SHAP interpretability visualizations
│ │ ├── beeswarm/ # SHAP beeswarm plots (wenalloys, oliynyk)
│ │ └── grid-shap/ # Grid-SHAP plots (composition, wenalloys, oliynyk)
│ │
│ └── validation/ # External validation predictions
│ ├── predictions_all.xlsx
│ └── [method]/ # Per-method validation results
│
├── scripts/
│ └── wenalloys_corrected.py # WenAlloys featurization utility
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
**Properties:** Hc (Coercivity), Js (Saturation Polarization), rho (Resistivity)  
**Algorithms:** RFR (Random Forest), ETR (Extra Trees), GBR (Gradient Boosting), XGB (XGBoost)
