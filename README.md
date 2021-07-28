# Garment_Employees_Productivity: Project Overview

* Created a tool that predicts the productivity performance of the working teams at a garment manufacturing factory (RMSE ~ 0.075). The productivity performs ranges from (0-1).
* Dataset is from the UCI Machine Learning Repository [here](https://archive.ics.uci.edu/ml/datasets/Productivity+Prediction+of+Garment+Employees)
* Did some Exploratory Data Analysis (EDA) to answer certain questions I asked myself from the prospective of if I was mananging all the teams in both departments, and to better understand the dataset.
* Engineered features to correct skewness, deal with categorical and missing data.
* Used a XGBoost Regressor model, performed some paramter adjustments and optimized it using GridsearchCV for the best model.

## __Motivation__: 

My inspiration for taking on this project comes from me wanting to work on more business related projects that answer questions from a management and director prospectivema and to also predict performance of employees based off certain features.

## Dataset Feature Explaination
[Feature Explaination](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/Garment_Project_Feature_Description.txt)

## Exploring the Data 
 ![alt text](https://github.com/faithfulalabi/African_Crisis/blob/main/EDA_GIF.gif?raw=true)
 
### Number of Entries per Department
From the observation of this plot, we can see that most of the enteries of the data are in the Sewing department.
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Entry_per_Department.png?raw=true)

### Number of Entries per Quarter 
The plot below shows the amount of enteries per quarter.
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Entry_per_Quarter.png?raw=true)

### Distribution of Targeted Productivity
This plot shows the distributed targeted productivity across the dataset.
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Targeted_Productivity_Distribution.png?raw=true)

### Distribution of Actual Productivity
This plot shows the distributed actual productivity across the dataset.
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Actual_Productivity_Distribution.png?raw=true)

### Average Trend of Incentives Paid Out on a Monthly Basis
This observation wanted to answer the average trend for incentives paid out on a monthly basis. We can see there was a huge spike after February. 
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Average_Incentives_Paid_out_Monthly.png?raw=true)

### Average Number of Unfinished Items per Team
The question i asked myself to generate this plot was, which teams had the highest number of unfinished items. We can observe from the plot that they were teams 10, 3, and 1. 
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Average_Number_of_Unfinished_Items_per_Team.png?raw=true)

### Average Monthly Trend of Work In Progress
I wanted to know since there was a huge spike in the average trend of incentives paid out after February, what was the monthly average trend in the amount of work in progress. We can observe that the trends are inversely proportional to each other
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Average_Monthly_Work_In_Progress.png?raw=true)

### Average Overtime per Team
What teams had the highest amount of average overtime? They were teams 4,3,and 5.    
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Average_Overtime_per_Team.png?raw=true)

### Total Incentives Payout by Team
From the plot we can observe that team 9 had the highest amount of incentives payout than any other teams.    
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Total_Incentive_Payout_by_Team.png?raw=true)

### Average Monthly Overtime Trend
The overall trend for the monthly overtime trended down and mostly flat for the 3 month of data we have.     
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Average_Overtime_Trend.png?raw=true)

### Total Idle people per Team
The plot below shows the total number of idle people per team. We can see that teams 7 & 8 has the highest total amount of idle people. 
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Sum_of_Idle_Men_per_Team.png?raw=true)

## Data Cleaning
After getting the dataset, I cleaned it up, dealt with missing data so our data can be acceptable for our model. I made the following changes:
* Filled all missing Work In Progress(WIP) column data with 0 because all the missing data were in the finishing department, meaning they were waiting on work from the sewing department.
* Converted the date column to datetime object.
* Converted the overtime column from minutes to hours.
* Combined the two seperate finishing departments into 1 finishing department.
* Transformed the actual productivity column to be less negatively skewed.



## Model Building

First I transformed the categorical strings into dummy variables. I then split the data into train and test sets with a test size of 20%.

I scaled the data and tested a Lasso, Ridge, ElasticNet, XGBRegressor, ExtraTreesRegressor, and AdaBoostRegressor models(see training scores plot below) using R^2 as my scoring metric. Ultimately I chose the XGBRegressor model because it had the highest R^2 score(see training scores plot below). Meaning 41.3% of the variation in y can be explained by the changes in X.
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/models.png?raw=true)

I tested my model on the training and test dataset without any adjustments to the hypeparameters and a scoring metric of R^2(see Actual vs Predicted plot below). I obtained:

Training score: 0.979257990983347
Testing score: 0.40931711159708206

From the scores above and the plot below, we can observe that our model is overfitting and not adapting well to new data. 
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/Initial_Actual_vs_Predicted.png?raw=true)

After tuning these parameters: learning_rate, max_depth, min_child_weight, subsample, colsample_bytree, n_estimators, objective, random_state. I was able to obtain a (see plot below): 

Training score: 0.7188269109746894
Testing score: 0.5417706699183125

From the plot below we can see that our model is no longer overfitting
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/Initial_Actual_vs_Predicted.png?raw=true)

I chose the RMSE, MAE, and R^2 because they're easy to interpret.


## Model Performance

* XGBRegressor : 
  test_RMSE: 0.07511378123742236
  test_MAE: 0.04898648752560755
  R^2:0.5417706699183125
