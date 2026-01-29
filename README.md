# surrogate-model-bayesian-optimization
# Prescriptive Optimization with Surrogate Modeling + Bayesian Optimization

This project builds a **surrogate model** for a target objective (e.g., **BMI** or another scalar “error” metric) and then performs **Bayesian Optimization** to recommend **high-quality candidate settings** under realistic feature bounds.  
It also includes **multi-objective Pareto analysis**, **uncertainty-aware top-K recommendations**, and **local interpretability** (PD/ICE + ALE) around the recommended optimum.

---

## What this does (high level)

### 1) Surrogate model training + selection
- Trains and compares surrogate regressors (e.g., **Gaussian Process**, **Random Forest**, **XGBoost**)
- Uses cross-validation to select the best model
- Saves the trained model and CV summary artifacts

### 2) Bayesian Optimization (BO) for prescriptive recommendations
- Uses BO (EI / q-EI style acquisition) to search within **data-inferred bounds**
- Produces a ranked list of **recommended feature settings** and logs the optimization progress

### 3) Multi-objective / Pareto front analysis
- Builds **Pareto fronts** between the target objective and selected proxy objectives/features
- Highlights “knee points” that represent good trade-offs

### 4) Uncertainty + robustness analysis for top-K candidates
- Reports uncertainty bands for the top-K recommended points
- Adds a local perturbation-based **robustness score** for more reliable recommendations

### 5) Interpretability around the optimum
- Generates **Partial Dependence / ICE** and **ALE** plots around the best setting
- Helps explain why the surrogate recommends certain ranges

---

## Repository contents

### Key artifacts (generated outputs)
Most outputs are stored as CSVs/PNGs and can be found in the artifacts folder:

**Bayesian Optimization**
- `bo_log.csv` — optimization iterations log
- `bo_recommendations.csv` — ranked candidate settings (top recommendations)

**Bounds + model**
- `optimization_bounds.csv` — data-inferred feature bounds used in optimization
- `surrogate_model.pkl` — trained surrogate model (serialized)
- `surrogate_cv_summary.csv` — CV metrics / model selection summary

**Pareto fronts + knee points**
- `viz_pareto_predicted.png` — main Pareto visualization
- `pareto_predicted_*.png` — Pareto plots for different feature/proxy pairs
- `pareto_predicted_mult_objective.csv` — multi-objective Pareto front data (if generated)
- `knees_predicted_*.csv` — knee points extracted from Pareto fronts

**Uncertainty + robustness**
- `topk_uncertainty.csv` — uncertainty summary for top-K candidates
- `topk_uncertainty_robustness.csv` — uncertainty + robustness (perturbation-based)

**Interpretability**
- `viz_pd_ice_*.png` — Partial Dependence + ICE plots around the optimum
- `viz_ale_*.png` — ALE plots around the optimum
- `viz_contour_error_*.png` — local contour/heatmaps near best setting (when enabled)
- `viz_acq_EI_*.png` — acquisition surface snapshot (when enabled)

---

## Example outputs (recommended to showcase)
If you want a quick visual tour, start with:
- `viz_pareto_predicted.png`
- `viz_contour_error_*.png`
- `viz_pd_ice_*.png` and `viz_ale_*.png`
- `topk_uncertainty_robustness.csv`

---

## How to run

### Option A: Run in Google Colab (recommended)
1. Upload the notebook to Colab
2. Upload your dataset CSV (if not included in this repo)
3. Run all cells to reproduce outputs

### Option B: Run locally
**Requirements**
- Python 3.9+ recommended

Install dependencies:
```bash
pip install -r requirements.txt
