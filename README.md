# REST API Homework - Air Quality Analysis for Milan

## Project Overview

This project demonstrates a comprehensive data science workflow for air quality forecasting in Milan, Italy. The analysis integrates data from two independent REST APIs to predict NO₂ concentrations using meteorological variables, revealing critical insights about urban air pollution patterns and their relationship to weather conditions.

## Data Sources

- **OpenAQ API**: Air quality measurements from multiple monitoring stations across Milan
- **Open-Meteo API**: Hourly meteorological data (temperature, humidity, wind speed, precipitation)
- **Study Period**: January 1 - June 30, 2025
- **Geographic Scope**: 5km radius around central Milan (45.46427°N, 9.18951°E)

## Workflow

### 1. Data Retrieval
- **OpenAQ Data**: Retrieved air quality measurements from all sensors within 5km of central Milan
- **Weather Data**: Downloaded hourly meteorological variables from Open-Meteo archive API
- **Export Strategy**: All data immediately saved to CSV files for reproducibility

### 2. Data Cleaning and Integration
- **Timezone Conversion**: UTC timestamps converted to Europe/Rome local time
- **Spatial Aggregation**: Multiple sensors averaged to city-level hourly measurements
- **Pollutant Selection**: Focused on regulatory pollutants (PM2.5, O₃, NO₂, CO, PM10)
- **Missing Value Handling**: Forward-fill and backward-fill imputation applied
- **Data Merger**: Air quality and weather datasets joined on hourly timestamps

### 3. Exploratory Data Analysis
- **Distribution Analysis**: Examined pollutant concentration patterns and meteorological variables
- **Correlation Analysis**: Identified relationships between pollutants and weather factors
- **Temporal Patterns**: Analyzed seasonal trends, diurnal cycles, and day-of-week effects
- **Rolling Averages**: Applied 24-hour and 7-day smoothing to reveal underlying trends

### 4. Regression Modeling
- **Target Variable**: Hourly NO₂ concentrations
- **Predictors**: Temperature, relative humidity, wind speed, precipitation
- **Models Tested**: Linear Regression, Random Forest, Gradient Boosting
- **Evaluation**: 80/20 train-test split with comprehensive performance metrics

## Key Findings

### Traffic Dominance
- **Rush Hour Patterns**: Clear bimodal peaks at 8 AM and 6 PM in NO₂ concentrations
- **Weekday Effect**: Consistently higher NO₂ on weekdays compared to weekends
- **Traffic Signature**: Unmistakable evidence that vehicular traffic is the dominant NO₂ source

### Seasonal Patterns
- **Winter-Spring Transition**: Primary pollutants (NO₂, PM2.5, CO) decline from winter to spring
- **Temperature Inversion**: Higher concentrations in winter due to reduced atmospheric mixing
- **Ozone Formation**: O₃ increases with temperature, showing photochemical formation patterns

### Meteorological Relationships
- **Temperature Effect**: Strong negative correlation with primary pollutants (-1.35 coefficient)
- **Wind Dispersion**: Wind speed effectively disperses pollutants (-0.82 coefficient)
- **Humidity/Precipitation**: Moderate effects on pollutant removal
- **Explained Variance**: Meteorology accounts for ~48% of NO₂ variability

### Model Performance
- **Random Forest Superior**: Best performance (R² = 0.48, lowest MAE/MSE)
- **Non-linear Advantage**: Ensemble methods outperform linear regression by ~14 percentage points
- **Residual Quality**: Random Forest shows most stable, unbiased prediction errors

### Correlation Insights
- **Inter-pollutant Correlation**: PM2.5, PM10, NO₂, CO strongly correlated (r > 0.6) - shared traffic sources
- **Ozone Independence**: O₃ negatively correlated with NO₂ (r ≈ -0.4), confirming distinct formation mechanisms
- **Weather-Pollution Coupling**: Strong relationships between meteorology and pollutant concentrations

## Results Summary

### Model Performance Comparison
| Model | R² | MAE | RMSE |
|-------|----|----|------|
| Random Forest | 0.48 | 10.85 | 11.55 |
| Gradient Boosting | 0.42 | 11.61 | 12.16 |
| Linear Regression | 0.34 | 12.23 | 12.95 |
| Baseline (Mean) | -0.01 | 15.18 | 16.01 |

### Critical Limitations
- **Missing Traffic Data**: No direct representation of vehicle emissions (52% unexplained variance likely traffic-related)
- **Limited Features**: Only 4 meteorological predictors used
- **Temporal Constraints**: 3-month window, missing summer dynamics
- **Spatial Simplification**: Single-point aggregation ignores intra-urban gradients

## Operational Implications

### Policy Insights
- **Traffic Management**: Rush hour restrictions could measurably reduce NO₂ exposure
- **Weather-Based Forecasting**: Meteorological conditions enable 1-2 day pollution forecasts
- **Health Warnings**: Model supports early warning systems during unfavorable weather

### Future Enhancements
1. **Traffic Data Integration** (Highest Priority): Vehicle counts, emission estimates
2. **Feature Expansion**: Atmospheric pressure, solar radiation, wind direction
3. **Temporal Modeling**: ARIMA/LSTM for better time-series capture
4. **Uncertainty Quantification**: Confidence intervals for operational decisions

## File Structure
```
├── notebook.ipynb          # Main analysis notebook
├── keys.py                 # API credentials (excluded from git)
├── data/                   # Data files (excluded from git)
│   ├── data_air_quality_milan.csv
│   ├── data_weather_milan.csv
│   └── data_weather_air_quality_milan.csv
├── .gitignore              # Git ignore rules
└── README.md               # This file
```

## Author

Michele Turco
Data Science in Action - University Course  
February 2026