# Time Series Modelling & Forecasting (UK Climate Data)

A reproducible statistical investigation of long-term temperature and air-frost patterns across **37 UK weather stations**, using monthly records published by the UK Met Office.

**Author:** Aslı Akel  
**Programme:** MSc Data Science and Artificial Intelligence

## Project highlights

- Validates and combines 39,427 station-month observations spanning 1853–2025.
- Uses real calendar time so missing months are not compressed into the trend index.
- Models maximum temperature with a linear trend and annual sine/cosine seasonality.
- Reports heteroskedasticity-and-autocorrelation-consistent (HAC) inference.
- Uses a 12-month moving-block residual bootstrap to preserve short-range temporal dependence.
- Quantifies uncertainty in station-level trends and long-range illustrative projections.
- Tests decadal changes in air-frost frequency using actual calendar-day denominators.
- Controls the false discovery rate across 37 simultaneous station tests using Benjamini–Hochberg correction.
- Separates statistical evidence, effect size, interpretation, and methodological limitations.

## Selected results

These values come directly from the saved notebook outputs:

- **37/37 stations** had a 95% moving-block bootstrap interval for the maximum-temperature trend entirely above zero.
- The median station trend was **0.207°C per decade**.
- Heathrow's estimated trend was **0.314°C per decade**, with a HAC 95% confidence interval of **0.238–0.390°C per decade**.
- Whitby had the largest estimated trend at **0.502°C per decade**; Armagh had the smallest at **0.060°C per decade**.
- **36/37 stations** showed evidence of changing frost-day proportions after Benjamini–Hochberg correction at a 5% false-discovery rate.

The August 2075 values in the notebook are deliberately labelled **model projections**, not physical climate forecasts. They extrapolate a historical linear model and are included to demonstrate prediction uncertainty and the risks of out-of-sample interpretation.

## Repository structure

```text
.
├── data/
│   ├── ALL-WEATHER-STATIONS.csv
│   ├── 37 station CSV files
│   └── README.md
├── uk_historic_weather_statistical_analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

The notebook is the primary project artifact and contains the complete workflow, narrative, figures, statistical tables, diagnostics, and saved results.

## Run locally

Python 3.10 or later is recommended.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Open `uk_historic_weather_statistical_analysis.ipynb` and run all cells from the repository root. Random seeds are fixed for reproducible bootstrap results.

## Methods

The temperature model includes elapsed calendar time plus annual sine and cosine terms. HAC standard errors provide regression inference robust to heteroskedasticity and short-range autocorrelation. A 12-month circular moving-block bootstrap supplies non-parametric station-level trend intervals.

The frost analysis constructs observed frost and non-frost day counts from each available month using its true calendar length. Missing months contribute no exposure. Chi-squared tests compare proportions across decades, and Benjamini–Hochberg adjustment addresses multiplicity across stations.

## Limitations

- Station records differ in duration, missingness, closure status, instrumentation, and local environment.
- The station collection is not a perfectly balanced spatial panel.
- Statistical association does not establish a causal mechanism.
- The linear seasonal model cannot represent all long-term climate dynamics.
- Extrapolation to 2075 assumes continuation of historical linear trends and is unsuitable for operational forecasting or policy decisions.
- The frost chi-squared test detects differences among decades but does not alone establish a monotonic trend.

## Data source and attribution

Data source: UK Met Office, [Historic station data](https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data).

The Met Office describes the files as monthly series containing mean daily maximum and minimum temperature, air-frost days, rainfall, and sunshine duration. The repository preserves the small CSV extracts used for reproducibility and attributes the Met Office as the source. Review the [Met Office legal and licensing information](https://www.metoffice.gov.uk/policies/legal) before reuse.
