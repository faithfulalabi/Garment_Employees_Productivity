# Garment_Employees_Productivity: Project Overview

* Created a tool that predicts the productivity performance (RMSE ~ 0.075) of the working teams at a garment manufacturing factory. The productivity performs ranges from (0-1).
* Dataset is from the UCI Machine Learning Repository [here](https://archive.ics.uci.edu/ml/datasets/Productivity+Prediction+of+Garment+Employees)
* Did some Exploratory Data Analysis (EDA) to answer certain questions I asked myself from the prospective of if I was mananging both departments, and to better understand the dataset.
* Engineered features to correct skewness, deal with categorical and missing data.
* Used a XGBoost Regressor model, performed some paramter adjustments and optimized it using GridsearchCV for the best model.

* __Motivation__: 

My inspiration for taking on this project comes from me wanting to work on more business related projects and answer questions from a management and director prospective.

## Dataset Feature Explaination
[Feature Explaination](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/Garment_Project_Feature_Description.txt)


## Exploring the Data 
 ![alt text](https://github.com/faithfulalabi/African_Crisis/blob/main/EDA_GIF.gif?raw=true)
 
### Number of Entries per Department
Observation of this plot, we can see that most of the enteries of the data are in the Sewing department
![alt text](https://github.com/faithfulalabi/Garment_Employees_Productivity/blob/main/eda_assets/Entry_per_Department.png?raw=true)
