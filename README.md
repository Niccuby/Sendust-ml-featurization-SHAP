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
