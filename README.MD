# Car Price Prediction Challenge

An academic machine learning notebook for the Computational Learning subject at Universitat Autònoma de Barcelona (UAB). It explores used-car attributes, preprocessing, and regression models using the Car Price Prediction Challenge dataset.

## Dataset and workflow

The notebook uses **Car Price Prediction Challenge**, published by **deepcontractor** on [Kaggle](https://www.kaggle.com/datasets/deepcontractor/car-price-prediction-challenge). Its target is `Price`; attributes include manufacturer, model, production year, mileage, engine volume, fuel type, and transmission.

The CSV is not distributed with this repository because an explicit license permitting redistribution here has not been established. Download the dataset separately from the linked Kaggle page and extract the CSV locally.

Before running the notebook:

1. Create a `data` directory in the repository root if it does not exist. In PowerShell, run `New-Item -ItemType Directory -Force -Path data`; on macOS/Linux, run `mkdir -p data`.
2. Place the downloaded CSV at exactly `data/car_price_prediction.csv`.
3. Open and execute the notebook with this repository's root as the working directory. Its existing `pd.read_csv('data/car_price_prediction.csv')` call then reads your local copy without code changes.

The local CSV is ignored by Git to prevent accidental redistribution. Downloading it is a prerequisite for execution; the historical notebook outputs remain available without rerunning it.

`kaggle.ipynb` contains exploratory analysis, feature preparation, target encoding, min-max scaling, and a Bayesian model search with repeated cross-validation. Models include linear regression, Lasso, Ridge, support vector regression, and random forests.

## Setup and usage

Run commands from this repository's root directory with Python 3 and pip:

```bash
python -m venv .venv
```

Activate the environment in PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

On macOS/Linux, use `source .venv/bin/activate`. Then install the existing dependencies:

```bash
python -m pip install -r requirements.txt
```

Open `kaggle.ipynb` in a Jupyter-capable editor. Jupyter itself is not listed in `requirements.txt`; a notebook frontend must be supplied separately. Execute cells in order from the repository root. Model search can be expensive and uses parallel workers.

## Recorded results and limitations

The final model cell specifies `RandomForestRegressor(n_estimators=296, max_depth=17, random_state=42)`. The saved notebook output records:

| Metric | Training set | Test set |
| --- | --- | --- |
| MAE | 0.057571 | 0.083994 |
| R² | 0.854309 | 0.711058 |

MAE is expressed on the normalized price scale, rather than in currency units. These are historical notebook outputs and were not regenerated during maintenance.

The notebook fits target encoding and scaling after concatenating training and test data. This can leak information into evaluation, and the preprocessing is outside the cross-validation pipeline. Treat the recorded scores as exploratory results; an independent evaluation would require training-only preprocessing within each fold. The original workflow is preserved.

Dependencies are unpinned, and there is no automated test suite or locked historical environment. The dataset must be obtained separately from Kaggle. Repository-authored source code is licensed under [MIT](LICENSE). Third-party data/assets, upstream libraries, submodules and external models retain their own terms; MIT does not relicense them.
