# Comparing-Classifiers
**Alessandro Morato**

**BH-PCMLAI, January 2024**

## 1. Problem Statement
The increasingly vast number of marketing campaigns over time has reduced its effect on the general public. Furthermore, economical pressures and competition has led marketing managers to invest on directed campaigns with a strict and rigorous selection of contacts. Such direct campaigns can be enhanced through an application of Data Analysis and Machine Learning techniques.

This work describes an implementation of a DM project based on the CRISP-DM methodology. Real-world data were collected from a Portuguese marketing campaign related with bank deposit subscription. The business objective is to find a model that can explain success of a contact (i.e. if the client subscribes the deposit). Such model can increase campaign efficiency by identifying the main characteristics that affect success, helping in a better management of the available resources (e.g. human effort, phone calls, time) and selection of a high quality and affordable set of potential buying customers.

## 2. Description of the Analysis
The problem was investigated with the use of the CRISP-DM framework, to produce and compare four classification models that can be used to predict whether a consumer contact led to a subscription in a financial product offered by the bank. The CRISP-DM approach covers:

- Understanding the business problem
- Understanding the data
- Preparing the data for modeling
- Modeling the data
- Evaluating the models
- Deploying

The preliminary data analysis required a significant effort, but it is a crucial passage in every ML project. Main steps were (i) missing/duplicated values management, (ii) understanding of features and preliminary plotting, (iii) filtering outliners in numerical features.

The dataset provided included features related to the bank and features related to the reneral economic situation. The analysis was tailored on the features provided by the bank, neglecting the remaning ones. The features considered in the analysis are:

- age
- job
- marital
- education
- default
- housing
- loan
- contact 
- month
- day_of_week 
- campaign
- previous
- poutcome
- pdays

Additional feature engineering on these columns was carried out, encoding some of them to change from categorical to numeric or to be more functional.

The processed data was then used to feed four models, each one evaluated based on accuracy and fit time, and then tuned them for improved precision. The 4 models are:(i) Logistic Regression, (ii) KNN, (iii) Decision Tree and (iv) SVC. High precision ensures that when the model predicts a customer will accept the coupon, it is usually correct. This helps in minimizing the cost and effort of targeting customers who are unlikely to sign with the bank. Considering the Business objective, a metric able to minimize the resources invested by the bank seemed ideal in this application.


## 3. Results
A baseline "model" was initially considered. In this case, the baseline was simply the majority class of the dataset: every prediction is called as the most common value. The baseline was compared with the 4 models not optimized. In terms of accuracy almost all models (except KNN) underperform the baseline model.

![image](https://github.com/user-attachments/assets/a765c08c-664b-4aca-9790-9ab5234182e8)

These results highlight how the dataset is unbalanced and how "accuracy" cannot be considered a reliable metric, strongly influenced by the predominant class (people not subscribing a bank account).

The analysis is carried again by optimizing the above 4 models, in function of the "precision" metric instead. Precision scores greatily improved, compared to no-optimized models. Even if accuracy is not the metric we are interested in, its scores also improved and are quite alligned each other.

![image](https://github.com/user-attachments/assets/aa7f8f86-dae5-4cca-a2cd-949d57e20cb2)


## 4. Conclusions
The dataset is very unbalanced, with more than 80% of rows referring to potential customers who didn't subscribe a deposit. Because of this, "accuracy" is not a reliable metric: all the models investigated provide high values, but this is a metric highly influenced by the majority group (i.e. people who didn't subscribe a deposit). Prove of this is the baseline metric: a model always predicting the majority group ("no") already provides an accuracy pretty high, actually higher than almost every no-optimized model considered.

To achieve the Business Objective, a more meaningful metric is required. "Precision" ensures that when the model predicts a customer will accept the coupon, it is usually correct. This helps in minimizing the cost and effort of targeting customers who are unlikely to sign with the bank.

Considering the Business objective, a metric able to minimize the resources invested by the bank seems ideal. According to this approach, an optimized KNN model provides the highest value of precision (66%, evaluated on test dataset), with a not negligeble efficiency in term of elapsed time. Another valuable option is the Decision Tree, with a slighly lower precision (63%, test dataset) and twice the time to fit; its recall is a bit higher though. Logistic Regression provides a fit time similar to decision tree, but with a worse precision. SVM provides a not very high precision value, with a huge time required to fit: not a recommended option.

## 5. Next Steps
- Considering the very unbalanced nature of this dataset, I would recommend to take actions to "rebalance" it. This means adopting techniques of oversampling (for minority group) or undersampling (for majority group). I tried something during this analysis but I didn't -trust the results. A more methodic approach should be developed in this topic.
- The model-optimization of this analysis focused on "precision". I would suggest to extend this optimization to other metrics as well, like "roc_auc". This should allow to get a better balance between precision and recall performance.
- I would also invest more resources in indentifying a set of "main features": this would allow to make the computational analysis more agile and find better optimized models. According to the correlation matrix, some features look correlated, so this could provide interesting insights to better understand the dataset. 
- Another interestng application would be considering an "ensamble" approach, structuring more models to work together and trying to overperform the results from a single model.

## References
The Jupyther notebook used to develop this analysis:

https://github.com/emmetizeta/Comparing-Classifiers/blob/main/prompt_III.ipynb

The dataset object of this analysis:

https://github.com/emmetizeta/Comparing-Classifiers/blob/main/bank-additional-full.csv

Documentation of the dataset:

https://archive.ics.uci.edu/dataset/222/bank+marketing

