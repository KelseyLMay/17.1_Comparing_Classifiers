# 17.1_Comparing_Classifiers
This repo contains the Jupyter notebooks, data, and graphs that explore the effect of different marketing campaign features on client conversion across 17 campaigns from May of 2008 to November of 2010.

## Business Objective ##
The Business Objective is to analyze the data from 17 marketing campaigns to identify key factors that influence client decisions, and create a predictive model that accurately predicts whether a prospective client will subscribe to a term deposit. The bank will be able to use this model and information to create effective and efficient campaign strategies that increase subscriptions to term deposits.

## Understanding the Data ##
Initial analysis revealed that no rows were missing data, but the rows with "unknown" for any of the following columns were removed: "job", "marital", "education", "default", "housing", and "loan". Next I categorized several of the fields for easier analysis: "month" was grouped into winter/spring/summer/fall seasons, and "age" and "pdays" were broken into several ranges based on the min, max, and unique values for the columns. I also dropped the "duration" column because the field description indicated it should be discarded if the intent is to have a realistic predictive model.

Next I created bar plots to better understand the relationships and trends in the data. I normalized the data by group within each column to better visualize the likelihood of a particular subgroup subscribing to a term deposit independent of how frequent that group appeared in the larger dataset. For example, my graph of the age range data shows the percent of yes/no responses within each age range, so the yes/no responses total 100% within each age range. I dropped the following columns based on my visual analysis indicating the result didn't vary significantly across the groups: marital status, education level, whether or not the client has a personal loan, the day of the week, or the number of days that passed after the client was last contacted from a previous campaign.

## Process ##
The categorical data was encoded and the numerical data was standardized, the data was split into training and test data, and models were built using GridSearchCV with various hyperparameters and 5-fold cross validation. The results were as follows:

| Model                    | Train Time | Train Accuracy | Test Accuracy |
|--------------------------|-----------|----------------|---------------|
| Logistic Regression       | 2.153765  | 0.889135       | 0.885864      |
| KNN                       | 3.916191  | 0.901189       | 0.877337      |
| Decision Tree Classifier  | 0.493299  | 0.891882       | 0.884552      |
| SVC                       | 0.630644  | 0.886327       | 0.914239      |

NOTE: I used the smaller subset of the data for the SVC model due it its high computational requirements.

Next I used PolynomialFeatures and LogisticRegression with an l1 penalty to explore which features were most important in the outcome. Those results indicated that several of the fields I had not previously explored in detail were the most influential, so categorized the data for those fields (the number of contacts during the current campaign, number of previous contacts, employment variation rate, consumer price index, consumer confidence index, the Euribor 3 month rate, and number of employees), created the same normalized graphs, and repeated the L1 logistic regression. 

## Results ##
The second L1 logistic regression model was 87.9% accurate, and indicated that clients are more likely to accept the offer if the Euribor 3 month rate is between 0-0.999, the employment variation rate is -1 through -3, or within an age range of 50-69. Conversely, clients are more likely to reject the offer if the number of contacts performed during this campaign and for this client is 10-29 (indicating that continuing to contact them beyond 10 times is unlikely to lead to conversion), the consumer price index is greater than 92, and, to a lesser extent, if the client falls in an age rane of 30-49.

Although none of my models achieved my target 90% accuracy, they all hovered around 88-89%. The SVC model had the highest accuracy but was done on a subset of the data because of its high computational requirements. The Decision Tree Classifier was the fastest and maintained accuracy so that model would be the most helpful out of the ones here. It is possible that additional analysis and exploring additional hyperparameter values would further improve results, although cross validation was used to optimize the current hyperparameters.

## Conclusion ##
My analysis indicates that newer cars (younger than 2010), cars with diesel fuel, or lower mileage (less than 100k miles) cars have the highest prices. In contrast, older cars (older than 2010), cars with higher mileage (more than 150k miles), or cars in poor condition have the lowest prices. I created a model that can be used to roughly predict the price of used cars based on certain criteria. However, the size of the mean squared error indicates that the data needs more cleaning or more data should be analyzed to create a model that can make more accurate predictions.

NOTE: All of the graphs mentioned above can be found in the [graphs directory](https://github.com/KelseyLMay/17.1_Comparing_Classifiers/blob/main/graphs)
