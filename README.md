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

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.45.21%20AM.png)

The plot above present a graph through we can easily understand which variable is most related to the target variable and helps to select the best predictor variables. It gives each of the variable’s worth in predicting the target variable.
Here, we can see that consumer confidence index (cons_conf_idx) is serving as the best predictor and it is very likely that a customer’s spending activity and income stability accounts to predict whether the customer gets subscribed to a term deposit account or not. Further nr_employed followed by euribor3m, emp_var_rate, pdays, poutcome, month are determined as best predictors, in descending order.

3.Output

The output window provides a complete summary of the data in the form of numbers. The output window includes information like the measurement levels of variables and corresponding frequencies, summary statistics for each of the variable types separately and mainly the Target variable statistics with respect to each of the variables present in the dataset.

By examining this summary, we can get to know about what kind of data we have and if there are any missing values in the dataset, we can find them and later work on them to be replaced for better analysis.

Following are the observations made for the current BANK dataset, from the output window:

•From the dataset, 9 interval variables and 10 nominal variables were found.


![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.45.38%20AM.png)

•Target variable relationship with other variables


![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.46.47%20AM.png)

The table provides a brief of how much each of the variables can account in
variable ‘y’. The column Variable Worth contains the log worth values of variables corresponding to the target variable. Higher the value more the variable can explain the response the variable. The plot in the previous section also explains the same numeric in the form of graph.

The column Variable Importance ranks each of the variable for predicting the Target variable, depending on the variable worth values.

From the table, we can see that variable “cons_conf_idx” can highly contribute than any other variables, to predict the response variable and variable “day_of_week” contributes the least.

4. DATA ANALYSIS AND PREPARATION

4.1.1 Data Partition

The raw bank dataset is now set to divide into train data and validation dataset. Separating data into train, test and validation data is very important when we build data models and very useful during the evaluation of data models. Typically, when we separate a data, a larger partition is used for training the model and smaller partition is used for validating/testing the model and later we check the built model with validation data to make sure there is no existence of overfitting of model. In our project, we are using only train and validation data partitions since testing is not included here.

• To carry out data partition in SAS enterprise Miner, we have a node named Data Partition in Sample section of SEMMA tool bar.

• In the properties panel of Data Partition, data allocations tab has been set to 55% of training data and 45% of validation data.

• The data partition method used here is default which selects to stratify the data on target variable. Since we have 89% of “no” responses and 11% of “yes” responses in target variable, Stratifying ensures that both responses “no” and “yes” are well- represented in data partitions.

• Once we run the node, the data gets partitioned with proportions as mentioned above and we can see the same in results. In addition, we can also see the proportion of each variable which got partitioned into train and validate data.
![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.47.04%20AM.png)

4.1.2 Data Replacement

As discussed earlier in Data analysis part, we observed that the variable pdays contains a value ‘999’ which needs to be replaced. Here, we are replacing these values with missing values(.) in both training and test data sets.

• For data replacement in SAS Miner, we have a node called Replacement in the Modify section of SEMMA tool bar. The partitioned data node is connected to replacement node.

• The replacement window of interval variables has been customised to add missing values as replacement for pdays=999 in properties panel and Default limit methods has been switched to none since we do not want to enforce the replacement and we will do it manually.

• In replacement editor of interval variable, we specify the variable to be replaced and what values to be replaced.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.47.19%20AM.png)

Since we want all ‘999’ to be replaced we will specify the Replacement upper limit as ‘998’ which replaces all values greater than ‘998’

• Once we run the node, the output window gives the number of values replaced in both training and validation dataset.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.47.31%20AM.png)

A total of (21857+17816) 39673 values in pdays have been replaced as missing values(.)
We can also see an added column in the dataset named Replacement: pdays which holds the replaced column values of pdays

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.47.41%20AM.png)

Now the data is ready for data modelling. In the next section, we shall start implementing different machine learning algorithms to build predictive models.
  
5.DATA MODELLING

