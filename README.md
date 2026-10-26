# Sendust-ml-featurization-SHAP
# Machine Learning-Guided Design of Sendust Alloys with SHAP Interpretation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)

> **Note:** This repository contains the code and data for the research paper:  
> *Interpretable machine learning for functional properties prediction of Fe–Si–Al alloys via feature engineering*,
> published in *Journal of Materials Science* [https://doi.org/10.1007/s10853-026-12999-z]

## Overview

This repository implements an interpretable machine learning framework for predicting magnetic and electrical properties of Fe-Si-Al (Sendust) soft magnetic alloys. The study combines:

- **Composition-based prediction** using chemical composition as features
- **Featurization methods**: matminer.WenAlloys and CBFV.oliynyk (Composition-Based Feature Vector by Oliynyk)
- **Feature selection** via Optuna with LightGBM
- **ML algorithms**: Random Forest Regressor, Extra Trees Regressor, Gradient Boosting Regressor, XGBoost
- **Interpretability**: SHAP (SHapley Additive exPlanations) analysis with SHAP beeswarm and custom Grid-SHAP visualization

<p align="center">
  <img src="assets/workflow_figure.png" alt="ML Pipeline Workflow" width="800"/>
  <br>
  <em>Overall workflow: from data processing and feature engineering to model interpretation and validation.</em>
  <br>
  <em>This repository contains the full implementation code for the pipeline shown above.</em>
</p>

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
- `splits/` — Saved folds for cross validation
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

<details>
<summary><strong>Notebooks (`notebooks/`)</strong></summary>

15 Jupyter notebooks covering the full ML pipeline — from raw composition data
to model training, feature engineering, feature selection, and SHAP interpretation.

---

#### Step 1 — Composition-Based Baseline Models

Training and evaluation using raw chemical composition (Fe, Si, Al fractions) as features.
Four regression algorithms (RFR, ETR, GBR, XGB) are trained and validated
with tuned hyperparameters for each target property.

| Notebook | Target Property |
|---|---|
| `01_composition_Hc.ipynb` | Coercivity (A/m) |
| `02_composition_Js.ipynb` | Saturation Polarization (T) |
| `03_composition_rho.ipynb` | Resistivity (μΩ·cm) |

---

#### Step 2 — WenAlloys Featurization + Model Training

Data preprocessing converts chemical composition (wt%) into (at%) elemental formulas,
followed by featurization using the matminer WenAlloys descriptor set,
manual feature selection, and training and validation of all four ML models.

| Notebook | Description |
|---|---|
| `04_preprocessing_wenalloys.ipynb` | Converts wt% composition into elemental formulas for WenAlloys |
| `05_wenalloys_Hc.ipynb` | Featurization, feature selection, and model training — Coercivity (A/m) |
| `06_wenalloys_Js.ipynb` | Featurization, feature selection, and model training — Saturation Polarization (T) |
| `07_wenalloys_rho.ipynb` | Featurization, feature selection, and model training — Resistivity (μΩ·cm) |

---

#### Step 3 — Oliynyk (CBFV) Feature Extraction

Data preprocessing converts chemical composition (wt%) into (at%) elemental formulas
for subsequent featurization using the CBFV Oliynyk descriptor set.
These notebooks extract raw Oliynyk features from chemical formulas 
and save them for downstream feature selection and model training.

| Notebook | Description |
|---|---|
| `08_preprocessing_oliynyk.ipynb` | Converts wt% composition into elemental formulas for Oliynyk |
| `09_oliynyk_Hc_extraction.ipynb` | Feature extraction — Coercivity (A/m) |
| `10_oliynyk_Js_extraction.ipynb` | Feature extraction — Saturation Polarization (T) |
| `11_oliynyk_rho_extraction.ipynb` | Feature extraction — Resistivity (μΩ·cm) |

---

#### Step 4 — Oliynyk Feature Selection (Optuna)

| Notebook | Description |
|---|---|
| `12_oliynyk_optuna_fs.ipynb` | Automated feature selection for all three properties using Optuna with LightGBM as the selector model. Outputs the optimal feature subsets for each target. |

---

#### Step 5 — Oliynyk Model Training

Training and evaluation using Oliynyk-selected features. Each notebook loads
the feature subsets produced by the Optuna selection step and trains
all four ML models (RFR, ETR, GBR, XGB) with the same hyperparameters used
in Steps 1 and 2.

| Notebook | Target Property |
|---|---|
| `13_oliynyk_Hc.ipynb` | Coercivity (A/m) |
| `14_oliynyk_Js.ipynb` | Saturation Polarization (T) |
| `15_oliynyk_rho.ipynb` | Resistivity (μΩ·cm) |

---

> **Pipeline order:**  
> `01–03` → `04–07` → `08–12` → `13–15`

</details>

### Results (`results/`)
- `metrics/` — Model performance metrics (Excel files)
- `shap/` — SHAP visualizations
  - `beeswarm/` — SHAP beeswarm plots
  - `grid-shap/` — Grid-SHAP visualizations
- `validation/` — External validation predictions

### Scripts (`scripts/`)
- `wenalloys_corrected.py` — Updated WenAlloys featurization

---

## WenAlloys: revised implementation

During this work, we identified discrepancies between the matminer `WenAlloys`
implementation (v0.10.0 and v0.10.1) and the original formulas from Guo (2015):

| Parameter | matminer v0.10.0 / v0.10.1 | This work |
|---|---|---|
| Configurational entropy (ΔSmix) | missing negative sign | −R·Σ xᵢ·ln(xᵢ), positive for random solutions |
| Mixing enthalpy (ΔHmix) | `abs()` applied, sign lost | sign preserved (negative for attractive interactions) |
| Yang Omega (Ω) | computed internally from the above | recalculated with explicit Tm: Ω = Tm·ΔSmix / max(1e-6, \|ΔHmix\|) |

The sign corrections change the values of the "Configuration entropy",
"Lambda entropy" and "Mixing enthalpy" features. Yang Omega was recalculated
for consistency; we did not independently verify whether its numerical value
changes (upstream review suggests it does not, since the modulus already
removed the sign of the entropy term).

See `scripts/wenalloys_corrected.py` for the revised implementation.

### Upstream status
Upstream status: see [hackingmaterials/matminer#962](https://github.com/hackingmaterials/matminer/issues/962).
Newer matminer releases may compute these features differently,
so use the pinned versions in `requirements.txt` to reproduce the paper.

### Reproducibility
Results in the paper were obtained with `matminer==0.10.1` and
`pymatgen==2026.5.4`. Use these pinned versions (see `requirements.txt`).
Do not apply the corrections from this repository on top of a matminer
version that already contains the upstream fix, otherwise the sign will be
flipped twice.

---

**Properties:** Hc (Coercivity, A/m), Js (Saturation Polarization, T), rho (Resistivity, μΩ·cm)  
**Algorithms:** RFR (Random Forest Regressor), ETR (Extra Trees Regressor), GBR (Gradient Boosting Regressor), XGB (XGBoost)
