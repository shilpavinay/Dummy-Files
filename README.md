**Bike Sharing Case Study**

**Business Goal:** 
You are required to model the demand for shared bikes with the available independent variables. It will be used by the management to understand how exactly the demands vary with different features. They can accordingly manipulate the business strategy to meet the demand levels and meet the customer's expectations. Further, the model will be a good way for management to understand the demand dynamics of a new market.
Problem Statement: A US bike-sharing provider Boom Bikes has recently suffered considerable dips in their revenues. They have contracted a consulting company to understand the factors on which the demand for these shared bikes depends. Specifically, they want to understand the factors affecting the demand for these shared bikes in the American market. The company wants to know: Which variables are significant in predicting the demand for shared bikes.
How well those variables describe the bike demands.
You are required to model the demand for shared bikes with the available independent variables. It will be used by the management to understand how exactly the demands vary with different features.
They can accordingly manipulate the business strategy to meet the demand levels and meet the customer's expectations. Further, the model will be a good way for management to understand the demand dynamics of a new market.

**Steps for Model Building **
1.Reading and Understanding Data 
2.Visualising the Data 
3.Data Preparation 
4.Splitting the Data into Training and Testing Sets 
5.Feature Scaling 
6.Building the Model 
7.Residual Analysis of the train data 
8.Making predictions using final model 
9.Model Evaluation
**Steps performed: **
**Step 1: Reading and Understanding the Data**
Data Quality Check - Checking for NULL/MISSING values & Finding Duplicate values
Inference : 1. No missing/NULL values found - Data looks good for our analysis. Please refer analysis below for details.
Inference : 2. Duplicate values are not present - Data looks good for our analysis. Please refer analysis below for details.
Data Cleaning - This will help to identify any Unknown/Unwanted values present in the dataset.
Inferences: There seems to be no Unknown/Unwanted values in the entire dataset. Please refer to analysis below
•	Removing redundant & unwanted columns
o	Based on the high-level look at the data and the data dictionary, the following variables can't be considered from further analysis:
o	instant: Its only an index value, we have a default index for the same purpose.
o	dteday : This has the date, Since we already have separate columns for 'year' & 'month’, hence, we can carry out our analysis without this column.
•	casual & registered: Both these columns contain the count of bike booked by different categories of customers. Since our objective is to find the total count of bikes and not by specific category, we will ignore these two columns.

