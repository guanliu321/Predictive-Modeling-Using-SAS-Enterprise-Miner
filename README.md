# Predictive-Modeling-Using-SAS-Enterprise-Miner
This project is to build a model in a dataset of more than 41,000 records to predict the best number of customers buying term deposits of the bank, so as to achieve the purpose of reducing the bank's investment in marketing. 

#Perform a Chi-square test to explore and understand the relationship between the predictor variable and the target variable in the dataset, and preprocess the dataset, such as normalizing the variables in the dataset. 

#Use SAS to build multiple prediction models, such as Decision tree, Maximal decision tree, Logistic regression, Random forest, Support Vector Machines, Neural Networks and Auto-Neural Networks. 

#Use Area Under Curve (AUC) and The misclassification rate compares these seven models and determines the best two models as Neural Networks and Auto-Neural Networks. 

#Utilized:SAS Enterprise Miner,Decision tree, Logistic Regression, Random Forest, Support Vector Machines, Neural Networks,AUC,Misclassification Rate,Chi-square Test

1. INTRODUCTION

Marketing selling campaigns in enterprises are a form of organising marketing activities of product/services. By carrying out campaigns, it can drive more profit to the company that otherwise may not happen. Banking sector is one of the industries which uses such campaigning activities to provide monetary services to people and make profit. To do this, the banks engage in direct marketing by investing a lot of money and infra structure to gain capital. One way of direct marketing in selling is to contact the customers through phone. A call centre allows the bank to communicate with clients from different places.
The aim of our study in this project is to reduce the bank’s investment of resources towards marketing by predicting the right number of customers to approach for subscribing to a new bank product like term deposits. Here we are using a Portuguese bank market campaign dataset who sell term deposits. The project should be able to select the best of clients so that instead of spending on approaching all the customers, the bank can aim selected customers who are more likely to subscribe for the term deposits.

2. DATASET

The dataset used in this project is related to telemarketing campaigns of a Portuguese Bank Institution, University of California, Irvine (UCI). It is located in the machine learning repository of UCI at URL: https://archive.ics.uci.edu/ml/datasets/Bank+Marketing . The link contains four datasets from which we are using 2 datasets namely bank-additional-full.csv with all observations (20 inputs) and bank-additional.csv with 10% of full data (20 inputs). It contains examples from May 2008 to November 2010. The marketing campaign was based on calls and in order to know if the term deposit would be subscribed or not, same customer was contacted more than once.
As mentioned earlier the data set contains 20 input variables including client’s personal data like age, job, marital status, loan background etc., contact details like duration, last contacted details and social & economic attributes. The 21st variable will be the binary outcome variable ‘y’ which determines whether the customer subscribed to term deposit or not with 2 possible values ‘yes’, ’no’. The classification goal here is to predict if the client will buy the term deposit.

3. DATA EXPLORATION

To build any data model it is very important to first understand the data completely to maximum extent. The obtained data which is imported into SAS enterprise Miner has to be explored to get insights about what kind of data we have and what else is missing from the data since efficient models cannot be built from weak data.

A statistical examination of data gives us a clear picture about the dataset in our study, which would be helpful for our further analysis. To do the same, a descriptive statistic is drawn on the dataset using nodes like StatExplore, Multiplot which are available from the explore tab on the Toolbar of SAS enterprise Miner. Descriptive statistics are very useful in studying the important and basic patterns of data of our interest. They provide simple summaries about each of the variables which resides in the dataset. Along with descriptive statistics, charts for every variable are also plotted which helps an individual to visually observe possible patterns. Rather than presenting the statistics in numbers, graphs allow easy interpretation of facts about data, especially if the data is very large. We shall start finding insights about each of the variables in the dataset.
 
3.1.1 INTERVAL VARIABLES

We have 9 interval variables in the dataset. None of them have missing values, hence no imputation of values is required. All the interval variables of bank dataset are as explained below:

• age: It indicates age of the client. It seems that age does not have much impact on the target variable ’y’ since the variance between the two responses of ‘y’ for age is very less.


• Campaign: It indicates number of contacts performed for this campaign for a client. The value ranges from minimum of 1 to maximum of 56. 

• pdays: It indicates the number of days after the client was contacted for the last time from previous campaign. The values range from 0 to 27 days and also it has value ‘999’ which indicates that the customer was not contacted at all. Around 96% of the examples say that the client was not contacted. This data makes no sense to training the model since we are required to train a model with data where the customer was contacted and corresponding observations are taken into consideration. Hence, going further we have to either ignore the observations where pdays=999 or we can replace them with mean/median of variable. Let us select the second option for this study where pdays=999 are replaced and imputed with median of pdays = 6.

