# Notebook Sequence: Smart Garden Analysis Pipeline

This folder contains the standardized analysis notebooks for the Smart Garden Management System project.

## Notebook Execution Order

Run notebooks in numerical sequence for reproducible results:

### `00-data-loading.ipynb`
**Purpose**: Load sensor data, validate schema, handle missing values
- Import sensor readings from CSV/database
- Validate data types and ranges
- Handle missing values and sensor failures
- Basic preprocessing and cleaning
- Output: Clean dataset ready for analysis

### `01-eda.ipynb`
**Purpose**: Exploratory Data Analysis of sensor patterns
- Statistical summaries (mean, median, std)
- Distribution analysis for each sensor type
- Correlation between sensors (moisture vs temp, etc.)
- Temporal patterns (daily/weekly/seasonal)
- Identify anomalies and outliers
- Visualization: Time series plots, heatmaps, distributions

### `02-model.ipynb`
**Purpose**: Train irrigation optimization models
- Prepare features for prediction (lagged values, weather data)
- Train multiple models (threshold-based, ML regression, forecasting)
- Hyperparameter tuning
- Cross-validation with time-series splits
- Model comparison and selection

### `03-eval.ipynb`
**Purpose**: Evaluate model performance and generate recommendations
- Performance metrics (MAE, RMSE, F1 for classification)
- Confusion matrix for watering decisions
- Water savings analysis vs baseline
- Plant health predictions
- Actionable recommendations
- Visualization of results and insights

---

## Dependencies

Add notebooks README with analysis pipeline guidepip install -r ../requirements.txt
```

Key packages:
- pandas, numpy for data manipulation
- matplotlib, seaborn for visualization
- scikit-learn for ML models
- statsmodels for time-series analysis

## Running Notebooks

```bash
jupyter notebook
# Then execute cells sequentially in each notebook
```

## Output Files

- `data/processed/clean_sensor_data.csv` (from 00)
- `data/processed/eda_summary.json` (from 01)
- `models/irrigation_model.pkl` (from 02)
- `reports/model_evaluation.html` (from 03)

---

**Last Updated**: November 2025
