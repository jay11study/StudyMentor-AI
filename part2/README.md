# Part 2 – Predictive Modelling

# Table of Contents

1. Project Overview
2. Dataset Description
3. Data Preparation
4. Regression Models
5. Regression Model Comparison
6. Regression Coefficient Interpretation
7. Logistic Regression Classification
8. Confusion Matrix Interpretation
9. ROC Curve and AUC
10. Logistic Regression Feature Importance
11. Threshold Comparison
12. Bootstrap Validation
13. Model Serialization
14. Conclusion

# Project Overview

This notebook builds machine learning models using the cleaned Student Performance dataset created in Part 1.

Two prediction tasks were completed,
- Predict the student's final grade (Regression)
- Predict whether the student passes or fails (Classification)

The models built in this notebook will be used in Part 3 for ensemble learning and in Part 4 for the LLM feature.

# Dataset Description

The cleaned dataset from Part 1 was used in this notebook.
Two target variables were used.

## Regression Target

Final Grade (G3)

## Classification Target

Pass

Students with:

- G3 greater than or equal to 10 were labelled as Pass (1).
- G3 less than 10 were labelled as Fail (0).

A passing mark of 10 was chosen because students need at least 10 marks out of 20 to pass in the Portuguese education system.

# Data Preparation

The following preprocessing steps were completed before training the models.

- Loaded the cleaned dataset.
- Created the Pass column.
- Removed the target columns from the features.
- Converted categorical columns using One-Hot Encoding.
- Split the dataset into training and testing datasets.
- Applied StandardScaler to scale the numerical features.

Scaling helps machine learning models perform better because all numerical values are brought to a similar range.

# Regression Models

Two regression models were trained to predict the final grade (G3).

## Linear Regression

Results,
- Mean Squared Error (MSE): 1.4759
- R² Score: 0.8487

The model explained about 85% of the variation in the final grades.

## Ridge Regression

Results,
- Mean Squared Error (MSE): 1.4755
- R² Score: 0.8487

Ridge Regression performed slightly better than Linear Regression.

It uses L2 regularization, which helps reduce overfitting by keeping the coefficient values smaller.

# Regression Model Comparison

| Model              | MSE    | R² Score |
|--------------------|--------|----------|
| Linear Regression  | 1.4759 | 0.8487   |
| Ridge Regression   | 1.4755 | 0.8487   |

Both models produced almost the same results.

Ridge Regression is slightly better because it has a lower Mean Squared Error and usually performs better on unseen data.

# Regression Coefficient Interpretation

The most important features were,

- G2
- G1
- failures
- Fjob_services
- Medu

G2 had the largest positive coefficient, which means it had the strongest effect on predicting the final grade.

Students who performed well in earlier exams usually performed well in the final exam.

The failures feature had a negative coefficient, which means students with more previous failures usually received lower final grades.

# Logistic Regression Classification

A Logistic Regression model was trained to predict whether a student would pass or fail.

Results,
- Accuracy: 91%
- ROC-AUC Score: 0.906

The model performed well and correctly classified most students.

The dataset contains more passing students than failing students, so the classes are slightly imbalanced.

# Confusion Matrix Interpretation

The confusion matrix produced the following results.

- True Positives: 105
- True Negatives: 13
- False Positives: 7
- False Negatives: 5

The model correctly predicted most students.

Only a small number of students were classified incorrectly.
The overall accuracy of the model was 91%.

# ROC Curve and AUC

The ROC curve was created using the predicted probabilities.

The model achieved an AUC score of 0.906.
An AUC value above 0.90 means the model is very good at separating students who pass from students who fail.

The ROC curve is much higher than the random prediction line, showing good model performance.

# Logistic Regression Feature Importance

The largest Logistic Regression coefficients were:
- G2
- G1
- school_MS
- Fjob_other
- Fjob_services
- age
- failures
- romantic_yes
- absences

G2 and G1 were the most important features.

This shows that previous exam scores are the strongest indicators of final student performance.

Features like failures and absences had negative coefficients, showing that they reduce the chance of passing.

# Threshold Comparison

Different probability thresholds were tested.

The default threshold of 0.50 gave the best balance between predicting passing students and failing students.
Changing the threshold changes the number of correct and incorrect predictions.

# Bootstrap Validation

Bootstrap sampling was used to check whether the Logistic Regression model gives stable results.

The average accuracy remained close to the original test accuracy.
This shows that the model is stable and performs consistently on different samples.

# Model Serialization

The trained models were saved using Joblib.

The following files were created,
- linear_regression.pkl
- ridge_regression.pkl
- logistic_regression.pkl

Saving the models allows them to be loaded later without training them again.

These models will be used in Parts 3 and 4.

# Conclusion

The machine learning models were successfully trained and evaluated.

The main findings are,
- Linear Regression predicted the final grades with good accuracy.
- Ridge Regression performed slightly better than Linear Regression.
- Logistic Regression achieved 91% accuracy.
- The ROC-AUC score of 0.906 shows that the classifier performs well.
- G1 and G2 were the most important features in both regression and classification.
- The trained models were saved successfully and will be used in the next parts of the project.

This notebook completes the predictive modelling stage and prepares the project for ensemble learning and model tuning in Part 3.