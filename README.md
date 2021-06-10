# Chicago Car Crash Classification using XGBoost Classifier 

<p align="center">
  <img width="800" height="400" src="https://github.com/dicchyant84/Chicago-car-crash-classification-using-XGBoost-classifier/blob/main/Graphs/Chicago.jpg">
</p> 

## Business Case

The Vehicle Safety Board is looking to reduce the number of accidents in the City of Chicago. Utilizing the car crash data received from the Chicago Data Portal, we will perform some meaningful EDA and provide recommendations to the Vehicle Safety Board.

Firstly, we will do some data exploration to answer the following three problem statements. We will then use the results to identify areas for improvement and come up with actionable steps that will help reduce the number of accidents in the City of Chicago.

>**1. Identify high-density areas of car crash in Chicago**

>**2. Analyze control failures to identify opportunities for improvement**

>**3. Check for trends in the time of crash to relocate resources appropriately**

Furthermore, we will create a classifier to categorize the accidents in two main cateogories for future references:

>**1. Unintentional: These are events or instances where the driver was unaware of the possibility of an accident.**

>**2. Intentional: These are events or instances where the driver was fully aware of the possibility of an accident.**

--------------------------------------------------------------------------------------------------------

## EDA 1: Identify high-density areas of car crash in Chicago

![Street_map](https://github.com/dicchyant84/Chicago-car-crash-classification-using-XGBoost-classifier/blob/main/Graphs/street_map.png)

From the map above you can see there is a high density of accidents in the downtown area of Chicago. It is also mostly red, which means that most of the accidents in that area are caused due to intent or driver error. However, we can also see blue plots spread all across the map, which suggests that there are good amount of accidents that are caused unintentionally or have an opportunity of improvement. Let's dive into EDA 2 and 3 to investigate this.

In summary,

* Intentional accidents concentrated in the Downtown area.
* Even distribution of Intentional and Unintentional accidents across the city.

## EDA 2: Analyze control failures to identify opportunities for improvement

![Predictors](https://github.com/dicchyant84/Chicago-car-crash-classification-using-XGBoost-classifier/blob/main/Graphs/predictor_plots.png)

From the above plots we can make out the following deduction:

* Most of the accidents have occured when the Driver vision was 'Not Obscured' and presumably was driving at a safe speed limit of 30 mph.
* However, having 'No Traffic Control Devices' has contributed the most to the number of accidents in Chicago. According to this, increasing the number of traffic control devices in the city can lead to a decrease in the number of unintentional accidents. This is also confirmed in the Device Condition plot which shows the highest count when having no controls.
* The weather condition and lighting condition does not seem to contribute much to the accidents.
* We can also see most of the accidents occuring where the trafficway type is 'Not Divided'. This means that dividing the roads can prevent more of these accidents.
* Finally, the roadway surface condition and road defect does not seem to cause much of these accidents either.

## EDA 3: Check for trends in the time of crash to relocate resources appropriately

![Time_of_crash](https://github.com/dicchyant84/Chicago-car-crash-classification-using-XGBoost-classifier/blob/main/Graphs/time_of_crash.png)

From the above plots we can see the following trends in time of crash:
    
* Most of the crashes seem to happen between the hours of 4 to 6 in the evening. This might be due to peak rush hour traffic where every one is trying to get back home from work. When we connect this with the crash density map, we can deduce that most of the accidents in Chicago are occuring in the Downtown area during these hours where people are rushing to get home from work. There needs to be better traffic management at these times. We can recommend the city to have more facilitators in the Downtown area during these hours to help manage the flow of traffic and reduce the number of accidents.
* For day of the week, we see increased number of accidents during the weekends. However, they do not differ by much from other days. Looking at this we can say that there should be more focus on the crash hour than the crash day as the crashes dont differ much between the days.
* In terms of crash month, the crashse are pretty consistent all year long. Except for April where we the crashses are the lowest. Currently, we do not have anything to support this so we will assume crashes to be consistent all year long.

## Recommendations

1. Increase the number of traffic control devices all across the city.

2. Create divided trafficway types all across the city.

3. Increase traffic policing during the hours for 4 pm - 6pm and on the weekends.



## M/L Classifier (XGBoost)

![conf_matrix](https://github.com/dicchyant84/Accident-classification-using-XGBoost-for-Chicago-Car-Crash-Data/blob/main/Graphs/xbg_confmatx.png)

* Train accuracy is :72.35291207937024

* Test accuracy is :70.5493907566489

* AUC is :0.68

Confusion Matrix
-----------------
|Predicted |     0|      1|     All|
|True      |      |       |        |
|0         | 27731|  23766|   51497|
|1         | 11957|  57844|   69801|
|All       | 39688|  81610|  121298|


Classification Report
--------------------
|             precision    recall  f1-score   support|
|
|          0       0.70      0.54      0.61     51497|
|          1       0.71      0.83      0.76     69801|
|
|    accuracy                           0.71    121298|
|   macro avg       0.70      0.68      0.69    121298|
|weighted avg       0.70      0.71      0.70    121298|

| Predicted |     0 |     1 |    All |  
| True      |       |       |        |   
| 0         | 27731 | 23766 |  51497 | 
| 1         | 11957 | 57844 |  69801 |   
| All       | 39688 | 81610 | 121298 |   

In conclusion:

* The model has an overall accuracy of 71% and an AUC of 0.68.


* **Precision** gives us the number of times the model was able to correctly classify each category without the penalty of it being incorrect. Both 'Unintenational' and 'Intentional' catergories were classified about 70% of the time correctly.


* **Recall** gives us the exact percentage of each category that the model was able to capture. For '0' or 'Unintentional', the model was only able to only categorize 54% of those present in our data. While for '1' or 'Intenational', the model was able to categorize about 76% of those present in our data. 


* **F1-Score** is the harmonic mean between Precision and Recall. It is a better measure for model accuracy since it incorporates both precision and recall scores. In our final model, we have a f1-score of 0.61 and 0.76 for each of our categories respectively. We can use this as a final measure of our model's performance. From the difference, we can also infer that there might be some class imbalances between the two categories.


