# Part 3 – Advanced Modeling, Ensemble Learning and Machine Learning Pipeline

# Table of Contents

1. Project Overview
2. Decision Tree Models
3. Gini and Entropy Comparison
4. Random Forest
5. Gradient Boosting
6. Feature Ablation Study
7. Cross Validation
8. Hyperparameter Tuning
9. Manual Learning Curve
10. Model Serialization
11. Model Comparison
12. Conclusion

# Project Overview

This notebook focuses on advanced machine learning techniques for predicting student academic performance.

Several ensemble learning models were developed and compared to identify the most reliable model. Cross-validation, hyperparameter tuning and model serialization were also performed to improve model performance and create a reusable machine learning pipeline.

The objective is to select the best model for deployment while reducing overfitting and improving prediction accuracy.

# Decision Tree Models

## Default Decision Tree

A Decision Tree classifier was first trained using the default parameters.

Results,
- Training Accuracy: 1.0000
- Testing Accuracy: 0.8538

The training accuracy reached 100%, while the testing accuracy was much lower. This shows that the model memorized the training data instead of learning general patterns.

Decision Trees are called high-variance models because they grow by making greedy decisions at every split. They continue splitting until no further improvement is possible, which often causes overfitting.

## Controlled Decision Tree

A second Decision Tree was trained using the following parameters:

- max_depth = 5
- min_samples_split = 20

Results,
- Training Accuracy: 0.9461
- Testing Accuracy: 0.9000
- Test ROC-AUC: 0.9366

The controlled tree produced a much smaller difference between the training and testing accuracy compared to the default tree.

The max_depth parameter limits how deep the tree can grow, reducing overfitting. The min_samples_split parameter prevents the tree from creating splits based on very small groups of data, making the model more stable.

# Gini and Entropy Comparison

Two Decision Tree models were compared using different splitting criteria.

Results,
- Gini Testing Accuracy: 0.8846
- Entropy Testing Accuracy: 0.8923

Gini Impurity Formula.
Gini = 1 − Σ(pi²)

Entropy Formula,
Entropy = −Σ(pi log₂(pi))

A Gini value of zero means that every sample in the node belongs to the same class. Such a node is perfectly pure.

For this dataset, the Entropy criterion achieved slightly better testing accuracy than the Gini criterion.

# Random Forest

A Random Forest classifier was trained using:

- Number of Trees = 100
- Maximum Depth = 10
- Random State = 42

Results,
- Training Accuracy: 1.0000
- Testing Accuracy: 0.9000
- ROC-AUC: 0.9391

Top Five Important Features

1. G2 (0.262599)
2. G1 (0.198282)
3. failures (0.057526)
4. school_MS (0.033645)
5. higher_yes (0.032852)

Random Forest calculates feature importance by measuring the average reduction in Gini impurity contributed by each feature across all decision trees.

Unlike Linear Regression coefficients, feature importance does not indicate whether a feature has a positive or negative relationship with the target. Instead, it measures how useful the feature is for making predictions.

Random Forest uses a technique called bagging. Each decision tree is trained on a random sample of the training data created using bootstrap sampling. At every split, only a random subset of features is considered. The predictions from all trees are then combined to produce the final prediction. This reduces variance and makes the model more reliable than a single Decision Tree.

# Gradient Boosting

A Gradient Boosting classifier was trained using:

- Number of Estimators = 100
- Learning Rate = 0.1
- Maximum Depth = 3
- Random State = 42

Results,
- Test ROC-AUC: 0.9586

Gradient Boosting builds trees one after another. Each new tree learns from the mistakes made by the previous trees, gradually improving the model's performance.

# Feature Ablation Study

The five least important features identified by the Random Forest model were removed.

Removed Features

- Fjob_health
- Fjob_teacher
- Mjob_teacher
- guardian_other
- Mjob_health

Results,
- Full Random Forest ROC-AUC: 0.9391
- Reduced Random Forest ROC-AUC: 0.9532

