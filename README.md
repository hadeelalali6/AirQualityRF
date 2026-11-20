Air Quality Classification Using Random Forest

Project Overview

This project aims to classify air quality levels using the Random Forest algorithm and evaluate the impact of optimization and hyperparameter tuning on model performance.

Dataset

The dataset contains 5,000 samples and 9 input features related to environmental conditions and air pollution.

Features

Temperature

Humidity

PM2.5

PM10

NO2

SO2

CO

Proximity to Industrial Areas

Population Density

Target Classes

Class

Samples

Good

2,000

Moderate

1,500

Poor

1,000

Hazardous

500

Total

5,000

Methodology

Data inspection and preprocessing

Exploratory Data Analysis (EDA)

Label encoding

Stratified train-test split

Random Forest classification

Optimization and hyperparameter tuning

Model evaluation and performance comparison

Model Configuration

Parameter

Value

Algorithm

Random Forest

Task

Multiclass Classification

Training Set

80%

Testing Set

20%

Random State

42

Cross-Validation

3 Folds

Evaluation Metrics

Accuracy

Precision

Recall

F1-Score

ROC-AUC

Log Loss

Out-of-Bag Score and Error

Confusion Matrix

Execution Time

Technologies Used

Python

Pandas

NumPy

Scikit-learn

Matplotlib

Seaborn

Kaggle Notebooks
