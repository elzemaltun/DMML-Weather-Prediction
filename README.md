# Weather Prediction Using Machine Learning

A machine learning project for predicting daily maximum and minimum temperatures using historical weather data from Cesena, Italy (2015-2025).

## Project Overview

This project implements and compares multiple regression models to predict temperature, addressing two key tasks:
1. **Same-day prediction**: Predicting temperature based on current weather conditions
2. **Time horizon forecasting**: Predicting temperature 3, 5, and 7 days ahead

## Dataset

- **Source**: Open-Meteo API
- **Location**: Cesena, Italy
- **Period**: 2015-2025 (~4000 daily observations)
- **Features**: Temperature, humidity, wind speed, pressure, precipitation, cloud cover, and more

## Project Structure

```
├── WeatherPredictionModel.ipynb    # Main Jupyter notebook
├── open-meteo-cesena2015-2025.csv  # Dataset
├── requirements.txt                 # Python dependencies
└── README.md                        # Project documentation
```

## Methodology

### 1. Data Understanding & Preprocessing
- Loaded and explored the dataset
- Aggregated hourly data to daily summaries
- Created temporal features (year, month, day, season)
- Handled data types and checked for missing values

### 2. Exploratory Data Analysis
- Temperature distribution analysis
- Time series visualization
- Seasonal pattern analysis
- Correlation matrix for feature selection

### 3. Feature Engineering & Selection
- Removed highly correlated features to avoid multicollinearity
- Selected 9 key features for modeling
- Applied StandardScaler for feature normalization

### 4. Model Training
Four regression models were trained and tuned using GridSearchCV:
- **Linear Regression** (baseline)
- **Random Forest Regressor**
- **Support Vector Regression (SVR)**
- **MLP Neural Network**

### 5. Evaluation Metrics
Models are evaluated using:
- **RMSE** (Root Mean Squared Error) - primary metric
- **MAE** (Mean Absolute Error)
- **R²** (Coefficient of Determination)

We chose RMSE as the primary metric because it penalizes larger errors more heavily, which is important in weather forecasting where large prediction errors are more costly. We use Test RMSE (not Train RMSE) for model selection to ensure we're measuring generalization performance on unseen data, avoiding overfitting.

## Results

### Same-Day Prediction
Multi-output regression predicting both `temp_max` and `temp_min`:
- Best performing model: **MLP Neural Network**
- Training period: 2015-2022
- Testing period: 2023-2025

### Time Horizon Forecasting
Separate models trained for 3-day, 5-day, and 7-day ahead predictions:

| Horizon | Best Model | Avg Test RMSE | Avg Test R² |
|---------|------------|---------------|-------------|
| 3-day   | MLP        | ~3.0°C        | ~0.82       |
| 5-day   | MLP        | ~3.0°C        | ~0.82       |
| 7-day   | MLP        | ~3.1°C        | ~0.81       |

As expected, prediction accuracy slightly decreases with longer forecast horizons due to increasing uncertainty in weather patterns.

## How to Run

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Open the notebook**:
   ```bash
   jupyter notebook WeatherPredictionModel.ipynb
   ```

3. **Run all cells**: Kernel → Restart & Run All

## Requirements

- Python 3.8+
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

## Key Findings

1. **MLP Neural Network** consistently outperforms other models for temperature prediction
2. **Temporal features** (month, season) are important predictors
3. **Prediction error increases** with longer forecast horizons, which aligns with the chaotic nature of weather systems
4. **Chronological train-test split** provides realistic evaluation of forecasting performance

## Authors

DMML Course Project