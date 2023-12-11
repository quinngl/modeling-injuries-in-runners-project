# Modeling and Understanding Injuries in Competitive Runners 

### DS 6040 - Fall 2023 <br> Stephanie Fissel, Jackie Fraley, Quinn Glovier

## Overview

This project focuses on modeling and understanding injuries in competitive runners using Bayesian Machine Learning techniques. This dataset consists of detailed training logs from a Dutch high-level running team spanning seven years (2012-2019), including middle and long-distance runners (800 meters to marathon). The goal is to analyze training parameters and subjective assessments to predict and prevent injuries. 

## Dataset Descriptuon

- **Source**: The dataset includes sample from 74 runners (27 women, 47 men) with an average team tenure of 3.7 years. Athletes compete at national and international levels .

- **Ethics**: The study adheres to the Declaration of Helsinki, and ethical approval was obtained.
- **Data Structure**: Two datasets are available, one with daily data (`day_approach_maskedID_timeseries.csv`) and another with weekly aggregated data (`week_approach_maskedID_timeseries.csv`). For our analysis, we chose to focus on using the weekly data.

## Variables

### Initial Predictor Variables

- `n_sessions`: Total number of sessions completed.
- `n_restdays`: Number of days without training.
- `total_kms`: Total running mileage.
- `max_km_oneday`: Maximum kilometers completed in a single day.
- `total_kmZ5`: Total kilometers covered in Z5-T1-T2.
- `total_hrs_alt_training`: Total time spent on cross-training.
- `n_strength_training`: Number of strength training sessions.
- `avg_exertion`: Average rating of exertion.
- `avg_recovery`: Average rating of how well-rested the athlete felt.

### Response Variable

- `injury`: Binary column indicating whether the training setup resulted in an injury (1) or not (0)

## Model Development

### Beta-Binomial Model

A Bayesian Beta-Binomial model was developed to analyze injuries. 
The reduced model's predictors include:
- `max_km_oneday`: Maximum kilometers completed in a single day.
- `total_kmZ5`: Total kilometers covered in Z5-T1-T2.
- `avg_exertion`: Average rating of exertion.

```python
with pm.Model() as glm:
    
    α = pm.Beta('α', alpha = 1, beta = 1) #intercept
    β1 = pm.Beta('β1', alpha = 1, beta = 1) #max kilometers in one day
    β2 = pm.Beta('β2', alpha = 1, beta = 1) #total kilometers ran with anaerobic heart rate
    β3 = pm.Beta('β3', alpha = 1, beta = 1) #average exertion
    μ =  α + β1 * X[:,0] + β2 * X[:,1] + β3 * X[:,2]
    p = pm.Deterministic("p", pm.invlogit(μ))
    y_hat = pm.Binomial('y_hat', n = 1, p = p, observed = y) 
```
## Evaluation

### HMC Sampling
#### General Information:
- Better for smaller data sets
- Slower
- More accurate (will give exact values)

#### Our Parameters:
- 1000 draw iterations
- 2000 tuning points
- Took 3 seconds total
- 4 cores

### ADVI Approximation
#### General Information:
- Better for large datasets
- Can only approximate
- May not converge

#### Our Parameters:
- Used pm.fit()
- 10,000 iterations
- 1,000 samples
- Average loss: 723.15

## Conclusions
### Takeaways for Athletes
- Average exertion: The further an athlete pushes beyond their limits, the greater the likelihood of injury
- Injuries: The pursuit of peak performance often walks hand in hand with the risk of injury as athletes push their boundaries
- Take care of your body: Attending to your body and embracing recovery not only prevents injury but also enhances performance 

### Takeaways from Modeling
- Victories: The model converged with sampling
- Lessons: Creating model parameters involves many trials and errors
- Drawbacks: Our Posterior Predictive Check and ELBO Plots have major room for improvement


This project is licensed under the MIT License. 
