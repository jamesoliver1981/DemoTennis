# Sharing the insights &amp; methods for building Mydigitaltenniscoach

This repo demonstrates some of the core work that has been done to create My Digital Tennis Coach (MDTC).  
MDTC generates insights in your match performance so you know what you need to train on, so you can improve quicker.

This repo shows how raw IoT data is evaluated, shots are identified and then how they are classified using stacked xgboost models.

### Overview

The data comes from the Apple Watch.  This is high frequency measurements of Accelerometer and Gyroscope data.  
This data will be explored in a EDA and Feature engineering notebook. (TBA)

This raw data is converted to shots upon which predictions are made.  
The predictions are based on stacked xgboost models, which exceed 90% accuracy on key shots and are expanded upon below.

All of this is then combined to points and the outcomes of these are evaluated, so the data can be visualized in the app.

Whilst the app is on the market, there are further analytics and visualisations that add greater insights.  
These will be be explored in a Visualisations notebook (TBA)

### Predictions Summary

This section gives an overview of the outcome of the model building that is demonstrated in the ["Building Highly Accurate Predictions"](https://github.com/jamesoliver1981/DemoTennis/blob/main/Building_Predictions/Building_Highly_Accurate_Shot_Predictions_in_Tennis.ipynb) notebook.  

The data used to model is already in a tabular format.  There are 8607 shots.
Each row represents 1 shot (labelled) and 366 variables.  
These variables are 61 milliseconds centred around the shot contact point and exist for each of the 3 planes around the accelerometer and gyroscope data (61*6 = 366)

The models focus on taking different time sections of the 61 milliseconds to determine which have the best predictive power.  
Some limited hyper parameter testing is done.  

The multi classification models are evaluation through accuracy evaluation & review of shot performance via cross tabs.
![Crosstab results of stacked models](https://github.com/jamesoliver1981/DemoTennis/blob/main/Images/CrossTab.png)

To boost the results, models with different set ups are blended together to get a higher overally accuracy rate.

These combinations enhance the accuracy for Backhand and Forehand to over 90%.  
![Accuracy of stacked models](https://github.com/jamesoliver1981/DemoTennis/blob/main/Images/ModelAccuracy.png)
As these are core shots in tennis, these models are used as the basis.  

Overally prediction accuracy of volleys and slice are not satisfactory and these are areas upon which further development is needed.
