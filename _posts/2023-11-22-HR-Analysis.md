---
title: "🧑🏻‍🤝‍🧑🏽 HR Analysis on Employee Turnover! FULL DATA SCIENCE PROCESS"
author: Ryan Lotilla
date: 2023-11-22 00:00:00 +0800
tags: [Data Science, Cleaning, EDA, Visualization, Logistic Regression, Decision Tree, Random Forest, Feature Engineering, Recommendations] 
pin: true
math: true
---

# Understanding Turnover for Salifort Motors
## Data Science (Cleaning, EDA, Logistic Regression, Decision Tree, Random Forest and Report)
## Findings 

Through analysis employee who leave likely fall into these 4 groups: 
1. Churned 1 includes:
- Significantly worked less hours with only 2 projects assigned
- dissatisfied and with lower tenure, 3 years and below
- This subgroup have lower tenures, worked less hours and had less projects assigned.

2. Churned 2 includes:
- Significantly more hours worked and more projects assigned
- Everyone with 7 projects assigned left
- This subgroup may have been exposed to overwork or experienced burnout.

3. Churned 3 includes:
- High satisfaction, but very significant amount of monthly work hours 225 - 275.
- High satisfaction, with higher tenure (more than 5 years) but still left
- This subgroup may have left due to lack in promotion and salary increase.

4. Churned 4 includes:
- 4 Year tenure with very low satisfaction
- This subgroup may have experienced impactful changes.
- Further investigation of changes in policies required.

Meanwhile employees who stayed have the ff experiences:
- An average of 3-4 projects assigned. Still with high monthly hours of 150-255 hours, from the average 166.7
- Satisfaction level ranges were relatively high for tenures 2-4, lowered for tenures 5-6, then returned to the initial ranges for 7 and above years.

## Project Flow Overview
### Planning
1. Data Cleaning - Checked for Missing Values, Duplicates and Outliers (using Interquartile range)

### Analyzing
2. Data Exploration and Visualization - Visualized and identified important relationships between important variables through heatmaps, boxplots, histograms etc.

### Model Construction
3. Logistic Regression model is shown to be a good predictor
4. Decision Tree model showed even greater performance
5. Random Forest model showed great performance also
6. Feature Engineering - Created a new column for "overworked" employees based on monthly hours. Variables that will be not be realistically available were dropped.
7. Model Reconstruction B & C - A second round of tree based models were created based on new features

### Reporting and Evaluation
8. Evaluation: Feature Importances were created for both tree based models.
9. Recommendations: Findings, and Next steps were reported.



This post contains a deep dive into a Human Resource dataset outlining the steps taken to understand what is causing turnover in the company. Insights are provided across the 
