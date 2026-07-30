# Limitations and Future Work

## Model Limitations

Despite feature selection, hyperparameter tuning, oversampling experiments, and sample-weighting strategies, the final model achieved limited predictive performance.

The main limitations identified were:

- **Zero-inflated target:** most observations had a condemnation rate equal to zero, making it difficult for the model to learn the less frequent positive cases.
- **Limited explanatory variables:** the available data mainly described the outcomes of sanitary inspection rather than the underlying causes of sanitary risk.
- **Restricted modelling period:** the Machine Learning dataset covered 2020–2024, while the broader analytical project covered 2011–2024.
- **Aggregated geographic information:** administrative regions may not adequately represent transport conditions, environmental exposure, or local epidemiological risk.
- **Low variability in categorical features:** several animal holding and production attributes were concentrated in a small number of categories, reducing their predictive value.
- **Monthly aggregation:** aggregation reduced sparsity and noise but may also have hidden short-term patterns and isolated sanitary events.

The final negative R² indicates that the model did not reliably explain the variability of the condemnation rate. The solution should therefore be considered an analytical prototype rather than a production-ready prediction system.

## Data Enrichment

Future versions of the project would benefit from variables more directly related to animal health, welfare, transport, and environmental conditions, including:

- Disease and outbreak history.
- Vaccination and veterinary treatment records.
- Farm biosafety indicators.
- Animal mortality and morbidity records.
- Transport distance and duration.
- Vehicle density, hygiene, and ventilation conditions.
- Weather conditions before and during transport.
- Animal handling and pre-slaughter holding conditions.
- Slaughterhouse operational incidents and process-related condemnations.

These variables could provide a more direct representation of the causes associated with sanitary condemnation.

## Alternative Modelling Approaches

### Binary Classification

The problem could be reformulated as a binary classification task:

> **Will a slaughter batch contain at least one condemned animal?**

This approach may provide a more operationally useful risk signal for inspection planning and resource allocation.

### Time-Series Modelling

Future work could also evaluate time-series approaches using daily or weekly data.

Potential methods include:

- Lag-based Machine Learning models.
- ARIMA or models with exogenous variables.
- Gradient boosting models with temporal features.
- Recurrent neural networks, such as LSTM, if sufficient data becomes available.

### Two-Stage Modelling

A two-stage approach could separate the problem into:

1. Predicting whether a condemnation event will occur.
2. Predicting the condemnation rate for cases where the event is expected to be positive.

This strategy may be more appropriate for a target distribution with a large number of zero values.

## Operational Validation

Before any production deployment, the model would require:

- Validation with domain experts and official veterinary inspectors.
- Testing on new and unseen operational periods.
- Monitoring for data drift and changes in inspection practices.
- Definition of acceptable risk thresholds.
- Assessment of fairness across regions, slaughterhouses, and animal holdings.
- A formal model governance and retraining process.

## Conclusion

The main opportunity for improvement lies not only in testing more complex algorithms, but in enriching the analytical dataset with variables that better represent the sanitary, environmental, logistical, and operational causes of condemnation.
