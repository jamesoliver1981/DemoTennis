# Sharing the insights &amp; methods for building MyDigitalTennisCoach

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
These will be be explored in a Visualisations notebook.

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

Overall prediction accuracy of volleys and slice are not satisfactory and these are areas upon which further development is needed.

### Visualisations

This section shows an example of the visualisations I am considering adding to the app.  
The notebook for creating these visuals can be found [here](https://github.com/jamesoliver1981/DemoTennis/blob/main/New_Visualisations/Visualise_ServePlus_Shots.ipynb)  

As an introduction, it is important to understand that contrary to popular opinion, the majority of tennis points are short.  
This bar chart shows that 60% of points are over once you have played just 2 shots.

![Stacked bar of point lengths](https://github.com/jamesoliver1981/DemoTennis/blob/main/Images/ProportionPoints.png) 

This is a BIG realisation, and it tells us playing forehand cross forever isn't where games are won.  
We need to be training our first 2 shots in the point; the serve or return, and the +1.  

However this doesn't tell us more specifically what we need to work on, so the next chart looks to break down what happens on the serve.  
![Sunburst of 1st Serve+ Outcomes](https://github.com/jamesoliver1981/DemoTennis/blob/main/Images/Serve%2BSunburst.png)  

What does this mean?  
16% of points are won directly with serve. This is a little low so needs some work.  

57% of 1st serve points played use a serve & then a Forehand. This is good but is a little low as we want to be maximising the opportunity to attack and the forehand is the primary weapon for this.  
This ties in with the serve only percentage being a little low.  
This tells us that the serve is a little too weak and we cannot get the outcomes we need here.  

What is also telling is what happens when we play a serve + Forehand.  
Of the 57% of points played, we win 14% directly and lose 10% directly.  
The remaining 33% continue to rally - ie points where 3 or more shots are needed.  
This shows that the serve + forehand really needs to be worked on.  
