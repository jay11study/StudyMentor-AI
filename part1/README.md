# Part 1 – Data Acquisition, Cleaning and Exploratory Data Analysis

# Table of Contents
1. Project Overview
2. Dataset Description
3. Dataset Justification
4. Data Cleaning Summary
5. Descriptive Statistics
6. Skewness Analysis
7. Outlier Detection
8. Visualisation Interpretation
9. Pearson Correlation Heatmap
10. Imputation Strategy Comparison
11. Spearman Rank Correlation
12. Grouped Aggregation
13. Conclusion

## Project Overview

This notebook performs data acquisition, cleaning, preprocessing and exploratory data analysis (EDA) on the Student Performance dataset. The objective is to prepare a clean dataset for machine learning while understanding the characteristics of the data before modelling.

The cleaned dataset generated in this notebook will be used in Parts 2, 3 and 4 of the StudyMentor AI capstone project.

# Dataset Description

## Dataset Name

Student Performance Dataset (Portuguese Language)

## Source

UCI Machine Learning Repository

https://archive.ics.uci.edu/dataset/320/student+performance

## Description

The dataset contains demographic, family, social and academic information collected from secondary school students in Portugal. The objective is to analyse factors affecting student academic performance and later build predictive machine learning models.

The Portuguese language dataset (`student-por.csv`) was selected because it contains more student records (649) than the Mathematics dataset (395), providing more data for model training and evaluation.

# Dataset Justification

This dataset was selected because,
- It is a real-world educational dataset.
- It contains both categorical and numerical features.
- It is suitable for data cleaning, visualization and machine learning.
- The target variable (Final Grade - G3) is appropriate for prediction tasks.
- The dataset is publicly available and widely used for educational data mining research.

# Data Cleaning Summary

## Missing Values

A missing value analysis was performed on every column using:
- Count of missing values
- Percentage of missing values

No missing values were found in any column. Therefore, no imputation was required.

Although no missing values existed, the median imputation strategy was demonstrated because it is more robust than the mean for skewed numerical variables.

## Duplicate Records

Duplicate rows were checked using `df.duplicated().sum()`.

No duplicate records were found in the dataset. Therefore, no rows were removed and the null-value percentages remained unchanged.

## Data Type Conversion

Categorical string variables were converted from the object data type to the category data type.
This significantly reduced memory usage while preserving the original information.

Memory optimisation improves computational efficiency during later machine learning tasks.

# Descriptive Statistics

Descriptive statistics were calculated for every numerical variable using the `describe()` function.

The summary includes,
- Count
- Mean
- Standard Deviation
- Minimum
- Quartiles
- Maximum

These statistics provide an overview of the distribution and spread of each numerical feature before modelling.

# Skewness Analysis

Skewness was calculated for every numerical variable.

The variable failures had the highest absolute skewness (3.09), indicating a strongly positively skewed distribution.

Most students had no previous failures, while only a small number had one or more failures.

In positively skewed distributions, the mean is influenced by extreme high values. Therefore, the median provides a better measure of central tendency and would be preferred if missing values required imputation.

A negatively skewed distribution behaves similarly in the opposite direction, where extreme low values pull the mean downward, making the median more representative.

# Outlier Detection using IQR

Outliers were identified using the Interquartile Range (IQR) method.

Two variables were analysed,

## failures

The IQR analysis identified 100 observations outside the calculated bounds.

These observations were retained because previous academic failures represent genuine student information rather than measurement errors.

Removing these observations would remove meaningful educational information.

## absences

The IQR analysis identified 21 observations outside the calculated upper bound.

These values were also retained because unusually high absenteeism is realistic and may strongly influence academic performance.

Instead of removing these observations, they will be considered during model development in Part 2.

# Visualisation Interpretation

## Line Plot

The line plot shows the variation of final grades (G3) across all students.

Although individual grades fluctuate considerably, most students scored between approximately 10 and 16 marks.

## Bar Chart

The average final grade generally increases as study time increases.

Students with higher study-time categories achieved higher average final grades than students with lower study-time categories.
This suggests that study time may have predictive value.

## Histogram

The histogram of the failures variable confirms a highly positively skewed distribution.

Most students recorded zero previous failures, while relatively few students recorded one or more failures.

## Scatter Plot

The scatter plot between G1 and G3 shows a strong positive relationship.
Students who achieved higher first-period grades generally achieved higher final grades.

## Box Plot

The box plot shows that higher study-time categories generally have higher median final grades.

Some overlap exists between categories, indicating that study time alone does not completely explain academic performance.

# Pearson Correlation Heatmap

The Pearson correlation heatmap was computed for all numerical variables.

The strongest relationship was observed between,
- G2
- G3

with a correlation coefficient of approximately 0.919.

Although this is a very strong correlation, it does not necessarily imply causation.

A plausible explanation is that both variables measure academic performance across different assessment periods. Therefore, the relationship is expected because students who perform well in the second period are likely to perform well in the final examination.

# Imputation Strategy Comparison

The two most skewed variables were,
- failures
- Dalc

For both variables, the mean and median were compared before any imputation.

Because both variables are positively skewed, the median would be preferred over the mean since it is less sensitive to extreme values.

No imputation was performed because the dataset contained no missing values.

# Spearman Rank Correlation

Spearman correlation was compared with Pearson correlation for all numerical variables.

The three largest absolute differences were observed between,
- Dalc and absences
- absences and G3
- G1 and G3

These differences suggest that the relationships may be monotonic but not perfectly linear.

For feature selection in Part 2, Pearson correlation will primarily be used because the selected machine learning models assume approximately linear relationships, while Spearman correlation provides additional insight into possible monotonic behaviour.

# Grouped Aggregation

Students were grouped according to study time.

The analysis showed,
- Highest Mean Group: Study Time Category 3 (Mean = 13.23)
- Highest Standard Deviation Group: Study Time Category 2 (Standard Deviation = 3.24)
- Mean Ratio (Highest ÷ Lowest):1.22

Students in Study Time Category 3 achieved the highest average final grade, suggesting that increased study time is associated with better academic performance. However, Study Time Category 2 showed the greatest variation in final grades, indicating that students who study a similar amount can still perform quite differently.

The mean ratio of 1.22 indicates that the highest-performing study-time group achieved an average final grade approximately 22% higher than the lowest-performing group. This suggests that study time carries useful predictive information. However, the variation within each group shows that study time alone is insufficient to accurately predict student performance and should be combined with other variables during model development.

# Conclusion

The dataset was successfully inspected, cleaned and analysed.

Key findings include,
- No missing values were present.
- No duplicate records were identified.
- Memory usage was reduced through categorical data conversion.
- The failures variable exhibited the highest skewness.
- Outliers were retained because they represent genuine student behaviour.
- G2 and G3 showed the strongest correlation.
- Study time appears to have predictive value for final grades.

The cleaned dataset has been saved as `cleaned_data.csv` and will be used in subsequent modelling tasks.