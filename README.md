# Data Science Salary Estimator: Project Overview 
* I was inspired to create this project after watching a YouTube series by Ken Jee about estimating the salaries of data scientists. His work helped me create a roadmap for completing the project.
* I created a tool that estimates data science job salaries. This tool is designed to help data scientists negotiate their income when they get a job.
* Analyzed the text of each job description to quantify the value companies put on certain skills such as Python, Excel, AWS, and Spark. 
* Used GridsearchCV to optimize Linear, Lasso, and Random Forest regressors to reach the best model.
* Built a client facing API using Flask 

## Code and Resources Used 
**Python Version:** 3.9.2  
**Framework:** Anaconda (Jupyter Notebook and Spyder)
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, flask, json, pickle  
**For Web Framework Requirements:**  ```pip install -r requirements.txt```   
**Flask Productionization:** https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

## Ken Jee YouTube Project Walk-Through
https://www.youtube.com/playlist?list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t

## Data
I've worked with Kaggle dataset https://www.kaggle.com/datasets/vincenttu/glassdoor-joblisting 
Dataset includes following columns:
* 'company': A string with or without a company rating
* 'job title': A string of the job title
* 'headquarters': A string of the company's headquarters location
* 'salary estimate': A string of the provided estimated salary or salary range
* 'job type': A string for the job type (full-time, part-time, internship, etc)
* 'size': A string estimating the number of employees at a job
* 'founded': An int specifying the year of company founding
* 'type': A string for company type (public, private, etc)
* 'industry': A string for their industry
* 'sector': A string for the sector
* 'revenue': A string for the revenue the company generated
* 'job description' : A string description of the job and/or the company

## Data Cleaning
Dataset was uncleaned and extremely messy, so I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:

*  Removed rows without salary estimate 
*  Removed some faulty rows from job type 
*	Parsed rating out of company text 
*  Removed unnecesary strings from salary estimate to make it more readable
*	Parsed numeric data out of salary 
*	Made a column for hourly wages 
*  Added columns for minimum, maximum and average salary estimates
*	Made a new column for company state 
*	Transformed founded date into age of company 
*	Made new columns for some skills that might be listed in the job description:
    * Python  
    * Spark 
    * R  
    * AWS  
    * Excel  
*  Parsed company size into numerical values
*  Created a column for average revenue
*  Columns for simplified title and position
*  Created a new csv file for cleaned data

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the tables. 

![image](https://user-images.githubusercontent.com/74883103/210280986-d688d940-bd27-4f69-9f61-07754bb8c358.png)
![image](https://user-images.githubusercontent.com/74883103/210281031-ed453eab-2260-4ce6-8ae4-d999eee5ba5a.png)
![image](https://user-images.githubusercontent.com/74883103/210281067-5e678083-db2c-4f16-81ec-394fa3b26c27.png)
![image](https://user-images.githubusercontent.com/74883103/210281093-c328c67b-64f4-4628-b1f6-ccee8673ff0e.png)

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.   

I tried three different models:
*	**Multiple Linear Regression** – Baseline for the model
*	**Lasso Regression** – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
*	**Random Forest** – Again, with the sparsity associated with the data, I thought that this would be a good fit. 

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. 
*	**Random Forest** : MAE = 7.06
*	**Linear Regression**: MAE = 13.40
*	**Ridge Regression**: MAE = 9.81

## Productionization 
In this step, I built a flask API endpoint that was hosted on a local webserver. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary. 


