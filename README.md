# Assignment 2: From Trees to Neural Networks

End-to-end implementation for comparing **XGBoost (GBDT)** vs **MLPClassifier (Neural Network)** on the UCI Bank Marketing binary classification task.

## Project Goal

Predict whether a client subscribes to a term deposit (`y`) and compare model families using:

- Accuracy
- Precision
- Recall
- F1
- AUC-PR
- Training time

The notebook enforces a no-leakage workflow: split first, fit preprocessing on train only, transform validation/test with fitted train preprocessors.
It also keeps validation for model selection and uses the test set only for final held-out evaluation.

## Repository Structure

- `notebooks/bank_marketing_xgb_vs_mlp.ipynb`: main runnable notebook
- `data/raw/`: input dataset location (not tracked in Git)
- `reports/metrics/`: exported metrics, trial tables, and best-params JSON
- `reports/figures/`: exported plots for report use
- `requirements.txt`: Python dependencies

## Data

Expected file:

- `data/raw/bank-full.csv`

If `bank-full.csv` is missing, place the UCI Bank Marketing dataset file in `data/raw/` before running.

## Method Summary

1. Load and normalize schema/target.
2. Run explicit data-quality audit (types, missingness, `unknown` counts, target distribution).
3. Apply light feature engineering (`prev_contacted`, `recent_contact`, `prior_success`).
4. Create one stratified `70/15/15` train/validation/test split.
5. Build separate preprocessors:
   - XGBoost: impute + one-hot (no scaling)
   - MLP: impute + scale numeric + one-hot
6. Tune XGBoost and MLP hyperparameters on validation AUC-PR.
7. Evaluate best models on validation and test.
8. Save tables/metrics/figures to `reports/`.

## Environment Setup (Windows PowerShell)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r .\requirements.txt
python -m ipykernel install --user --name assignment2-aml --display-name "Python (assignment2-aml)"
```

Recommended Python: `3.11+`

## Run

```powershell
.\.venv\Scripts\Activate.ps1
jupyter lab
```

Then open and run all cells in:

- `notebooks/bank_marketing_xgb_vs_mlp.ipynb`

Headless reproducible execution option:

```powershell
.\.venv\Scripts\Activate.ps1
jupyter nbconvert --to notebook --execute --inplace .\notebooks\bank_marketing_xgb_vs_mlp.ipynb
```

## Generated Outputs

Metrics and artifacts are written to:

- `reports/metrics/evaluation_summary.csv`
- `reports/metrics/model_comparison.csv`
- `reports/metrics/xgb_trials.csv`
- `reports/metrics/mlp_trials.csv`
- `reports/metrics/xgb_best_metrics.json`
- `reports/metrics/mlp_best_metrics.json`

Figures are written to:

- `reports/figures/xgb_train_val_loss.png`
- `reports/figures/xgb_feature_importance_top20.png`
- `reports/figures/xgb_learning_rate_comparison.png`
- `reports/figures/xgb_learning_rate_sensitivity_from_trials.png`
- `reports/figures/mlp_loss_curve.png`
- `reports/figures/mlp_architecture_comparison.png`
- `reports/figures/mlp_depth_width_effect.png`
- `reports/figures/mlp_learning_rate_sensitivity_from_trials.png`
- `reports/figures/test_pr_curves.png`
- `reports/figures/model_comparison_metrics.png`

## Reproducibility

- Fixed random seed is used in data split and model training.
- Hyperparameter trial sampling is seed-controlled when caps are enabled.
- Artifacts are exported from the notebook for grading traceability.