The aim of our project is to build predictive models for the bank dataset by using all relevant algorithms available in SAS enterprise miner and evaluate each of them to find the best model for predicting the target variable ‘y’. So here we are starting with training a decision tree model since this model does not need imputation to deal with missing values.

1.DECISION TREE:

Decision Tree is a supervised learning algorithm which is easily understood and interpreted among all classification algorithms. It is mostly used for classification problems but also for regression problems. When training a dataset to classify a variable, the decision tree makes smaller subsets of data based on certain node rules until the target variable falls under one category. The selection of variables to be splitted is calculated by the system based on parameters like maximum information gain.

Here in this project we are building 2 models using decision tree, one is the interactive or maximal decision tree model and another one is an auto-pruned decision tree model. To manage the missing values in decision trees, we have customised the algorithm to use up to 4 surrogate rules when it encounters an input value with missing observations.

1a. Maximal Decision tree:

The Maximal decision tree works as an interactive decision tree where a user can select the variables to be splitted at each node of the tree. The basic idea of maximal tree is the decision tree is splitted upto maximum extent using all of the variables resulting in a massive decision tree. The algorithm is Chi-square driven and the selection of variables at nodes depend on the Chi-square driven statistic value -log(p) of the variables. Since the model is interactive, we can see which variables have the best Chi-square statistic and also the best point at which the node gets splitted to. Each time a variable is selected and node is created, for the next node the variables -log(p) decreases which explains that the current variable becomes the leaf node for the first selected variable.
In SAS enterprise we have got number of algorithms to use in which we can choose Decision tree for now. The maximal decision tree is created by using the Train node option which splits the decision tree to maximum number of branches. Below is the maximal tree created.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.50.25%20AM.png)

 As we can see, the tree contains a number of branches and leaf nodes. The tree in total contains 54 leaf nodes. The misclassification rates for the model are 0.0972 and 0.0991 respectively for train and validate data.
 
The maximal tree is not best decision tree to use, the reason is that specifying too many splits in the decision tree results in overfitting of the data model to the current dataset which should not happen. If we happen to select a smaller number of variables then we will get a higher accurate predictive data model when it is exposed to an unknown dataset. Hence, the decision tree needs to be pruned and it will be done in our next model.

1b. Regular decision tree (Auto-pruned):

In regular decision tree the subtree method is selected as Assessment, which means that the decision tree first creates a maximal tree and then prunes the same to get a final effective decision tree with reduced set of branches. Here, we know that the target outcome should be ‘1’ or ‘0’ and thus we select the assessment measure as Decision. This tries to optimise the branches that would decide to predict a ‘1’ or ‘0’ for target variable.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.53.05%20AM.png)

As we can see from above built model, the original decision tree is trimmed to 44 leaf nodes. The leaf nodes have been decreased by 10 numbers which results in better performance when it is used for a new dataset. The misclassification rate is found to be 0.0986 and 0.099 for train and validation data respectively.

2. REGRESSION

Before doing regression, we have to consider that whether our data meets the criteria for being analysed using regression. The things we have to check about is missing values in the columns of data and the considering the transformation of variables which are not normal.

a. Handling missing values

In case of decision trees handling the missing values is not a problem since we have surrogate rules for rescue. This specification allows SAS enterprise miner to use upto the mentioned number of surrogate rules in each non-leaf node if the splitting rule depends on an input having missing values. But in regression, the case is that the algorithm automatically ignores the observations which contains 50% of missing values. Hence if we want to make use of all the data, we have to impute the missing values. Until now we have got missing values in only one variable i.e. pdays. In this study, these missing values are imputed with the median of the non-missing values of variable pdays.The missing value cut off is set to 97% since we have 96% missing.

• Before regression, an impute node has been used in SAS enterprise miner to replace missing values. The default input method is selected as median and hence median of pdays i.e. ‘6’ will be imputed in place of all missing values. By default, the missing cut

