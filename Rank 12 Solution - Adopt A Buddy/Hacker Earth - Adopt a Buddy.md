Hacker Earth: Machine Learning Challenge - Adopt a buddy

Problem Statement

A leading pet adoption agency is planning to create a virtual tour experience for their customers showcasing all animals that are available in 
their shelter. To enable this tour experience, you are required to build a Machine Learning model that determines type and breed of the 
animal based on its physical attributes and other factors.
Data Description:

The data folder consists of 2 CSV files
   • **train.csv** - 18834 x 11
   • **test.csv** - 8072 x 9

Exploratory Data Analysis (EDA):

1.	It appears that breed category 2 is a minority class. We can use Smote from imblearn to oversample this class
2.	It appears that pet category 0 and 4 are among minority classes. We can use Smote from imblearn to oversample these classes
3.	More than half of the features are among minority classes, we can extract first word to create new color feature to reduce the classes here
4.	Both the features length and height can be dropped which led to improvement of score by 1
5.	If using dimension features - convert to same unit (m/cm)
6.	Length and Height both tend to have wide distribution which is seen through the distribution plots
7.	Drop the pet dimension columns and x2 if required as they are weakly correlated and don't have enough predicting power for the 2 target variables
8.	2 records exist where the listing date is less than the issue date, convert them to positive
9.	Generate time features - e.g. Quarter, weekend, month, year
10.	Generate master color feature from the available color type
11.	Standard scale the data except for categorical features


Feature Reduction:

ANOVA F-value For Feature Selection: 
The features are quantitative, compute the ANOVA F-value between each feature and the target vector. 
The F-value scores examine if, when we group the numerical feature by the target vector, the means for each group are significantly different

Features dropped: dimension features – length & height (scores as low as 0 & 1)

Model Building:

CatBoost Model with KFold cross validation (n_splits = 6)
Part 1: Predict the pet category target class
•	Predict the target variable pet category which is independent of the breed category class
•	Model: CatBoost --> KFold splits: 6
Part 2: Predict the breed category target class
•	Predict the target variable breed category which is dependent of the pet category class
•	Model: CatBoost --> KFold splits: 6
Results:
Achieved a F1Score of 90.76 on leaderboard using CatBoost Classifier