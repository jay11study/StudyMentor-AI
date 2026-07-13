# StudyMentor AI

StudyMentor AI is a Machine Learning and Large Language Model (LLM) project developed as part of an AI and Machine Learning capstone.

The project analyses student academic performance using real educational data and builds machine learning models to predict whether a student is likely to pass or fail. It also integrates a Large Language Model (LLM) to generate easy-to-understand explanations for each prediction.

The project is divided into four parts, covering the complete machine learning workflow from data preparation to model deployment and LLM integration.

| Project  | StudyMentor AI |
|--------- |----------------|
| Language | Python |
| Dataset  | Student Performance (UCI) |
| Machine Learning | Scikit-learn |
| LLM      | OpenRouter API |
| Models   | Linear Regression, Logistic Regression, Decision Tree, Random Forest, Gradient Boosting |

# Project Objectives

The objectives of this project are:

- Clean and prepare a real-world dataset.
- Perform exploratory data analysis (EDA).
- Build regression and classification models.
- Compare different machine learning algorithms.
- Improve model performance using ensemble methods.
- Tune model hyperparameters using GridSearchCV.
- Save and reload the best machine learning model.
- Integrate a Large Language Model (LLM) to explain predictions.
- Apply structured JSON validation and basic AI safety guardrails.

# Dataset

Dataset Name - 
Student Performance Dataset (Portuguese Language)

Source - 
UCI Machine Learning Repository
https://archive.ics.uci.edu/dataset/320/student+performance

Description:
The dataset contains demographic, family, social and academic information collected from secondary school students in Portugal.

The Portuguese dataset (`student-por.csv`) contains 649 student records and was selected because it provides more training examples than the Mathematics dataset.

# Project Structure

StudyMentor-AI
│
├── part1
│   ├── data
│   ├── notebook
│   ├── output
│   ├── plots
│   └── README.md
│
├── part2
│   ├── data
│   ├── notebook
│   ├── output
│   ├── plots
│   └── README.md
│
├── part3
│   ├── data
│   ├── notebook
│   ├── output
│   ├── plots
│   └── README.md
│
├── part4
│   ├── data
│   ├── notebook
│   ├── output
│   └── README.md
│
├── requirements.txt
└── README.md

# Project Workflow

## Part 1 – Data Acquisition, Cleaning and Exploratory Data Analysis

This part focuses on understanding and preparing the dataset.

Activities completed:

- Data acquisition
- Missing value analysis
- Duplicate detection
- Data type optimisation
- Descriptive statistics
- Skewness analysis
- Outlier detection using IQR
- Correlation analysis
- Data visualisation
- Feature exploration
- Cleaned dataset generation

Output:
- cleaned_data.csv

## Part 2 – Machine Learning Models

This part develops both regression and classification models.

Regression models:
- Linear Regression
- Ridge Regression

Classification models:
- Logistic Regression

Activities completed:

- Feature encoding
- Feature scaling
- Train-test split
- Regression evaluation
- Classification evaluation
- Confusion matrix
- ROC Curve
- Feature importance analysis

## Part 3 – Advanced Machine Learning

This part improves the classification models using ensemble learning.

Models implemented:
- Decision Tree
- Controlled Decision Tree
- Random Forest
- Gradient Boosting

Additional tasks:
- Feature importance
- Feature ablation study
- Cross-validation
- GridSearchCV
- Machine learning pipeline
- Manual learning curve
- Model serialization using Joblib

Output:
- best_model.pkl


## Part 4 – LLM Powered Prediction Explanation

This part integrates a Large Language Model (LLM) with the trained machine learning model.

Activities completed:
- OpenRouter API integration
- Prompt engineering
- Structured JSON output
- JSON schema validation
- Prediction explanation
- Temperature comparison
- PII guardrail
- End-to-end prediction explanation pipeline

# Technologies Used

Programming Language:
- Python

Libraries:
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- Requests
- JSONSchema
- python-dotenv

Development Environment
- Jupyter Notebook
- Visual Studio Code

# Machine Learning Techniques

The project demonstrates the following techniques:

- Data Cleaning
- Exploratory Data Analysis (EDA)
- Feature Engineering
- One-Hot Encoding
- Feature Scaling
- Regression
- Classification
- Ensemble Learning
- Cross Validation
- Hyperparameter Tuning
- Pipeline Creation
- Model Serialization
- Large Language Model Integration
- Prompt Engineering
- Structured Output Validation

# Results

The project successfully demonstrates the complete machine learning lifecycle.

Key achievements include:
- Cleaned and analysed a real-world educational dataset.
- Built multiple regression and classification models.
- Compared model performance using ROC-AUC and cross-validation.
- Improved model performance using ensemble methods.
- Saved and reloaded the best-performing model.
- Integrated a Large Language Model to explain predictions.
- Implemented JSON schema validation.
- Added PII detection to improve safety before API calls.

# How to Run the Project

1. Clone this repository.
2. Install the required libraries.
pip install -r requirements.txt

3. Create a `.env` file in the project root and add your OpenRouter API key.

4. Run the notebooks in the following order:
- Part 1
- Part 2
- Part 3
- Part 4
Each notebook uses the outputs generated by the previous part.


# Repository Contents

This repository contains:
- Jupyter notebooks
- README documentation
- Trained machine learning model
- Cleaned dataset
- Generated outputs
- Visualisations