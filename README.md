# Air Quality Prediction with Rolling Window Features

This repository implements air quality prediction using rolling window features to enhance the model's accuracy and prediction capabilities. Below are the key steps and features of the implementation:

## Rolling Window Feature Update

1. **Rolling Window Calculation**  
   The dataset used for training has been updated by introducing a new feature: a 3-day rolling mean of the PM2.5 values. This was calculated using the following command:  
   ```python
   df_roll['pm25_3day_roll_mean'] = df_roll['pm25'].rolling(window=3).mean()
# Air Quality Prediction: Rolling Window Features

This project incorporates rolling window features into the air quality prediction pipeline to enhance the model's predictive accuracy and data utility.

## Feature Storage in Hopsworks

The newly created rolling window feature is stored as a new feature in Hopsworks to ensure it is accessible for future predictions and training processes.

## Daily Feature Update

A dedicated notebook (`2_air_quality_feature_pipeline.ipynb`) is used to update the rolling window features daily. For each day, the rolling window mean is recalculated using the current PM2.5 value and stored in the feature store.

## Model Retraining

The predictive model was retrained with the updated dataset, which now includes the rolling window feature (`pm25_3day_roll_mean`). This additional feature has improved the model's capability to learn trends and dependencies in the data.

## Inference Pipeline

### Daily Prediction Loop

A loop was implemented to perform inference day by day. For each future day, the model predicts the PM2.5 value based on the available data and updates the rolling window feature for subsequent predictions. This ensures that the rolling window feature reflects real-time predictions and weather conditions for accurate forecasting.

### Single-Day PM2.5 Prediction

For every day in the inference process, the model predicts the PM2.5 value of the next single day. This step leverages both weather forecast data and the predicted rolling window feature.

### Updated Inference with New Features

The model was used to make predictions of PM2.5 values by incorporating both the rolling window feature and other estimated features.

## Results Display

The results of the inference, including predictions made with the updated rolling window feature, are displayed at the following link:  
[Air Quality Rolling Window Predictions](https://jacopodallafior.github.io/Air_Quality_Rolling_Window/air-quality/)

## Key Files and Notebooks

- **`2_air_quality_feature_pipeline.ipynb`**: Updates rolling window features and stores them in Hopsworks.
- **`model_training.ipynb`**: Retrains the model with the new features.
- **`inference_pipeline.ipynb`**: Implements the day-by-day prediction loop for PM2.5 values.
