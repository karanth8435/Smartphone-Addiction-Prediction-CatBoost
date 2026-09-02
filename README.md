# Smartphone Addiction Prediction using CatBoost

## Project Overview

This project is my machine learning solution for the **Kaggle Playground Series S6E8 — Predicting Smartphone Addiction** competition.

The objective is to predict the probability of `addicted_label` from behavioral, demographic, and lifestyle-related features. The evaluation metric is **ROC-AUC**, so the models generate probability scores rather than hard 0/1 predictions.

This repository documents two versions of my own approach:

1. **Baseline CatBoost model**
2. **Improved CatBoost model** using controlled feature engineering and stronger model settings

> **Note:** The `aggressive_blend` submission and its supporting OOF files are intentionally excluded because that version included work contributed by another person and is not being presented as my own work.

## My Improvement

| Version | Mean 5-Fold CV ROC-AUC |
|---|---:|
| Baseline CatBoost | **0.957149** |
| Improved CatBoost | **0.961318** |
| Improvement | **+0.004169** |

The improved workflow also produced an overall OOF ROC-AUC of **0.961317**.

## Machine Learning Workflow

```text
Raw Competition Data
        ↓
Data Loading & Validation
        ↓
Target / ID Separation
        ↓
Categorical Missing-Value Handling
        ↓
Behavioral Feature Engineering
        ↓
5-Fold Stratified Cross-Validation
        ↓
CatBoost Training
        ↓
ROC-AUC Evaluation
        ↓
Baseline → Improved Model
        ↓
Final Probability Predictions
        ↓
Kaggle Submission
```

## Model Details

### Baseline CatBoost

- 5-fold Stratified Cross-Validation
- CatBoostClassifier
- 700 iterations
- Learning rate: 0.05
- Depth: 7
- ROC-AUC as the evaluation metric
- Native handling of selected categorical features

**Mean fold ROC-AUC:** 0.957149  
**Overall OOF ROC-AUC:** 0.957148

### Improved CatBoost

- 5-fold Stratified Cross-Validation
- 1,800 iterations
- Learning rate: 0.035
- Depth: 8
- `l2_leaf_reg = 5`
- `random_strength = 0.5`
- Early stopping
- Additional behavioral ratio/share features

**Mean fold ROC-AUC:** 0.961318  
**Overall OOF ROC-AUC:** 0.961317

## Feature Engineering

The improved version adds features intended to describe how overall screen time is distributed across different activities.

Examples include:

- `leisure_screen_hours`
- `screen_minus_work`
- `social_media_share`
- `gaming_share`
- `weekend_to_daily_screen`
- `notifications_per_app_open`

## Validation Strategy

I used **5-fold Stratified Cross-Validation**.

For each fold:

1. Train CatBoost on the training portion.
2. Generate validation probabilities.
3. Calculate ROC-AUC.
4. Store out-of-fold predictions.
5. Average test-set probabilities across folds.

## Kaggle

### Competition

[Predicting Smartphone Addiction — Kaggle](https://www.kaggle.com/competitions/playground-series-s6e8)

### My Submissions

[View my Kaggle submissions](https://www.kaggle.com/competitions/playground-series-s6e8/submissions)

The baseline workflow generates `submission.csv`, while the improved workflow generates `submission_improved.csv`.

> The `aggressive_blend` submission is intentionally excluded from this portfolio repository.

## Results & Evidence

### Baseline Cross-Validation

![Baseline CV](images/cv_baseline.png)

### Improved Cross-Validation

![Improved CV](images/cv_improved.png)

### Model Improvement

![Model Improvement](images/model_improvement.png)

### Kaggle Baseline Submission

![Kaggle Baseline Submission](images/kaggle_baseline.png)

### Kaggle Improved Submission

![Kaggle Improved Submission](images/kaggle_improved.png)

## Repository Structure

```text
Smartphone-Addiction-Prediction-CatBoost/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── S6E8_CatBoost_Baseline.ipynb
│   └── S6E8_CatBoost_Improved.ipynb
│
├── images/
│   ├── cv_baseline.png
│   ├── cv_improved.png
│   ├── model_improvement.png
│   ├── kaggle_baseline.png
│   └── kaggle_improved.png
│
└── results/
    ├── submission_baseline.csv
    ├── submission_improved.csv
    ├── cv_results_baseline.csv
    └── cv_results_improved.csv
```

## Files

**`S6E8_CatBoost_Baseline.ipynb`**  
Original CatBoost baseline workflow with feature preparation, 5-fold cross-validation, validation scoring, final training, and submission generation.

**`S6E8_CatBoost_Improved.ipynb`**  
Improved workflow with controlled feature engineering and stronger CatBoost settings.

The repository contains the small validation-result CSVs and the two submissions used in my own workflow.

The following are intentionally not included:

- `submission_aggressive_blend.csv`
- `oof_predictions.csv`
- `oof_predictions_improved.csv`

Large competition datasets such as `train.csv` and `test.csv` are also not included. They can be downloaded from the official Kaggle competition page.

## Reproducibility

1. Download the competition data from Kaggle.
2. Place the required competition files in the notebook working directory.
3. Install the packages listed in `requirements.txt`.
4. Open either notebook.
5. Run the notebook from top to bottom.
6. The baseline workflow generates `submission.csv`.
7. The improved workflow generates `submission_improved.csv`.

## Key Takeaways

- Built a complete CatBoost classification pipeline.
- Used stratified 5-fold cross-validation.
- Established a reproducible baseline.
- Improved the baseline through controlled behavioral feature engineering and model configuration.
- Increased mean CV ROC-AUC from **0.957149 to 0.961318**.
- Generated probability-based predictions for ROC-AUC evaluation.

## Tools & Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- CatBoost
- Jupyter Notebook
- Kaggle
