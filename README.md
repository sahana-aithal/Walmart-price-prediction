# Walmart Predictions

Introduction:
A major problem faced in modeling retail data is the lack of historical data availability and a need to make decisions based on limited history. It is very well known that the sales of a retail store are affected by holidays, markdowns and other major select events. The project emphasizes on performing data analysis on the historical data of 45 different retail stores across different locations and finding out the impact of different features on the retail data.

Problem questions:
Which store has the most unemployment numbers? How much has holidays impacted the sales of the store? What is the department having the highest/lowest sale? What is the correlation between the ‘features’ and sales of the retail store? What are the yearly sales of the retail stores?

Using the dataset we have tried to answer the following questions:
Predicting the weekly sales based using Regression models for different weeks depending on variables such as Temperature , Fuel Price, Markdown, whether the week was a Holiday week and the week number using data from multiple years. 
Classifying Sales of a Store based on the factors affecting, using which Stores can be ready for high sales or can take effective cost saving measures if the sales in the forthcoming weeks are going to be low.
Depending on Department Weekly sales we have tested different models and chosen the best model, so that the Company can manage inventory to be supplied to stores in different corners of the country.

Data Collection:
Stores dataset: This contains anonymous information of 45 stores, indicating the type and size of them.
Label(s): Store, type, size
 Size: 45 rows
Features dataset: The dataset contains additional data related to the store, department, and regional activity for the given dates.
Label(s): 
Store - the store number
Date - the week
Temperature - average temperature in the region
Fuel_Price - cost of fuel in the region
MarkDown1-5 - anonymized data related to promotional markdowns. MarkDown data is only available after Nov 2011, and is not available for all stores all the time. Any missing value is marked with an NA
CPI - the consumer price index
Unemployment - the unemployment rate
IsHoliday - whether the week is a special holiday week

      Size: 8190 rows

       3. Sales dataset: The dataset contains the historical sales data from 2010-02-05 to             2012-11-01 for the 45 stores. 

    Label(s):
Store - the store number
Dept - the department number
Date - the week
Weekly_Sales -  sales for the given department in the given store
IsHoliday - whether the week is a special holiday week

    Size: 421,570 rows