• Further we will be creating a new column with imputed values and use it as an input in the data modelling. For this we have to do personalise the settings for indicator variable with Type set as Unique and Role set to input. In addition, we will get a variable which indicates whether a value is imputed or not: ‘1’ for imputed and ‘0’ for not imputed, and this will also be an input variable. Both of those become inputs to be tested whether or not they affect the outcome variable.

• Once we run the node, the values get imputed and we can see two additional columns in the data as shown below:
For example, we can see that in train data 21857 values are replaced and the same happens in validation data which replaces 17816 values.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.53.22%20AM.png)

For example, we can see that in train data 21857 values are replaced and the same happens in validation data which replaces 17816 values.


![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.53.31%20AM.png)

In the above figure we can see that there are totally 3 columns: replaced column, imputed column and imputation indicator column. The missing values are replaced by value ‘6’. Once the values are imputed the original pdays column role becomes rejected.

b. Transformation of variables

After imputing the variables, we should not consider transforming some of our variables which does not look normal. Transforming the data before modelling always improves the response of model by stabilizing its variance, removing non-linearity and handle the data which is not normal. We can opt to transform one or more variables in our dataset.

Here we are selecting two variables for transformation: campaign and previous since these interval variables does not seem to be normal when checked for skew and kurtosis.

The common log transformation method is used to control the skewness of the variable. As a result, 2 new transformed variable columns are added and we can see that the common log transformation tries to normalise both the variables.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.53.41%20AM.png)

Now our data is ready for building a regression model. We drag a regression model into the workspace and connect the impute node to it and directly run the model.

• The default settings of regression node build a model where all variables are used to build the model and the results are as shown below. The significance level of accepting any model as significant is considered as 0.05.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.53.52%20AM.png)

From the above screenshot we can say that our regression model is statistically significant (<0.0001) and it is capable of explaining the target variable ‘y’.

• Since we have used the default setting of regression the algorithm uses all variables to build the model and we can see from the results that not all variables are significant in explaining the target variable ‘y’.

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.54.07%20AM.png)

• Here comes the use of Stepwise model selection where the algorithm automatically selects the variables based on their Chisq value stepwise and runs the model. The results of this model are as shown below:

![alt text](https://github.com/guanliu321/Predictive-Modeling-Using-SAS-Enterprise-Miner/blob/main/Figure/Screen%20Shot%202020-12-18%20at%204.54.18%20AM.png)

   The process uses 21 steps to select the best variables for the model with number of variables reduced to 11, capable of efficiently predicting the target variable ‘y’. The misclassification rate was found to be 0.0992 for both train and validation data.
   
3. RANDOM FOREST

Random forest is classifier algorithm which uses a number of decision tress to build a best predict data model. The algorithm selects the variables depending on the variable importance calculated and several number of weak decision trees are created. As the number of tress increase the model becomes gradually efficient with decreasing error rate. Some of the interesting observations in the random forest model as are explained below:

The table in the left gives the variable importance indicating euribor3m, nr.employed, month as the variable with most importance and loan with least. Depending on this calculation the algorithm tries to build number of weak decision tree models. Also, the second graph indicates that there were 100 weak decision trees built and as number of trees increased the Misclassification error rate decreased trying to make the model to behave as the best fit. Until 20 trees the misclassification rate gets decreased and further the trend becomes stagnant and finally at 100th decision tree the misclassification rate is 0.0994 and 0.0998 for train and validation data respectively, which is a good measure comparatively.

4. SUPPORT VECTOR MACHINE (SVM)

A support vector machine is a binary classifier algorithm where it separates the observations into two classes. There is a margin drawn in between the two observations, the more we can separate these two models by increasing the margin, we will have a better and more accurate model when applied to an unknown data. Since all data cannot be separated with a 1-D margin we use kernel functions where a higher-dimensional margin is placed between the observations. A selected kernel and its parameters accounts in how well a classification model is built.
Here, in our SVM model we tried different kernel functions and have selected linear kernel with 2 polynomial degree as the best option to deal with.
  