The reduced model achieved a slightly higher ROC-AUC than the original model.

This suggests that the removed features added very little useful information and may have introduced unnecessary noise.

Using fewer features can reduce computational cost and simplify model maintenance without reducing prediction performance.

# Cross Validation

Five-fold Stratified Cross Validation was performed for all models.

Results

| Model | Mean ROC-AUC | Standard Deviation |
|------|------:|------:|
| Logistic Regression | 0.9565 | 0.0162 |
| Controlled Decision Tree | 0.8898 | 0.0436 |
| Random Forest | 0.9726 | 0.0162 |
| Gradient Boosting | 0.9594 | 0.0237 |

Cross-validation provides a more reliable estimate of model performance because every observation is used for both training and validation across multiple folds. This reduces the dependence on a single train-test split.

# Hyperparameter Tuning

GridSearchCV was used to find the best Random Forest model.

Parameter Grid

- n_estimators = 50, 100, 200
- max_depth = 5, 10, None
- min_samples_leaf = 1, 5

Results

- Parameter Combinations: 18
- Cross Validation Folds: 5
- Total Model Fits: 90

Best Parameters

- max_depth = 10
- min_samples_leaf = 5
- n_estimators = 200

Best Cross Validation ROC-AUC

0.9785

Grid Search evaluates every possible combination of parameters. Although it usually finds the best model, it requires more computation than Randomized Search, which tests only a random selection of parameter combinations.

# Manual Learning Curve

The tuned pipeline was trained using different portions of the training dataset.

| Training Fraction | Training AUC | Test AUC |
|------:|------:|------:|
| 20% | 1.0000 | 0.9314 |
| 40% | 0.9963 | 0.9323 |
| 60% | 0.9929 | 0.9336 |
| 80% | 0.9935 | 0.9468 |
| 100% | 0.9945 | 0.9436 |

The training AUC decreased slightly as more training data was used. This is expected because the model becomes less likely to memorize a larger dataset.

The testing AUC generally improved as more training data became available. This shows that additional data helps the model learn better.

The testing AUC began to stabilise near the end, suggesting that the model is approaching its best performance for this dataset.

# Model Serialization

The best machine learning pipeline was saved using Joblib as:

best_model.pkl

The saved model was successfully loaded again using joblib.load(), and predictions were generated for two sample student records without any errors.

This confirms that the trained model can be reused without retraining.

# Model Comparison

| Model | 5-Fold Mean AUC | 5-Fold Std AUC | Test AUC |
|------|------:|------:|------:|
| Logistic Regression | 0.9565 | 0.0162 | 0.9060 |
| Controlled Decision Tree | 0.8898 | 0.0436 | 0.9366 |
| Random Forest | 0.9726 | 0.0162 | 0.9391 |
| Gradient Boosting | 0.9594 | 0.0237 | 0.9586 |
| Tuned Random Forest | 0.9785 | - | 0.9436 |

Although Gradient Boosting achieved the highest Test ROC-AUC on the single test dataset, the Tuned Random Forest achieved the highest average ROC-AUC during five-fold cross-validation (0.9785). Cross-validation provides a more reliable estimate of how well a model will perform on unseen data because it evaluates the model on multiple train-test splits instead of only one.

For this reason, the Tuned Random Forest is selected as the final recommended model. It provides strong overall performance, good generalization and stable prediction results.

# Conclusion

Several advanced machine learning models were trained and compared.

The main findings are,
- The default Decision Tree showed clear signs of overfitting.
- Controlling the tree depth improved generalization.
- Random Forest performed better than a single Decision Tree.
- Removing the least important features slightly improved the Random Forest model.
- Cross-validation showed that Random Forest consistently produced strong results.
- GridSearchCV further improved the Random Forest through hyperparameter tuning.
- The trained model was successfully saved and reloaded using Joblib.

The Tuned Random Forest pipeline is selected as the final model because it achieved the best overall cross-validation performance while maintaining excellent prediction accuracy on unseen data.