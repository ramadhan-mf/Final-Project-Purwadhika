# Final Project Purwadhika
This final project is one of the requirements for graduating from Job Connector Data Science and Machine Learning Purwadhika Start-up and Coding School

<p align="center"  color="rgb(0, 90, 71)">
<h1>About the Final Project</h1>
</p>
<p align='justify' style="font-weight: bold;">
- The purpose of this project is to be able to predict weekly sales targets based on previously stored weekly sales data.<br>
- The dataset used in this project is data sourced from Kaggle.com which contains sales data for 45 Walmart stores located in various regions.<br>
- The reason I choose this dataset is, because the environment that Walmart has is very similar to the company I work for today. Has many branches and also has several sub divisions / departments in sales.<br>
- So my hope after implementing the project is that I can re-implement the model using the data that my company has.<br>
</p>

### 1. Data Extraction
At this stage the process that I did is uploading csv data that can be obtained from kaggle.com. There are 4 data which are as follows:<br>
1.stores.csv: a file containing anonymous information on the 45 Walmart stores and their types and sizes.<br>
2.train.csv: File that informs training data from 2010-02-05 to 2012-11-01. The columns include: Store, Dept, Date, Weekly Sales, IsHoliday.<br>
3. test.csv: File in the same format as Train.csv, but without the Weekly_Sales column, which must be filled in by the results of the prediction models that have been made.<br>
4. features.csv: Files that contain additional information related to stores, departments, other regional activities based on the input time.<br>

### 2. Data Preprocessing
At this stage, 3 steps are taken in preparing the data before it is used in the model:
1. Merging data in the file feature.csv, train.csv and stores.csv.
2. Detect and fill null data on the previous merging data.
3. Detect if there is duplicate data.

### 3. Exploratory Data Analysis (EDA)
At this stage, a visual approach (heatplot and scatter plot) is carried out to see if there is a close relationship between each feature / column in the dataset to the Weekly_Sales feature / column.

<p align="center"> <img src="https://user-images.githubusercontent.com/69567029/99923120-d47fee00-2d66-11eb-9bf5-7857b3115047.PNG" alt="" width="700" height="500"> </p><br>
<h5> Correlation Weight </h5>
<p align="left"> <img src="https://user-images.githubusercontent.com/69567029/99923331-cbdbe780-2d67-11eb-8f4e-879f2630a2ef.PNG" alt="" width="400" height="300"> </p>

### 4. Feature Engineering
At this stage, data features are selected which later will be used as data sources for the modeling process. Because the model used is ARIMA which can only process data in the form of univariate time series, the Weekly_Sales feature is choosen with Date as the index. But before using the Weekly_Sales feature, there are steps that are taken, including:<br>
1. Group Weekly_Sales data into the same time, where the previous Weekly_Sales data is still divided by department and store.<br>
2. Sampling data Weekly_Sales back into weekly form.<br>

###### *paramaters*

```
param_model_2 = {
    'max_depth' : [-1,7,12,14,17],
    'num_leaves' : [31,70,120],
    'min_data_in_leaf' : [60,100,120],
    'learning_rate' : [0.001,0.01,0.05],
    'num_iterations' :[200,400,600]
}
```

###### *evaluation*

```
===== CLASSIFICATION REPORT SCORING FROM F1 SCORE =====
              precision    recall  f1-score   support

           0       0.84      0.81      0.83     14561
           1       0.96      0.97      0.96     71177

    accuracy                           0.94     85738
   macro avg       0.90      0.89      0.90     85738
weighted avg       0.94      0.94      0.94     85738

tn :  11838  fp :  2723  fn :  2276  tp :  68901

======== BEST PARAMETERS SCORING FROM F1 SCORE ========
{'learning_rate': 0.05, 'max_depth': 12, 'min_data_in_leaf': 60, 'num_iterations': 600, 'num_leaves': 120}
```

### 5. Modelling
The modeling method I use in this project is ARIMA or Auto Regression Integrated Moving Average.
The main reason is, because this method is the first method I know from Purwadhika for processing time series data for forecasting purposes. Another reason is, ARIMA is a good model where, as the name suggests, this model is a combination of 2 models, namely integrated Auto Regression and Moving Average.
In modeling, I take 2 approaches, the first is by modeling using original data and the second using data that has gone through the deseason process. Then I also tried to do a test based on out of time cross validation.
Then the final step is to test the model to forecast Weekly_Sales for the next week, based on the input of the desired number of weeks.

### 6. The Evaluation
From the results that have been modeling it can be concluded that the best data used is original data because it is already stationary (based on statistical tests) and the best ARIMA model is by tuning:<br>
p = 2, d = 0, q = 0.<br>
And the results of the evaluation of the metrics are:<br>
MAPE value: 3%.<br>
Correlation value: -6%<br>
MinMax Value: 3%.<br>

The model can also produce sales target predictions for the following week, based on trends in training data.

### 7. Improvement Point of this Project
Even the model already can predict the Weekly Sales based on previously stored weekly sales data, The results provided by the model are still too broad, where the new model can only predict global weekly sales figures, not specific for each store. And as is generally known, the ARIMA model cannot be used to forecast data for a long period of time. Therefore, I personally realize that this model is not optimal. The project objectives and the selection of the algorithm model were not yet suitable. But from this project, I learned a lot about new things that I will use in the next forecasting project. thanks:). 
