# Weather Temperature Forecasting Project (GHA)

Hourly temperature forecasting (1-7 days ahead) comparing baseline, classical statistical, and deep learning models on high-frequency weather data.

## 📊 Project Overview

**Objective:** Predict hourly average air temperature for 24-168 hour horizons using a 10-minute weather dataset.

**Models Compared:**
- **Baseline:** Naive, Seasonal Naive
- **Classical:** SARIMA, ETS (Exponential Smoothing)
- **Deep Learning:** LSTM

**Key Findings:** ETS dominates longer horizons (RMSE 2.009°C @ H168), Naive excels short-term (1.705°C @ H24), LSTM underperforms (6.3-6.8°C RMSE).

## 📁 Repository Structure

### weather-forecasting-project-gha/

**data/**

- all_model_results.csv
- baseline_classical_forecasts.csv
- baseline_classical_results.csv
- cleaned_weather.csv
- lstm_forecasts_168h.csv
- lstm_results.csv
- summary_table.csv
- weather_temperature_hourly.csv

**figures/**

- figure_1_temperature_patterns.png
- figure_2_model_rmse_heatmap.png
- figure_3_48h_forecast_comparison.png
- figure_4_best_model_per_horizon.png

**notebooks/**

- 01_data_exploration_preprocessing_GHA.ipynb
- 02_baseline_classical_models_GHA.ipynb
- 03_advanced_models_GHA.ipynb
- 04_evaluation_comparison_GHA.ipynb

**report/**

- ITLB366_Group_D_GHA_.pdf


## 🛠️ Dataset

**weather_temperature_hourly.csv** (final modeling dataset):
| Column     | Type    | Description                  |
|------------|---------|------------------------------|
| `date`     | datetime| Time index                  |
| `y`        | numeric | **Target: Hourly temp (°C)**|
| `hour`     | int     | Hour of day (0-23)          |
| `hour_sin` | numeric | Cyclical hour encoding      |
| `dow_sin`  | numeric | Cyclical day encoding       |

**Source:** High-frequency meteorological data (2020-01-01 to 2021-01-01)

## 📈 Results Summary

**Best Models by Horizon:**
| Horizon | Best Model | RMSE (°C)    | Use Case              |
|---------|------------|--------------|----------------------|
| H24     | Naive      | 1.705        | Daily planning      |
| H48     | ETS        | 2.583        | Weekly inventory    |
| H72     | ETS        | 2.434        | Medium-term         |
| H168    | ETS        | **2.009**    | Strategic planning  |

**Stability (RMSE Variance):** ETS (0.0449) > LSTM (0.0539) > Naive (0.1075)

## 🚀 Quick Start

1. **Clone repository:**
git clone https://github.com/aejae-da/weather-forecasting-project-gha.git
cd weather-forecasting-project-gha


2. **Install dependencies:**
pip install -r requirements.txt


3. **Run notebooks sequentially:**
jupyter notebook notebooks/01_data_exploration_preprocessing_GHA.ipynb

→ 02_baseline → 03_advanced → 04_evaluation → 05_report


## 📋 Requirements
pandas==2.0.3
numpy==1.24.3
matplotlib==3.7.2
seaborn==0.12.2
scikit-learn==1.3.0
statsmodels==0.14.0
torch==2.1.0
jupyter==1.0.0
pmdarima==2.0.4


## 🏆 Key Insights

- **ETS** optimal for production (accuracy + stability + interpretability)
- **Naive** surprisingly competitive short-term
- **LSTM** needs multivariate data/larger dataset
- Classical > Deep Learning for this univariate task
