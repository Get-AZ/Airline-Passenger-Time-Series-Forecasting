# Airline Passenger Time Series Forecasting

Reproducible monthly forecasting with **ARIMA, SARIMA, seasonal naïve baseline, rolling-origin cross-validation, and residual diagnostics**.

## Dataset
[Airline Passengers CSV](https://raw.githubusercontent.com/jbrownlee/Datasets/master/airline-passengers.csv), 144 monthly observations from January 1949 to December 1960; counts in thousands.

## Validated findings (user-run Colab outputs)
| Model | 1960 MAE | 1960 RMSE | 1960 MAPE |
|---|---:|---:|---:|
| Tuned SARIMA (0,1,0)(1,1,0,12) | 16.600 | 21.479 | 3.751% |
| Original SARIMA (1,1,1)(1,1,1,12) | 16.673 | 21.621 | 3.762% |
| Seasonal naïve | 47.833 | 50.708 | 9.988% |
| ARIMA (2,1,2) | 41.835 | 55.223 | 8.220% |

Four expanding-window 12-month folds (1956–1959) selected tuned SARIMA on mean RMSE (23.073). The 1960 holdout was not used in grid tuning. SARIMA improves RMSE by 57.64% versus seasonal naïve on 1960.

**Limitation:** tuned SARIMA residual Ljung–Box lag-24 p=0.0265 (lag-12 p=0.0547), suggesting remaining autocorrelation. Forecast intervals are model-based and may be miscalibrated. The 1960 holdout had already been viewed during early experimentation, so this is not a fully blind external benchmark.

## Reproduce
1. Open `notebooks/airline_forecasting_reproducible.ipynb` in Google Colab.
2. Run all cells from top to bottom with internet access for the dataset.
3. The notebook independently reloads the CSV, performs training-only model selection, tests on 1960, and forecasts 1961.

## Repository layout
- `notebooks/`: executable notebook
- `docs/`: technical report
- `career/`: LinkedIn and CV text
- `interview/`: 30 interview questions with answers
- `results/`: validated user-run metrics and forecast

## Reproducibility
Python 3.11+ recommended; dependencies in `requirements.txt`. Different statsmodels versions may cause small numerical differences. The repository includes no pretrained model and does not claim deployment.

## License
MIT (for authored project code and documentation). Dataset originates from the linked third-party source.
