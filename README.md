# Smartphone Addiction Prediction using CatBoost

Machine learning classification project based on the Kaggle Playground Series S6E8 competition.

## Project Overview

The objective is to predict the probability of smartphone addiction using behavioral, demographic, and lifestyle-related features.

The competition evaluates predictions using ROC-AUC.

## Approach

### Baseline
A CatBoost classifier was trained using 5-fold stratified cross-validation.

### Improvement
The baseline was improved using controlled behavioral feature engineering and stronger CatBoost hyperparameters.

## Model Performance

| Version | Mean CV ROC-AUC |
|---|---:|
| Baseline CatBoost | 0.957149 |
| Improved CatBoost | 0.961318 |
| Improvement | +0.004169 |

## Key Improvements

- Behavioral feature engineering
- 5-fold Stratified Cross-Validation
- CatBoost hyperparameter tuning
- Early stopping
- Probability-based ROC-AUC evaluation

## Kaggle

[Predicting Smartphone Addiction — Kaggle](https://www.kaggle.com/competitions/playground-series-s6e8)

[My Kaggle Submissions](https://www.kaggle.com/competitions/playground-series-s6e8/submissions)

## Results

### Cross-Validation

![CV Comparison](images/model_improvement.png)

### Kaggle Submission — Baseline

![Baseline Submission](images/kaggle_baseline.png)

### Kaggle Submission — Improved

![Improved Submission](images/kaggle_improved.png)

## Repository Structure

...