Exploratory Data Analysis:
![image](https://user-images.githubusercontent.com/43316158/158931267-ca2c8a9e-1751-4af2-bfa7-003d88119418.png)


Scatter plot of ‘weekly_sales’ vs ‘store’ shows some values below 0 and values ranging between 0 and 700000. 

![image](https://user-images.githubusercontent.com/43316158/158931300-cba157e3-d5ef-4d69-82d7-3cc37ae8b9cd.png)

The number of True and False in IsHoliday

![image](https://user-images.githubusercontent.com/43316158/158931339-414d131f-0a22-4b27-adef-7fae21528b34.png)


The distribution of size in the store table.

Correlation matrix of the features table shows high correlation between ‘markdown1’ and  ‘markdown4’. 

![image](https://user-images.githubusercontent.com/43316158/158931390-c931d6d6-2b6c-42dc-87bc-05412d8a52a8.png)


Correlation matrix of the sales table shows no significant correlation between any features. 
![image](https://user-images.githubusercontent.com/43316158/158931417-5f8e1f12-4806-479c-a641-60c0a718525e.png)


Correlation matrix of stores table shows no significant correlation between any features.

![image](https://user-images.githubusercontent.com/43316158/158931469-38cab97c-e7d2-465a-b65b-b2b7e29dbbed.png)


Created a line graph to observe the weekly_sales trend over the years 2010,2011 and 2012

![image](https://user-images.githubusercontent.com/43316158/158931525-e10c204d-d472-456e-83a2-23b1fef759ca.png)


Data Preprocessing:

Presence of null values is checked in each of the dataset.


![image](https://user-images.githubusercontent.com/43316158/158931573-b944a88e-a70f-42cd-baa9-a67788f9cca8.png)



It is found that only the features table has null values in all ‘Markdown’ columns, CPI and Unemployment. We replace the NULL values with meaningful data as below: 
Markdown: Null values as missing Markdown values can potentially mean no markdown. 
CPI: Mean value of CPI has been used to replace NULL values
Unemployment: Mean value of Unemployment has been used to replace NULL values.

Descriptive Data Preparation:

Merging features and stores tables on ‘Store’

![image](https://user-images.githubusercontent.com/43316158/158931654-bd052a52-530a-4a5a-bbe6-ad6bfb5e4d9d.png)


Merging features and sales tables on ‘Store’, ‘Date’, and ‘IsHoliday’:

![image](https://user-images.githubusercontent.com/43316158/158931707-41ae39f3-783a-4903-84bf-faec92deb33b.png)


Correlation matrix of feature_sales:

![image](https://user-images.githubusercontent.com/43316158/158931731-a7799a20-c796-4933-b027-d906cf89f1e5.png)


From the above correlation matrix, we observe the following:
‘year’ and ‘fuel_price’ have a high correlation of 78%, therefore we decided to drop the column ‘fuel_price’.
‘markdown1’ and ‘markdown4’ have a high correlation of 84%, therefore we decided to drop the column ‘markdown4’.



Modeling techniques:

We have performed multiple models for each problem question addressed above. They are as follows:

Question 1: 
Standardization using MinMaxScalar() is performed on the ‘feature_sales’ data to normalize all the numeric values. 

![image](https://user-images.githubusercontent.com/43316158/158931819-5eb38b8e-4288-41a5-9692-9b8d25f45b2f.png)


Linear Regression:

We observe that linear regression is performing with 20% accuracy. 

Random Forest Regressor:
Using plots on Random Forest Regressor parameters we were able to find the best hyperparameters for which such a high score was produced by the model.

![image](https://user-images.githubusercontent.com/43316158/158931867-54ee5940-d26a-44a7-8abf-343d2bf2569a.png)

![image](https://user-images.githubusercontent.com/43316158/158931888-9ffc1be4-167e-40d5-aabc-c281027e0248.png)

From this we found that the optimal number of estimators is 50, and max depth is 25 which could effectively predict the sales value quite optimally.

![image](https://user-images.githubusercontent.com/43316158/158931930-fa3e1a8b-1910-4385-9a97-9a3e2c19977c.png)


Question 2:

Standardization using StandardScalar() has been used in the following question to normalize our data. 
We create a new DataFrame called ‘new_sales’ which groups the ‘feature_sales’ on months, year and store number. 


We then create a new column with 3 categories: ‘low’, ‘medium’, and ‘high’ for sales.


We have performed the following 3 models:

Decision Tree:

![image](https://user-images.githubusercontent.com/43316158/158931959-64755f09-c5c4-44de-bbfd-200495ac8d38.png)


Random Forest:

![image](https://user-images.githubusercontent.com/43316158/158932008-eba0662e-7675-42b6-ba54-b83ade099b27.png)

XGBoost: 

![image](https://user-images.githubusercontent.com/43316158/158932051-33afee36-fa62-48ff-9bc3-e38e349d6941.png)


 Question 3:

Standardization using MinMaxScaler() is performed on the ‘feature_sales’ data to normalize all the numeric values. 
We create a new DataFrame called sales where we group by feature_sales on ‘Department’ and ‘Date’
We have removed the Stores column and, grouped by Department to get weekly sales of each department.

And drop all the markdown columns:


The following 3 models have been performed:
Decision tree regressor: 

![image](https://user-images.githubusercontent.com/43316158/158932084-3aa3cb19-f95c-4b4d-bf8a-6f554fe03c5f.png)

Random Forest Regressor:

![image](https://user-images.githubusercontent.com/43316158/158932139-a69ed0ce-9022-4751-991b-94806484d2d6.png)


Results:

We have found the following results for the 3 questions:
Random Forest Regressor performs with the accuracy of 93%
XGBoost regressor performs with the accuracy of 80%
Random forest regressor performs with the accuracy of 95%

