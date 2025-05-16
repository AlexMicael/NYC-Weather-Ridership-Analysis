# Weather × Ridership Analysis with Apache Spark


[![License](https://img.shields.io/badge/License-Apache_2.0-0D76A8?style=flat)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.7.12](https://img.shields.io/badge/Python-3.7.12-green.svg)](https://shields.io/)

## Project Overview

This project analyzes the impact of weather on New York City public transportation ridership using Apache Spark. It combines open MTA ridership data and Open-Meteo weather data, performs feature engineering, computes correlations, and builds a predictive model for subway ridership.

## Key Tasks

- Initialize Spark session
- Load and clean MTA daily ridership data (subway, bus, LIRR, Metro North)
- Load and process historical weather data (temperature, precipitation, wind)
- Join ridership and weather data on date
- Feature engineering: create rain, hot day, and cold day flags
- Analyze correlations between weather and ridership
- Aggregate average ridership by weather conditions
- Train a linear regression model to predict subway ridership
- Predict upcoming ridership using weather forecasts
- Save results to disk

## Setup

1. **Install dependencies**  
   Install directly:
   ```bash
   pip install pyspark findspark pandas sodapy openmeteo-requests requests-cache retry-requests numpy
   ```

2. **Run the notebook**  
   Open `NYC_Transit_Ridership_and_Weather_Analysis.ipynb` in Jupyter, GCP or VS Code and run all cells.

## Data Sources

- **Ridership:** [MTA Daily Ridership Data (NY Open Data)](https://data.ny.gov/Transportation/MTA-Daily-Ridership-Data-Beginning-2020/vxuj-8kew)
- **Weather:** [Open-Meteo Historical & Forecast API](https://open-meteo.com/)

## Outputs

- Enriched and joined dataset (Parquet)
- Aggregated CSVs for ridership by rain, hot, and cold days
- Trained regression model (Spark ML)
- Predicted ridership for upcoming days (Parquet)

## Author

[Alex Chen Hsieh](https://www.linkedin.com/in/alex-chen-hsieh/)

---

*Project created as part of Introduction to Cloud Computing (CS 452) at Binghamton University, 2025*
