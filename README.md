# Assignment 2: Notebook Workflow

This project is set up to run the assignment end-to-end in a local notebook.

## Structure

- `data/raw/`: original assignment data
- `data/interim/`: temporary cleaned outputs
- `data/processed/`: final modeling-ready data
- `models/`: saved model artifacts
- `notebooks/`: assignment notebook(s)
- `reports/metrics/`: saved metrics, params, and summary CSVs
- `reports/figures/`: saved report-ready PNG figures

## Environment

- Python virtualenv spec: `requirements.txt`
- Assignment-required model libs included: `scikit-learn` (MLP) and `xgboost` (GBDT)
- Recommended Python: `3.11` (tested setup is compatible with `3.11+`)

## Create the environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r .\requirements.txt
python -m ipykernel install --user --name assignment2-aml --display-name "Python (assignment2-aml)"
```

## Run the assignment

1. Start Jupyter:

```powershell
.\.venv\Scripts\Activate.ps1
jupyter lab
```

2. Open and run all cells in:

- `notebooks/bank_marketing_xgb_vs_mlp.ipynb`

3. Find outputs in:

- `reports/metrics/`
- `reports/figures/`
