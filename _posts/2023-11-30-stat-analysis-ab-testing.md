---
title: "🆎🧪 Significance Testing and Statistical Analysis on Taxi Revenue"
date: 2023-11-30 00:00:00 +0800
categories: [Statistics, ABTesting, NYCTLC-Series]
tags: [Statistical-Analysis, AB-Testing, Descriptive-Analysis, Python]
---


# A/B Testing and Statistical Analysis for NYC TLC Fare Payment 

![nyctaxi](/portfolio/ABTest_NYC/TaxiEmpireHotel.png)
*Empire Hotel in NYC Taken from an episode of Gossip Girl. Image Source: thenotsoinnocentsabroad.com/blog*

## Project Overview

- A/B Testing showed there is a statistically significant difference in average total payment between cash and credit card payments. 
- Further analysis shows that the difference might be due to tips. 
- Another A/B test was conducted without the tips, showing that there is no statistical difference in fare amount, when tips were not accounted.
- Using the groupby function, we see that tips are only recorded for credit card payments.
- Recommendations were given to incentivize logging of tips.


You can access the JUPYTER Notebook IPYNB file here **[LINK](httpx)**

## Objectives
- NYC TLC requests an analysis of the relationship between fare amount and payment type (cash vs credit card payments) via A/B testing.
- Answer: **Does different types of payment methods (cash vs credit card) amount to a statistically significant difference in total amount paid?**
- Provide recommendations to increase revenue for taxis.

# Project Process

## Project Context
- This output is part of a multiple series of outputs for New York City Taxi & Limousine Commission (NYC TLC)
- This is a simpler project more focused on gathering insight and analysis than technical process (as compared to our **[HR Analysis Output](https://rydata.github.io/posts/hr-analysis/)**).

## Steps Taken
### 1. Data Exploration
- use of .head, .describe, .shape and .groupby for initial analysis on our data.

```python
# grouping payment type and total amount
taxi_data.groupby('payment_type')['total_amount'].mean()
```

|payment_type|mean_total_amount|
| -------- | ------- |
|1 (Credit Card) |17.66| 
|2 (Cash) |13.55|
|3 (No charge) |13.58|
|4 (Dispute) |11.24|
|5 (Unknown) | None |

- From here we can see that credit card payments are much higher than other types of payments.
- This difference might be from random sampling rather than true difference. To investigate this, we can conduct a hypothesis test.


### 2. Hypothesis testing (Round 1)
- Our goal is to conduct a two-sample t-test. 

#### Identify our null and alternative hypothesis:
  - H0: There is no difference in the average total fare amount between customers who use credit cards and customers who use cash.

  - HA: There is a difference in the average total fare amount between customers who use credit cards and customers who use cash.

#### Choose a significance level:
- We choose a 5% significance level for our two-sample t-test. 5% is usually the industry standard and is requested for this project. 

- We use the ff code block to conduct our test:

#### Finding the p-value:

We use this code block to use scipy stats hypothesis testing library.

```python
# conducting our hypothesis test
cash = taxi_data[taxi_data['payment_type']==2]['total_amount']
credit_card = taxi_data[taxi_data['payment_type']==1]['total_amount']
stats.ttest_ind(a=credit_card, b=cash, equal_var=False)
```
Result:
Ttest_indResult (statistic=20.34644022783838, pvalue=4.5301445359736376e-91)



### 3. Hypothesis Testing Interpretation (Round 1)

Since p-value is significantly smaller than our significance level of 5%, we reject the hypothesis test.

We can conclude that there is a statistically significant difference in the average total fare amount credit card vs cash users.

### Insight!

 Clarifications has to be made regarding the larger payment for credit cards. It is recommended to look into the following:
  - First, is there a system bug that causes credit card users to pay more? What may have caused these? 
  - Second, it may be insightful to also look at the average amount of monthly rides for credit card users. 
    - Do credit card users tend to be more "power users"? 
    - Meaning are they the type of people that spend more on rides or go in longer amount of rides? 
  - Third, is looking at the differences that credit card offers. 
    - Are there any ongoing promotions for credit card users? 
    - Does the hassle free and cashless nature of credit card important to the riders? 
  

![cash_v_card](/portfolio/ABTest_NYC/cash_card.png)
*Img Source:www.moneymax.ph*

## Hypothesis Testing Part 2

Another comparison is the comparison of the fare amount, which does not include tips, only the base payment.
A second round of a/b testing can be looked into to answer this. 

### 1. Data Exploration (Round 2)

Instead of total amount paid, we use the fare amount to exclude tips.
```python
# Grouping payment type and fare amount mean
taxi_data.groupby('payment_type')['fare_amount'].mean()
```

|payment_type|mean_total_amount|
| -------- | ------- |
|1 (Credit Card) |13.43| 
|2 (Cash) |12.21|
|3 (No charge) |12.19|
|4 (Dispute) |9.91|
|5 (Unknown) | None |

Removing the tips, we see that there is not as much difference anymore between cash and credit card payments.

### 2. Hypothesis Testing (Round 2)


#### Identify our null and alternative hypothesis:
  - H0: There is NO difference in the average fare amount (excluding tips) between customers who use credit cards and customers who use cash.

  - HA: There is A difference in the average fare amount (excluding tips) between customers who use credit cards and customers who use cash.

#### Choose a significance level:
- In this case we retain 5% as our significance level

#### Finding the p-value:
We apply A/B testing with the same code block:

```python
cash_fare= taxi_data[taxi_data['payment_type']==2]['fare_amount']
credit_card_fare = taxi_data[taxi_data['payment_type']==1]['fare_amount']
stats.ttest_ind(a=credit_card_fare, b=cash_fare, equal_var=False)
```
Ttest_indResult(statistic=6.866800855655372, pvalue=6.797387473030518e-12)

- Assuming a significance value of 5%, we can see that there is no statically significant difference from cash and payment method.

### 3. Hypothesis Testing Interpretation (Round 2)

- Although further analysis on the possible 'bug' on higher amount for credit card users, this can be ruled out as there is less difference comparing the mean fare amount for cash and card.

We can do another `groupby` on payment type and `tip_amount` by its mean.

|payment_type|tip_amount|
| -------- | ------- |
|1 (Credit Card) |2.73| 
|2 (Cash) |0|
|3 (No charge) |0|
|4 (Dispute) |0|
|5 (Unknown) | None |

- We can observe that no tips are reported during cash payments, only at credit card.


# Conclusions and Recommendations

![tipping-img](</portfolio/ABTest_NYC/tipping picture.jpg>)
*Image Source: https://www.blackandwhitecabs.com.au*

## Insight
- It can be said that the higher amount for credit cards is due to the fact that tips are not recorded anymore by drivers for cash payments. 
  - It is worth investigating if the company takes a percentage of tips from the riders, disincentiving them from recording tips. 
- Additionally, it is possible that when paying with credit card, there is an option or requirement within the application to tip, leading to more pay. 
- Another explanation is that riders do not carry as much cash, so it is easier to pay with credit card for long trips. 
  - In this case, fare amount determines payment type rather than vice versa.

## Recommendations
- It can be seen that tips are no longer reported on the system on average compared to credit card payment methods. 
- It is possible for the team to look into methods to further incentivize recording of tips given, through the ff:
  - Performance Bonuses
  - Recognition and Rewards
  - Education and Training
  - Transparent Communications and Policies
  - Technological Systems Feedback
  - Further discussion with drivers
- Finally, conducting additional analysis on what causes tipping through interviews, surveys, additional data or FGD can be a viable step for the company.

# Thank you for your time reading!