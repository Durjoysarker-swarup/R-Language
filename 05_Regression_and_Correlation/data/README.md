# Data Files

All files are synthetic and stored in `data/raw/`. Units: yield in t/ha, nitrogen and phosphorus in kg/ha, fertilizer in kg, rainfall in mm, temperature in °C, organic matter in %.

## File to qmd mapping

| CSV file | Rows | Columns | Used in |
|----|----|----|----|
| `agriculture_yield_data.csv` | 10 | nitrogen, rainfall, yield | `01_regression_fit_interpretation.qmd` |
| `yield_soil_data.csv` | 30 | nitrogen, rainfall, yield | `01_regression_fit_interpretation.qmd` |
| `high_correlation_agriculture.csv` | 50 | yield, nitrogen, rainfall, temperature | `02_correlation_multicollinearity.qmd`, `03_multicollinearity_remedies.qmd` |
| `agricultural_yield_data.csv` | 100 | Soil_Nitrogen, Soil_Phosphorus, Rainfall, Temperature, Yield | `03_multicollinearity_remedies.qmd` |
| `agri_yield_data.csv` | 100 | Crop_Yield, Fertilizer_kg, Rainfall_mm, Soil_Nitrogen | `04_assumption_diagnostics.qmd` |
| `day6_crop_data.csv` | 100 | yield, nitrogen, rainfall, temperature, pH, organic_matter | `05_model_selection.qmd` |
| `yield_data.csv` | 30 | yield, nitrogen, rainfall | `06_prediction_rmse_report.qmd` |
| `yield_data_high_r2.csv` | 40 | yield, nitrogen, rainfall | `06_prediction_rmse_report.qmd` |

## What each file demonstrates

| CSV file | Purpose |
|----|----|
| `agriculture_yield_data.csv` | High R² but non-significant individual predictors |
| `yield_soil_data.csv` | Scatter plots with regression line |
| `high_correlation_agriculture.csv` | Correlation matrix, `pairs.panels()`, VIF, PCA |
| `agricultural_yield_data.csv` | Ridge regression with `glmnet` |
| `agri_yield_data.csv` | Residual diagnostics (4 plots, `qqPlot`, `ncvTest`) |
| `day6_crop_data.csv` | AIC, BIC, stepwise selection (pH is a noise predictor) |
| `yield_data.csv` | Weak model with low R² |
| `yield_data_high_r2.csv` | Final model, prediction, RMSE, report |

## Notes

- Read files with relative paths, e.g. `read.csv("../data/raw/yield_data.csv")`.
- Files are reproducible: each was generated with a fixed seed.
- No missing values, no text columns.
