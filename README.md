# Injury Prediction in Competitive Runners 

## Overview

This project focuses on predicting injuries in competitive runners using Bayesian Machine Learnung techniques. This dataset consists of detailed training logs from a Dutch high-level running team spanning seven years (2012-2019), including middle and long-distance runners (800 meters to marathon). The goal is to analyze training parameters and subjective assessments to predict and prevent injuries. 

## Dataset Descriptuon

- **Source**: The dataset includes sample from 74 runners (27 women, 47 men) with an average team tenure of 3.7 years. Athletes compete at national and international levels .

- **Ethics**: The study adheres to the Declaration of Helsinki, and ethical approval was obtained.
- **Data Structure**: Two datasets are available, one with daily data (`day_approach_maskedID_timeseries.csv`) and another with weekly aggregated data (`week_approach_maskedID_timeseries.csv`). For our analysis, we chose to focus on using the weekly data.

## Variables

### Predictor Variables

- `n_sessions`: Total number of sessions completed.
- `n_restdays`: Number of days without training.
- `total_kms`: Total running mileage.
- `max_km_oneday`: Maximum kilometers completed in a single day.
- `total_kmZ5`: Total kilometers covered in Z5-T1-T2.
- `total_hrs_alt_training`: Total time spent on cross-training.
- `n_strength_training`: Number of strength training sessions.
- `avg_exertion`: Average rating of exertion.
- `avg_recovery`: Average rating of how well-rested the athlete felt.

### Responses Variable

- `injury`: Binary column indicating whether the training setup resulted in an injury (1) or not (0)

## Model Development

### Beta-Binomial Model

A Bayesian beta-binomial model was developed to predict injuries. The model includes predictors such as the number of sessions, rest days, total kilometers, and subjective assessments. 

```python
# Exmple code for model development
```

## Results and interpretation


## Conclusion









This project is licensed under the MIT License. 
