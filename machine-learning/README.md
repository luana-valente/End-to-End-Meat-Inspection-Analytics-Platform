# Machine Learning

This folder documents the predictive modelling component developed to assess whether historical slaughter, production, operational, geographic, and economic data could be used to predict sanitary condemnation rates.

The complete modelling notebook is available in:

[`../notebooks/machine-learning/`](../notebooks/machine-learning/)

## Problem Definition

The problem was formulated as a **supervised regression task**, where the target variable represents the proportion of condemned animals within a slaughter control period.

The modelling dataset was built from the sanitary control fact table and complementary Silver and Gold datasets.

It included:

- Temporal features.
- Slaughter volume.
- Animal holding characteristics.
- Slaughterhouse characteristics.
- Geographic information.
- Pork market prices.
- Estimated economic indicators.

## Data Preparation

The modelling workflow included:

- Removal of inconsistent and incomplete key records.
- Missing value treatment using training data only.
- Feature engineering for geographic proximity between animal holdings and slaughterhouses.
- Removal of target-derived variables to prevent data leakage.
- Temporal aggregation from daily to monthly granularity.
- Temporal train-test split, using 2020–2023 for training and 2024 for testing.
- Outlier and multicollinearity analysis.

Monthly aggregation was selected because it reduced target sparsity while preserving a sufficiently large dataset for modelling.

## Models Evaluated

The following regression algorithms were compared:

- Random Forest Regressor.
- Extra Trees Regressor.
- XGBoost Regressor.
- Multi-Layer Perceptron Regressor.

Model performance was evaluated using:

- Mean Absolute Error (MAE).
- Root Mean Squared Error (RMSE).
- Coefficient of Determination (R²).
- Additional error metrics for observations with a positive condemnation rate.

## Final Model

XGBoost achieved the best comparative performance and was selected for further optimization.

The final configuration used:

- Four selected features: slaughter volume, date, pork price, and standardized livestock units.
- Randomized hyperparameter search.
- No oversampling.
- No additional sample weighting.

| Metric | Final Result |
|---|---:|
| MAE | 0.0041 |
| RMSE | 0.0212 |
| R² | -0.0051 |
| MAE for positive cases | 0.0120 |
| RMSE for positive cases | 0.0520 |

## Model Interpretation

SHAP values were used to interpret the final XGBoost model.

The main contributing variables were:

1. Slaughter volume.
2. Standardized livestock units.
3. Date.
4. Pork market price.

The results indicate that operational scale had a greater influence on model predictions than the available geographic and categorical characteristics.

## Main Limitation

Despite optimization, predictive performance remained limited.

The low global error must be interpreted carefully because the target variable contains a high proportion of zero values. The negative R² indicates that the model did not reliably explain the variability of sanitary condemnation rates.

> [!IMPORTANT]
> The results suggest that the available datasets describe the outcomes of sanitary inspection more effectively than the underlying causes of sanitary risk.

## Future Work

Potential improvements include:

- Reformulating the problem as binary classification.
- Testing time-series approaches.
- Adding weather and environmental variables.
- Incorporating transport distance and duration.
- Including animal health, vaccination, treatment, and disease history.
- Adding animal welfare and slaughterhouse process indicators.
- Improving the representation of recent epidemiological events.

The final model should therefore be considered an analytical prototype rather than a production-ready risk prediction system.
