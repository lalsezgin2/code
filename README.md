Flight Delay Prediction Using Weather and Flight Characteristics
Overview

This project analyzes and predicts departure flight delays from John Glenn International Airport (CMH) during the month of December, a period known for heavy travel demand and harsh winter weather. Using historical flight performance and weather data, the goal is to understand which flight characteristics, weather conditions, and operational factors are most important in predicting whether a flight will be delayed.

The project combines exploratory data analysis, feature engineering, and multiple predictive modeling approaches to evaluate delay patterns and model performance under class imbalance.

Research Question:

Can flight delays for December departures from CMH be predicted using weather conditions, flight characteristics, and the operational scale of carriers and destinations?

Data Sources:

Two public datasets were used:

1. Marketing Carrier On-Time Performance
  - Source: Bureau of Transportation Statistics
  
  - Years: 2018–2019, 2022–2024 (COVID years excluded)
  
  - Scope: Flights departing from CMH
  
  - Contains flight timing, carrier, destination, distance, and delay indicators

2. Local Climatological Data
- Source: National Centers for Environmental Information (NCEI)

- Hourly weather data matched to flight departure hour

- Includes temperature, wind, humidity, visibility, pressure, and precipitation

- After cleaning, filtering to December, and merging by hour, the final dataset contains flight-level observations with corresponding weather conditions.

Key Variables

Target Variable:

  - DEP_DEL15: Binary indicator of departure delay (15+ minutes)

Flight & Time Variables

  - Day of month, day of week, scheduled departure hour

Distance

  - Flights per hour / flights per day (congestion metrics)

Weather Variables

  - Hourly wind speed
  
  - Relative humidity
  
  - Dry bulb temperature
  
  - Visibility
  
  - Altimeter setting
  
  - Dew point temperature
  
  - Precipitation

Engineered Variables

  - HOT_CARRIER: Top-quartile carriers by flight volume
  
  - HOT_DEST: Top-quartile destinations by flight volume

Methods:

The analysis was conducted in R and includes:
  
  - Data cleaning and preprocessing
  
  - Feature engineering for congestion and scale effects
  
  - Exploratory data analysis (EDA)
  
  - Train/test split (70/30)
  
  - Logistic regression
  
  - Logistic regression with cross-validated threshold adjustment
  
  - LASSO for predictor selection
  
  - Random forest for non-linear modeling and variable importance
  
  - Model evaluation using accuracy, sensitivity, specificity, precision, and AUC
  
  - Class imbalance (more on-time than delayed flights) is a central challenge addressed throughout the modeling process.

Key Findings:

  - Flight scheduled departure hour, distance, day of month, and weather conditions (especially wind speed and humidity) are strong predictors of delays.
  
  - High-volume carriers are associated with different delay patterns than lower-volume carriers.
  
  - Logistic regression performs poorly without threshold adjustment due to class imbalance.
  
  - Random forest achieves the highest sensitivity for detecting delayed flights, though some bias toward on-time flights remains.
  
  - Weather effects become more prominent in non-linear models.

Files in This Repository

  - final_dataset.csv – Cleaned and merged dataset used for modeling
  
  - data_preprocessing.Rmd – Data cleaning, merging, and feature engineering
  
  - final.Rmd – Full analysis, modeling, and interpretation
  
  - final.html – Rendered HTML report (recommended for viewing)

How to View the Results

  - Open final.html for the complete report with visuals and results
  
  - Use final.Rmd to inspect or reproduce the analysis

Tools & Libraries

  - R
  
  - tidyverse, caret, glmnet, randomForest, pROC, ggplot2, kableExtra

Notes & Limitations

  - Results are predictive, not causal
  
  - Analysis is limited to December and CMH
  
  - Performance is constrained by class imbalance and available predictors