• cons.conf.idx: It is a monthly indicator which determines consumer confidence index. The value ranges from minimum of -50.8 to -26.9. It explains about the country’s current and future economic situation each month.

• cons.price.idx: It is a monthly indictor which determines consumer price index. The value ranges in decimal points from 92 to 95. It explains the changes in prices paid by consumers for goods and services each month. 

• emp.var.rate: It is a quarterly indicator which determines employment variation rate in the country. The value ranges from -3.4 to 1.4. 

• euribor3m: It is a daily indicator which determines the average interest with which the all European banks borrow from each other that mature after 3 months. 

• nr.employed: It indicates the number of persons employed and is a quarterly indicator. 

• previous: Indicates the number of contacts performed before the current campaign and for a particular client. 

• duration: The duration variable has been rejected in this analysis because if duration=’0’ then y=’no’ which means that we will not know the duration of call without calling the customer and this variable highly effects the target variable ‘y’.

3.1.2 NOMINAL VARIABLES

We have 10 nominal variables in our dataset and there are no missing categorical values and thus no imputation is needed. A review of all the nominal variables plot reveals the following observations.

• contact: The variable indicates the communication type of the campaign for a particular client. It has 2 possible values “cellular” and “telephone”. Around 63% of clients were contacted through “cellular” and around 37% of clients were contacted through “telephone”. The clients who were contacted through cell phone had more “yes” responses than who were contacted through telephone. 

• day_of_week: The variable tells the last weekday when the client was contacted. The possible values are 5 weekdays from “monday” to “friday”. 

• default: Indicates whether a client has a credit card provided by bank or not. The possible values are “yes”,”no” and “uknown”. 

• education: The categorical variable indicates the educational qualification of the client. It had 8 possible educational qualifications and it is found from the graph that the parameter did not affect the response variable ‘y’.

• housing: Indicates whether the client already has a house loan borrowed from bank. Includes 3 possible values with “yes”,”no” and “unknown”. 

• job: Indicates the type of job that a client is employed with. The bank had more clients who were working in admin and blue-collar jobs and its likely to see that they were the ones with more “yes” response for term deposit

• loan: The variable determines whether the client already has personal loan borrowed from the bank. The possible values being “yes”,”no” and “unknown”, customers who do not have prior personal loans in bank seems to buy the term deposits than the customers who already have personal loan.

• month: Indicates the last contact month of the year. Values ranging from Jan to Dec. 

• marital: Determines the marital status of bank clients. 

• poutcome: It is the outcome variable of previous campaign. The possible values include “success”,”failure” and “non-existent”.

• y: In the given dataset, it is observed that the target response ‘y’ has around 89% of “yes” responses and around 11% of “no” responses. 

Using the StatExplore node the following observations were done:

1.Chi-Square Plot

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.44.57%20AM.png)

A Chi-square statistic gives us the relationship between each of the variables and the target variable. The Chi-square statistic is very similar to the co-efficient of determination, R-squared value. It the measure of how much a variable can explain the variance in target variable. Since our target variable is categorical Chi-square statistic would be the best way of assessing variable relationships. Reviewing the above plot, we can select variables for our data models and thus do feature selection. From the graph it is evident that nr.employment variable has the highest Chi-square statistic followed by other variables like cons.conf.idx, emp.var.rate, pdays, poutcome, euribor3m, month and so on.

2.Variable Worth
The plot above present a graph through we can easily understand which variable is most related to the target variable and helps to select the best predictor variables. It gives each of the variable’s worth in predicting the target variable.
Here, we can see that consumer confidence index (cons_conf_idx) is serving as the best predictor and it is very likely that a customer’s spending activity and income stability accounts to predict whether the customer gets subscribed to a term deposit account or not. Further nr_employed followed by euribor3m, emp_var_rate, pdays, poutcome, month are determined as best predictors, in descending order.

3.Output

The output window provides a complete summary of the data in the form of numbers. The output window includes information like the measurement levels of variables and corresponding frequencies, summary statistics for each of the variable types separately and mainly the Target variable statistics with respect to each of the variables present in the dataset.

By examining this summary, we can get to know about what kind of data we have and if there are any missing values in the dataset, we can find them and later work on them to be replaced for better analysis.

Following are the observations made for the current BANK dataset, from the output window:

•From the dataset, 9 interval variables and 10 nominal variables were found.
