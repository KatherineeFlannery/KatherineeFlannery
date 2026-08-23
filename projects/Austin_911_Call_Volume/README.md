## Project Overview

How accurately can machine learning predict hourly 911 police dispatch call volume?

This project uses historical Austin Police Department Computer Aided Dispatch incident data to predict hourly police dispatch call volume using a random forest regression model. 

The goal was to determine whether temporal patterns and recent historical call volumes could provide useful predictions of future 911 demand. A dummy regressor was used as a baseline to determine whether the machine learning model provided meaningful improvement over a simple average-based prediction.

The final random forest regression model outperformed the baseline dummy regressor, reducing the mean absolute error from 10.48 calls per hour to 6.37 calls per hour and achieving an $R^2$ of 0.58 on the held-out test set. 

## Business Problem   

911 call centers must balance staffing and emergency-response resources with changes in demand throughout the day and week.
A model that can anticipate periods of higher call volume could potentially support staffing and resource-allocation decisions.
This project focuses on police-dispatch incidents in Austin, Texas, using the four most recent complete years available for the analysis: 2022–2025.

## Research Question: 

To what extent can temporal and historical call-volume features predict 911 police dispatch hourly call volume using a Random Forest regression model?

Random forest regression models combine predictions of multiple decision trees.

<img width="668" height="254" alt="randomforest" src="https://github.com/user-attachments/assets/9b98cd74-ed71-42ba-b9bc-8549208551ba" />

Dummy regressor models make simple predictions based on a strategy. For this analysis, the dummy regressor will output the mean of the training data and provide a baseline to compare performance against. 

<img width="624" height="180" alt="dummyregressor" src="https://github.com/user-attachments/assets/87e6d3a9-1bff-430e-a3c6-1b592622bc1b" />

This study hypothesizes that the random forest regressor model will outperform the dummy regressor by identifying trends in the historical data. 

## Data 

The project utilizes one publicly available dataset, APD Computer Aided Dispatch Incidents, provided by the City of Austin on the data.gov website. 

The file includes historical incident-level data for 911 calls involving police dispatch in the city of Austin in a CSV format. 

The original dataset contains:
- 4,082,993 incident records
- 27 variables
- Historical records from 2017-June 2026

The analysis uses a subset of the last four full years, 2022-2025. The original incident-level records were aggregated into a continuous hourly time series. Hours with no calls were retained and assigned a call volume of zero.

## Data Source

[APD Computer Aided Dispatch Incidents](https://catalog.data.gov/dataset/apd-computer-aided-dispatch-incidents)

## Exploratory Data Analysis

The hourly call volume averages approximately 43 calls per hour, with a maximum of 117 calls per hour. 

The analysis identified several recurring patterns:
- Call volume was generally lower between the hours 3 a.m. and 6 a.m.
- Between the hours of 3 p.m. and 11 p.m. the hourly call volume is highest, requiring more staff. 
- Hourly call volume demonstrated a recurring 24-hour pattern.
- High-volume periods were retained because these spikes represent meaningful demand that the model should learn to predict.

<img width="540" height="457" alt="callsperhour" src="https://github.com/user-attachments/assets/d27ed275-d7a3-4bd5-8884-adc835f9dad8" />

## Feature Engineering

The following predictors were developed from the incident data:

<img width="457" height="252" alt="variables_" src="https://github.com/user-attachments/assets/98bf2fe2-a245-4c9a-b144-fc1328d6eea4" />

Cyclical variables were transformed using sine and cosine encoding so that the model could recognize the cyclical nature of variables such as hour, month, and day of week. 

The 24-hour and 168-hour lag variables were included to capture recurring daily and weekly patterns. 

## Modeling Approach

A Random Forest Regressor was selected as the primary model because it can capture nonlinear relationships and interactions between predictors. 

The data is divided chronologically to ensure that the model is trained on earlier data and evaluated on later data which better reflects how the model will be used. The test size is set to 336 hours, which represents 2 full weeks to allow for staffing decisions to made in a timely fashion while limiting the length to maintain prediction accuracy. A gap of 24 is used to prevent data leakage.

<img width="474" height="213" alt="trainingsplit" src="https://github.com/user-attachments/assets/4b0c6721-5350-45bf-8b93-84c1706a1f75" />

The training data is divided into 5 time-series splits that get longer with each split. The purpose of this is to provide cross validation splits for model tuning. 

The analysis utilizes GridSearchCV with the TimeSeriesSplit for hyperparameter tuning of the model. The GridSearchCV selects the best performing model using the negative mean squared error since GridSearchCV maximizes the scoring method and a lower mean squared error indicates better performance. 

## Model Performance

The final model is evaluated on the unseen test data and compared against the dummy regressor model. 

<img width="468" height="141" alt="performance" src="https://github.com/user-attachments/assets/5dcd6834-217a-4070-9a6a-7e6494931d28" />

The Random Forest's MAE of 6.37 means that, on average, it's predictions were approximately 6.4 calls away from the actual call volume. Compared with the Dummy Regressor, the Random Forest reduced MAE by approximately 39%. The Random Forest also explained approximately 58% of the variance in the hourly call volume on the held-out test data. 

## Feature Importance

<img width="420" height="313" alt="feature_importance" src="https://github.com/user-attachments/assets/5f756e27-6a53-4bc1-b476-a252e686d0a1" />

The most influential features in the Random Forest model were:
- 168-hour call-volume lag
- Hour sine
- 24-hour call-volume lag
- Hour cosine

The importance of the lag variables suggests that recent historical call volume provides substantial information about future demand. The hour-based features also demonstrate the importance of recurring daily patterns. 

## Limitations

The Random Forest regression is bound by the range of the training data, meaning that the model will not predict beyond the minimum and maximum values in the training data. Additionally, the historical data may not capture unusual future call volumes.

The analysis does not incorporate external factors that could influence call volume such as weather, local events, or location within the city. 

## Business Implications

The results suggest that machine learning could potentially be used as a decision-support tool for anticipating periods of increased police-dispatch demand.

A forecasting system could potentially help managers consider:
- Staffing levels
- Resource allocation
- Anticipated periods of higher demand
- Short-term operational planning

The model should be considered a decision-support tool rather than a replacement for operational judgment.

## Model Improvement

Future improvements to the model could include:
- Incorporating additional predictors such as weather or local events.
- Modeling call volume by council district.
- Comparing Random Forest with additional time-series models.
  
