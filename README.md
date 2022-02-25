# Background
Taken from [Kaggle West Nile Virus][1]

[1]: https://www.kaggle.com/c/predict-west-nile-virus/ "Title"
West Nile virus is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death.

In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

# Problem Statement
Taken from [Kaggle West Nile Virus][1]

[1]: https://www.kaggle.com/c/predict-west-nile-virus/ "Title"
Given weather, location, testing, and spraying data, build a machine learning model that can predict when and where different species of mosquitos will test positive for West Nile virus. A more accurate method of predicting outbreaks of West Nile virus in mosquitos will help the City of Chicago and CPHD more efficiently and effectively allocate resources towards preventing transmission of this potentially deadly virus.

# Data Dictionary

| Name |	Dataset | Description|
| --- | --- | --- |
|Date	|train/test	|Date the check for WNV was performed|
|Address|	train/test|	Approximate trap address|
|Species	|train/test	|Mosquito species caught in trap|
|Block	|train/test	|Block Number of address|
|Street	|train/test	|	Street of address|
|Trap	|train/test	|Trap ID|
|AddressNumberAndStreet	|train/test	|Approximate address |
|Latitude	|train/test|	Latitude |
|Longitude|	train/test	|Longitude |
|AddressAccuracy	|train/test	|Accuracy of address information |
|NumMosquitos	|train|Number of mosquitoes in a sample|
|WnvPresent|	train	|Whether or not WNV is present in a sample |
|Station|	weather|Station 1 or 2|
|Date	|weather	|Date of measurement|
|Tmax	|weather	|The maximum temperature for the day in degrees Fahrenheit (F).|
|Tmin|	weather|The minimum temperature for the day in degrees Fahrenheit (F).|
|Tavg|	weather	|The average temperature for the day in degrees Fahrenheit (F).|
|Depart	|weather|Departure from normal temperature. |
|DewPoint|	weather	|Average Dew Point temperature in degrees Fahrenheit (F)|
|WetBulb	|weather	|Average Wet Bulb temperature in degrees Fahrenheit (F)|
|Heat	|weather	|If Tavg is higher than 65F, how much higher|
|Cool| weather|If Tavg is lower than 65F, how much lower|
|Sunrise|	weather	|Time of sunrise|
|Sunset	|weather	|Time of sunset|
|CodeSum|	weather	|Significant weather phenomena|
|Depth|	weather	|Snow depth on the ground to the nearest inch|
|Water1	|weather|	Water depth on the ground to the nearest inch|
|SnowFall	|weather	|Snowfall for the day to the nearest tenth of an inch.|
|PrecipTotal|	weather	|Total of all forms of precipitation for the day to the nearest hundredth of an inch. |
|StnPressure	|weather|Average station pressure in hg (inches)|
|SeaLevel	|weather|Average sea level pressure in hg (inches)|
|ResultSpeed|	weather	|Resultant Wind Speed - Vector sum of wind speeds divided by number of observations (MPH)|
|ResultDir|	weather	|Resultant Wind Direction - Vector sum of wind divided by number of observations (in tens of degrees)|
|AvgSpeed	|weather	|Average wind speed (MPH)|
|Date|	spray|Date of pesticide spraying|
|Time	|spray|Time of pesticide spraying|
|Latitude	|spray|Latitude of spray location|
|Longitude	|spray	|Location of spray location|



# Methodology

1. Data cleaning and value imputation
2. Exploratory Data Analysis
3. Data modeling using Logistic Regression, K Nearest Neighbors, Gradient Boosting, AdaBoost, Support Vector Machine, Decision Tree Classifier
4. Scoring models
5. Selecting the best performing model


# Key Findings
**Model Evaluation and Selection**

Given that the train dataset is imbalanced with only 5% of cases with positive WNV, the use of accuracy as a metric for our model evaluation would be flawed.

- This is because our model would learn to disregard positive-WNV cases, and solely pick up negative-WNV cases (95% of accuracy in this case).
- Additional methods such as under-sampling or oversampling should be done to balance this dataset.
- SMOTE is an oversampling technique where the synthetic samples are generated for the minority class. This algorithm helps to overcome the overfitting problem posed by random oversampling. It focuses on the feature space to generate new instances with the help of interpolation between the positive instances that lie together.

![ROC-AUC Curve](https://github.com/KY21/GA-Project-4/blob/main/assets/roc-auc.png)

The area under the ROC curve (AUC) can be interpreted as the probability that the classification model correctly ranks a random positive example higher than a random negative example. So an AUC which is close to 1 is quite often considered to be a confirmation of the model being good.

The final model selected was the logistic regression model with an ROC score of 0.68. The model had high recall score (i.e. low false negatives) but weak precision (i.e. high false positives which might lead to wastage of vector control resources). 

Other findings include:
* Spraying should occur between July - August
* Airports are potential hotspot for mosquitos and vector control measures should be taken seriously to avoid the import nor export of infected-mosquitoes via flights
* Northern side of Chicago is at a higher risk for WNV

# Recommendations

Further steps required would include further tuning of the model to reduce misclassification. This would increase cost savings in areas identified as high-risk and in need of pesticide spraying. More data on infected patient clusters, other environment factors (e.g. bird clusters, water bodies) and new and other vector control methods (e.g. catch basins with larvicide, ) would help narrow the scope of spraying too.

Other recommendations include house inspections for possible breeding grounds for mosquitos and to provide education to homeowners on how to best manage their property. Community support is also necessary for vector control especially on private properties.

