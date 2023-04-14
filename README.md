# Credit Card Fraud Detecttion: Project Overview

This is a project from Kaggle. The dataset contains transactions made by credit cards in September 2013 by European cardholders.
The dataset is highly unbalanced.There are 492 frauds and 284,315 clean transactions. The positive rate (frauds) is only 0.172%.

The dataset contains time-instance, transaction amount, class(fraud or not) and numerical input variables which are the result of a PCA transformation. The original features and background information are not provided. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependant cost-sensitive learning. Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.

With a high unbalanced ratio, a direct applying of classification could lead to high variance. We apply downsampling method to the non-fraud class by randomly sample data from class 0 and build model on the resampled dataset.


## Main Manipulations

- Analysis the data, exstracting the frequency and transaction amount patterns of frauds
- Building Random Forest and XGboost models for predicting fraudulant transactions
- Building neural network work with Tensorflow to detect fraudulant transactions

## Code and Resources Used

**Python Version:** 3.10 \
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, tensorflow \
**Data Source:** https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

## EDA
- Aggregate the transactions in unit hour. The data provide instances in seconds, by gathering the events in hours, we found a main difference between fraud and non-frand transaction
- Re-scale the data with RobustScaler. We found that fraud transaction are more tend to be small in amount. There are sporadic large fraud transaction as outlier. We resclae the data to reduce the risk to sabotage the behavior of the models

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/amount_frequency.png" width="1100" height="450" />
</p>


The data contains records in unit seconds, which elapsed between each transaction and the first transaction in the dataset. There are more than 280,000 in the dataset, the enormous records bury the pattern of the collective behavior. We construct a column "hour" by aggregating the transation amount in each hour. We should the relation between the amount and time. From the graph we can see that for non-fraud transaction, there is an obvious period which is about 24 hours. This can be easily explain that true transactions occored within normal working hours and the peaks mark at day time. There are certain transaction happen at night. For fraudulant transaction, there is no pattern. The fraudster keep attack the system in short intervals. A possible reason is that with large attack rate and small transaction amount, the fraudster and hide the tracks an acumulate considerable quota.

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/fraud_amount.png" width="850" height="450" />
</p>

In this graph we plot the transaction amount versus time instance. There is no obvious correlation between the two variables. A key feature is that the fraudulant transaction amount are mainly small (around 500), which confirms the assumption from previous observation. There are some large transactions look like outliers. The reason could be that the fraudster sometime take a bold move to steal a large amount or that the transactions are from different fraudster with different strategy.

## Modeling
<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/RandomForest_n.png" width="600" height="450" />
</p>

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/RandomForest_ROC.png" width="600" height="450" />
</p>