**Step 2: Visualising the Data - Numerical & Categorical Variables**
•	By visualising the numeric variables, there are some independent variables like atemp , temp etc. that show a positive correlation with the target variable cnt. We can conclude that a linear model can be considered in this case.
•	The variable season’s category 3 (Fall) has the highest median, which shows that the demand was high during this season. It is least for 1 (spring). So, the count of bike sharing is least for spring and high in fall.              
•	During the year 2019, number of bikes shared are higher as there is a high count of users as compared to the year 2018              
•	The bike demand is almost constant throughout the week.              
•	The count of total users is in between 4000 to 6000 (~5500) during clear weather.              
•	The count is highest in the month of September.              
•	The count of users is less during the holidays.              
•	The count has zero values for weather situation with category 4 ('Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog')
Step 3: Data Preparation Creating Dummy Variables: 
The variables mnth weekday season weathersit have various levels, for ex, weathersit has 3 levels, variable mnth has 12 levels. Created DUMMY variables for these 4 categorical variables namely - mnth, weekday, season & weathersit.
Step 4: Splitting the Data into Training and Testing Sets 
The first basic step for regression is performing a train-test split. The 70-30 ration is used to split the data.
Step 5: Rescaling the Features 
The scaling won't impact the linear model in case of simple linear regression, but while performing multiple linear regression it might impact the model. As we can see that the value of the feature cnt has much higher values as compared to the other features like temp, atemp etc. So it is extremely important to rescale the variables so that they have a comparable scale. If we don't have comparable scales, then some of the coefficients as obtained by fitting the regression model might be very large or very small as compared to the other coefficients. This might become very annoying at the time of model evaluation. So it is advised to use standardization or normalization so that the units of the coefficients obtained are all on the same scale. 
There are two common ways of rescaling: Min-Max scaling and Standardisation (mean-0, sigma-1). I have used MinMax scaling.
From the map, atemp and temp seems to be correlated to the target variable cnt. Since, not much can be stated about the other independent variables, hence we will build a model using all the columns.
Step 6: Building a linear model 
Fit a regression line through the training data using statsmodels. In statsmodels, you need to explicitly fit a constant using sm.add_constant(X) because if we don't perform this step, statsmodels fits a regression line passing through the origin, by default. APPROACH USED : We will use a mixed approach to build the model. Here we are using RFE approach for feature selection and then we will use the statsmodel approach for building the model.
After building and observing the liner model, I see that the p-value for all the variables is < 0.05 . Hence, I will keep all the columns and proceed with the model.
Checking VIF for multicollinearity: Variance Inflation Factor or VIF, gives a basic quantitative idea about how much the feature variables are correlated with each other. It is an extremely important. 
Parameter to test our linear model. VIF less than 5 variables needs to be dropped.
Preparing the final model: All the columns has VIF value less than 5 and temp slight has a little more than 5 which can be ignored. Let us finalise lm_2 as the final model to proceed with the future analysis and model prediction.
Step 7: Residual Analysis 
Residual analysis of the train data Let us do residual analysis to understand if the error terms are also normally distributed as this is one of the major assumptions of linear regression. I have plotted the histogram for the error terms and to conduct analysis.
The error terms are centred around 0 and follows a normal distribution, this is as per one of the major assumptions of linear regression.
Cross-verifying the above conclusion using a qq-plot as well: Most of the data points lie on the straight line , which indicates that the error terms are normally distributed.
Step 8: Making Predictions Using the Final Model 
We have fitted the model and checked the normality of error terms using residual analysis, let us make predictions using the final model.
R-squared Caclulations: R-squared is a goodness-of-fit measure for linear regression models. This statistic indicates the percentage of the variance in the dependent variable that the independent variables explain collectively. R-squared measures the strength of the relationship between your model and the dependent variable on a convenient 0 – 100% scale.
R_squared on the test set is 0.804 R-squared on the trained set 0.840. Looks like these numbers are reasonable and nearly equal. This indicates that, the data model analysed and predicted using train data set is almost able to apply those inferences in test data set.
Step 9: Model Evaluation –
Graph for actual versus predicted values for evaluation. We can confidently conclude that the final model fit has descent prediction and can be used for further inferences.
Best fitted line - Analyse variable names and the coefficient values for the final equation
Final Conclusions: 
The equation for best fitted line is : Cnt = 0.1737 + 0.4728 X temp + 0.2343 X yr + 0.0796 X season_Winter + 0.0753 X mnth_Sep + 0.0584 X weeday_Saturday + 0.0465 X workingday + 0.0433 X season_Summer - 0.0389 X mnth_Jan - 0.0482 X mnth_Jul - 0.0561 X holiday - 0.0597 X season_Spring - 0.0826 X weathersit_Mist & Cloudy - 0.156 X windspeed - 0.291 X weathersit_Light Snow & Rain
•	All the positive coefficients like temp, season_Summer indicate that an increase in these values will lead to an increase in the value of Cnt and all the negative coefficients indicate that an increase in these values will lead to a decrease in the value of cnt.
•	By looking at the R-Sqaured and adjusted R-Sqaured value of both train and test dataset we could conclude that the above variables can well explain and predict more than 83% of bike demand.
•	The factors affecting the bike demand is explained by coefficients of the variables.
•	In the final model top three features contributing significantly towards explaining the demand are: Temperature - 0.472823 - Temp is the most significant with the largest coefficient and is followed by weathersit : Light Snow, Light Rain + Mist & Cloudy (-0.291727) and year (0.234361).
•	From the above final module features, it indicates that, the variables temperature , season/ weather situation and month are significant in predicting the demand for shared bikes.
•	The rentals reduce during holidays.
•	Bike rentals is more for the month of September
Overall, it indicates that the bike rentals are majorly affected by temperature,season and month.
