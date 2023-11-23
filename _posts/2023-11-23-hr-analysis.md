---
title: "🧑🏻‍🤝‍🧑🏽 HR Analysis on Employee Turnover! Full Data Science Process"
date: 2023-11-23 00:00:00 +0800
categories: [Full Process, Data Science]
tags: [data science, cleaning, eda, visualization, logistic regression, decision tree, random forest, feature engineering, recommendations]
---

## Data Science Process 
In this project, the following skills were applied: Cleaning, EDA, Logistic Regression, Decision Tree, Random Forest and Report

## Project Objective Overview
- Central Question: **Why causes employees to leave the company?**
- We are tasked to understand the employee turn over in the company.
- Based on this, we pull insights and strategical recommendations.
- Libraries used include: numpy, pandas, matplotlib, seaborn, sklearn (logistic regression, decision tree, random forest, gridsearch, metrics) and pickle to save the model.
- You can access the Jupyter Notebook IPYNB file here **[LINK](https://github.com/rydata/rydata.github.io/blob/main/portfolio/HR%20Analysis/Course%207%20Salifort%20Motors%20project%20lab.ipynb)**

## Project Findings Overview
### On Employees who left:
- Employees are generally overworked with almost double the regular monthly hours.
- Those who left either worked less hours and had only 2 projects assigned OR
- Are overworked with 255 - 300+ hours and had had more projects 4-7.
- Everyone with 7 projects assigned left. 
- Even highly satisfied employees, with more than 5 years are leaving due to lack of promotion and salary increase.
- Those with 4 years in the company, left due to drastic policy change.  

### On Employees who stayed:
- Staying employees had an average of 3-4 projects assigned, rendering monthly hours of 150-255 (still high compared to average of 167hrs)
- Satisfaction levels were generally high but lowered for tenure/years 5-6.

### On modeling:
- The logistic regression model approach had achieved high scores (79% precision, 82% recall, and f1 of 80%).
- The decision tree model and random forest had even better scores and performed similarly (94% precision, 91% recall, f1 of 93%, accuracy and auc 98%). 
- Feature Engineering was used to drop data which will not be realistically available.
- Second round of tree models were created. The random forest is the champion model and scored the ff on the test set: (87% precision, 91% recall, 89% f1, accuracy 96% and auc 94%)


### Recommendations at the end!


# Data Cleaning Process 

After importing the packages we can do our initial data cleaning

- head(), .info, .describe and .columns to better understand our data
- rename the columns to snake_case (lowercase and underscores) and correct mispellings

```python
df0 = df0.rename(columns={'Work_accident': 'work_accident',
                          'average_montly_hours': 'average_monthly_hours',
                          'time_spend_company': 'tenure',
                          'Department':'department'})
```

- .isnull(), .duplicated(), .drop_duplicates() to check for missing values and duplicates
- boxplot to check for outliers 

![outlier_boxplot](/portfolio/HR_Analysis/tenure_boxplot.png)
