# Comparing-Classifiers
Compare the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines) on Marketing campaign data.

The objective of the task is to `optimize` the marketing campaign. This includes identifying the important factors and their impact in the Decision Making of a customer. We also need to create a model that gives us an idea of `likelihood` of a customer buying the term plan.
The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns. This data represents 17 marketing campaigns. It consists of `21 features` including both categorical and numerical variables.

Firstly, I had taken all the 21 features into account, prepared the features and did the complete comparison analysis with different modeling techniques.

As part of the exploratory data analysis,
1. In the distribution of `poutcome` status by subscription, we could see that the Success rate is higher if the last campaign was failed.
2. In the distribution of `month` status by subscription, Success ratio is better in the months of March, September, October and December. This could also be because of the sampling bias.
3. `day_of_week` doesn't seem to have any varying impact. We would drop it for purpose of modeling.
4. A slight difference in the success rate based on `housing` status is present.

The `Categorical` columns were one-hot encoded as they are not ordinal and the `Numerical` Features were scaled between 0 and 1 using MinMax scaler.
Duplicates were removed too.

| #Model | #Train Time | #Train Accuracy | #Test Accuracy | #Precision | #Recall | #F1 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Logistic Regression | 1.350925 | 0.910693 | 0.908605 | 0.680328 | 0.404315 | 0.507202 |
| K-Nearest Neighbors(KNN) | 0.015157 | 0.918326 | 0.892415 | 0.578261 | 0.277662 | 0.375176 |
| Decision Tree | 0.233961 | 1.000000 | 0.883915 | 0.501038 | 0.503827 | 0.502429 |
| SVM | 15.455619 | 0.903823 | 0.898162 | 0.718826 | 0.204593 | 0.318527 |


##### Logistic Regression has the Highest F1 Score. We are using the F1 score as evaluation metric, because of imbalance in Target Class Variable.

Secondly, I used just the bank information features (columns 1 - 7), prepared the features and the target column for modeling with appropriate encoding and transformations.

`LabelEncoder` was used for encoding the categorical variables such as `job`, `marital`, `education`, `default`, `housing`, `loan`, I did a few experiments to compare the `SimpleImputer` and the `IterativeImputer`.
Considering the base imputer as `Bayesian Ridge`, I estimated the score(neg mean square error) on the entire dataset by filling missing values by mean and median. Also used 3 different estimators to find the imputation method with the smallest error.
`SimpleImputer` had the lowest error, so used this with the `Median` strategy.

Using the default settings for each of the models,

| #Model | #Train Time | #Train Accuracy | #Test Accuracy |
| :---: | :---: | :---: | :---: |
| Logistic Regression | 0.075283 | 0.763077 | 0.761364 |
| K-Nearest Neighbors(KNN) | 0.015791 | 0.781795 | 0.703648 | 
| Decision Tree | 0.017253 | 0.869615 | 0.572069 |
| SVM | 1.511302 | 0.763077 | 0.761364 |

As part of improving the model accuracy, I did a few data transformations like using MinMax scalar on the `age` feature and created dummies for the categorical features. Also did grid search with additional hyperparameters.

| #Model | #Train Time | #Accuracy | #Precision | #Recall |
| :---: | :---: | :---: | :---: | :---: |
| Logistic Regression | 0.047673 | 1.0000 | 1.0 | 1.000000 |
| K-Nearest Neighbors(KNN) | 0.005939 | 0.9686 | 1.0 | 0.868421 |
| Decision Tree | 0.005005 | 1.0000 | 1.0 | 1.000000 |
| SVM | 0.366605 | 1.0000 | 1.0 | 1.000000 |

