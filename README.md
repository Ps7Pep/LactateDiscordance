# LactateDiscordance

## LactateDiscordanceETL contains the ETL functions to obtain the cohort dataset

Note that this project uses data from 3 different sources, but only two of them are open access (MIMIC and eICU). This script contains the code to extract, transform and load all the data from all 3 sources, so people interested can check it. However, only the ETL parts related with MIMIC and eICU could be reproduced in case people interested have access to those databases.

This repo contains the file *alldbs.csv*, which is the output of the ETL script. People interested may reproduce the analysis using this file as input in the rest of notebooks.

## The rest of notebooks contain the different analyses applied to the data obtained by the ETL

The analyses notebooks are subdivided in 4 steps. And should be used in this order.

### 1st analysis for each database. 

These 1st analysis for each database are done in 3 files: *LactateFinal-HJ23.ipynb*, *LactateFinal-MIMIC.ipynb* and *LactateFinal-eICU.ipynd*. 

In each file we work with one database separately, but all of 3 files start by reading the *alldbs.csv* file. The 3 scripts create a table 1 for the whole study and a table 1 for each database, and for their database detect and imput the missing values, standarize the data, study the correlation between variables, and build 3 models (Logistig Regression model, Random Forest and Partial Least Squares). For each model we obtain the most important features by feature forward selection and the relationship of each feature with High or Normal lactate. 

We store the dataset used for running the models in the **GeneratedFiles/Databases** directory. Each dataset is stored after the scpecific preprocess of the data for that model is done. We also store the tableone png and csv for the whole study and for each database in **Tables** directory. The coefficients of the relationship between the important features for each pair of model/database and lactate are stored in **GeneratedFiles/ImportantVariables** as coef_$(model)_$(db).csv. 

### Understanding important features for each model among the 3 databases.

In the *LactateFinal-ImportanceFigures.ipynb* we read the files of **GeneratedFiles/ImportantVariables** that were generated in the 1st analysis for each database. This files contain the coefficients of the relationship between the important features and lactate for each pair of model/database. We group the coefficients for each model and select those features for each model that appear at least in 2 of the 3 databases. The important features for each model among 3 databases are stored in **GeneratedFiles/ImportantVariables** as $(model)_important.csv.

The graphs generated in the file are stored in **Figures** as importance_$(model).png.

### 2nd analysis for each database. 

The 2nd analysis for each databases is done in the files: *LactateFinal-HJ23-Part2.ipynb*, *LactateFinal-MIMIC-Part2.ipynb* and *LactateFinal-eICU-Part2.ipynd*. 

In each file (one for each database), we read the databases generated in **GeneratedFiles/Databases**, obviously we only read those related to the database in the database script. Each script runs the 3 models for each database but only with the important features selected in last step and stored in **GeneratedFiles/ImportantVariables** as $(model)_important.csv. 

For each model we obtain again the coefficients of the relationship between the important features and lactate for each pair of model/database, but now, each database has the same important features for the same model. So the same features in MIMIC, in eICU and HJ23 are used for Logistic Regression, as an example. 
This coefficients are stored in **GeneratedFiles/ImportantVariables** as coef_$(model)_$(db)_2.csv.

### Understanding important features for lactate discordance. 


This is done by the file *LactateFinal-ImportanceFigures-Part2.ipynb*.
The files in **GeneratedFiles/ImportantVariables** as coef_$(model)_$(db)_2.csv are read and we study the coefficients of the relationship between important variables and lactate grouped by models, so we have one graph for LR, other for RF and other for PLS. 

We can understand wichh variables are important for High Lactate or Low Lactate with these graphs, and see if a variable seems to have the same coefficient among the 3 databases in one model. 
The graphs generated in the file are stored in **Figures** as importance_$(model)_2.png.


<sup><sub>Disclaimer: Note that slightly differences between the results presented in the manuscript and results obtained when re-running the code may exist  due to packages versions 

